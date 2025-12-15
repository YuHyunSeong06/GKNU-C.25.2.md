C-1
```c
#include <raylib.h>
#include <stdlib.h> // rand(), srand()
#include <time.h>   // time()

// ----------------------------------------------------------------------------------
// 상수 및 구조체 정의
// ----------------------------------------------------------------------------------
#define SCREEN_WIDTH  480
#define SCREEN_HEIGHT 700
#define LANE_COUNT    4
#define MAX_OBSTACLES 20

// 게임 화면 상태 정의
typedef enum {
    MENU = 0,
    GAMEPLAY,
    ENDING
} GameScreen;

// 장애물 구조체
typedef struct {
    int lane;       // 0 ~ 3 (어느 칸에 있는지)
    float y;        // y 좌표
    bool active;    // 현재 화면에 활성화되어 있는지 여부
} Obstacle;

// ----------------------------------------------------------------------------------
// 메인 함수
// ----------------------------------------------------------------------------------
int main(void)
{
    // 1. 초기화
    InitWindow(SCREEN_WIDTH, SCREEN_HEIGHT, "Avoid The Blocks");
    SetTargetFPS(60);

    // 랜덤 시드 설정 (매번 다른 패턴)
    srand((unsigned int)time(NULL));

    // 게임 변수
    GameScreen currentScreen = MENU;
    int laneWidth = SCREEN_WIDTH / LANE_COUNT;

    // 플레이어 설정
    int playerLane = 1; // 0, 1, 2, 3 중 초기 위치
    float playerRadius = 25.0f;
    float playerY = SCREEN_HEIGHT - 80.0f; // 플레이어 고정 Y 위치

    // 장애물 설정
    Obstacle obstacles[MAX_OBSTACLES] = { 0 };
    float obstacleSpeed = 6.0f;
    int obstacleSpawnTimer = 0;

    // 2. 메인 게임 루프
    while (!WindowShouldClose())    // ESC키를 누르면 루프 종료 (기본 동작)
    {
        // ------------------------------------------------------------------------------
        // 업데이트 (Update) - 게임 로직 처리
        // ------------------------------------------------------------------------------
        switch (currentScreen)
        {
        case MENU:
        {
            // SPACE를 누르면 게임 시작
            if (IsKeyPressed(KEY_SPACE))
            {
                // 게임 변수 초기화 (재시작 시 필요)
                playerLane = 1;
                obstacleSpeed = 6.0f;
                obstacleSpawnTimer = 0;
                for (int i = 0; i < MAX_OBSTACLES; i++) obstacles[i].active = false;

                currentScreen = GAMEPLAY;
            }
            // ESC는 WindowShouldClose()에 의해 자동 처리되므로 별도 로직 불필요
        } break;

        case GAMEPLAY:
        {
            // 1) 플레이어 이동 (칸 단위 이동)
            if (IsKeyPressed(KEY_LEFT))
            {
                playerLane--;
                if (playerLane < 0) playerLane = 0; // 왼쪽 벽 막힘
            }
            else if (IsKeyPressed(KEY_RIGHT))
            {
                playerLane++;
                if (playerLane >= LANE_COUNT) playerLane = LANE_COUNT - 1; // 오른쪽 벽 막힘
            }

            // 2) 장애물 생성 (타이머)
            obstacleSpawnTimer++;
            if (obstacleSpawnTimer > 40) // 약 0.6초마다 생성 (60FPS 기준)
            {
                obstacleSpawnTimer = 0;

                // 비활성화된 장애물 슬롯을 찾아 새로 생성
                for (int i = 0; i < MAX_OBSTACLES; i++)
                {
                    if (!obstacles[i].active)
                    {
                        obstacles[i].active = true;
                        obstacles[i].lane = rand() % LANE_COUNT; // 0~3 랜덤 레인
                        obstacles[i].y = -100; // 화면 위에서 시작
                        break;
                    }
                }

                // 시간이 지날수록 난이도(속도) 상승 (선택 사항)
                if (obstacleSpeed < 12.0f) obstacleSpeed += 0.05f;
            }

            // 3) 장애물 이동 및 충돌 체크
            // 플레이어의 실제 화면 좌표 계산 (충돌 체크용)
            Vector2 playerCenter = { (float)(playerLane * laneWidth + laneWidth / 2), playerY };

            for (int i = 0; i < MAX_OBSTACLES; i++)
            {
                if (obstacles[i].active)
                {
                    obstacles[i].y += obstacleSpeed;

                    // 화면 아래로 벗어나면 비활성화
                    if (obstacles[i].y > SCREEN_HEIGHT)
                    {
                        obstacles[i].active = false;
                    }

                    // 충돌 감지 (원 vs 직사각형)
                    // 직사각형 영역 정의
                    Rectangle obstacleRect = {
                        (float)obstacles[i].lane * laneWidth, // x
                        obstacles[i].y,                       // y
                        (float)laneWidth,                     // width
                        60.0f                                 // height (장애물 높이)
                    };

                    if (CheckCollisionCircleRec(playerCenter, playerRadius, obstacleRect))
                    {
                        currentScreen = ENDING; // 게임 오버!
                    }
                }
            }
        } break;

        case ENDING:
        {
            // 엔딩 화면에서 스페이스바를 누르면 메뉴로 복귀 (혹은 바로 재시작)
            if (IsKeyPressed(KEY_SPACE))
            {
                currentScreen = MENU;
            }
        } break;
        default: break;
        }

        // ------------------------------------------------------------------------------
        // 그리기 (Draw) - 화면 렌더링
        // ------------------------------------------------------------------------------
        BeginDrawing();

        ClearBackground(BLACK); // 배경 검은색

        switch (currentScreen)
        {
        case MENU:
        {
            // 타이틀 그리기
            const char* title = "AVOID";
            int titleWidth = MeasureText(title, 80);
            DrawText(title, SCREEN_WIDTH / 2 - titleWidth / 2, SCREEN_HEIGHT / 4, 80, GREEN);

            // 안내 문구
            const char* msg1 = "Start to SPACE BAR";
            const char* msg2 = "Quit to ESC";

            int msg1Width = MeasureText(msg1, 30);
            int msg2Width = MeasureText(msg2, 30);

            DrawText(msg1, SCREEN_WIDTH / 2 - msg1Width / 2, SCREEN_HEIGHT / 2, 30, WHITE);
            DrawText(msg2, SCREEN_WIDTH / 2 - msg2Width / 2, SCREEN_HEIGHT / 2 + 50, 30, GRAY);
        } break;

        case GAMEPLAY:
        {
            // 1) 레인 구분선 그리기 (시각적 도움)
            for (int i = 1; i < LANE_COUNT; i++)
            {
                DrawLine(i * laneWidth, 0, i * laneWidth, SCREEN_HEIGHT, DARKGRAY);
            }

            // 2) 플레이어(원) 그리기
            // 현재 레인의 중앙 X 좌표 계산
            int playerCenterX = playerLane * laneWidth + laneWidth / 2;
            DrawCircle(playerCenterX, (int)playerY, playerRadius, WHITE);

            // 3) 장애물(직사각형) 그리기
            for (int i = 0; i < MAX_OBSTACLES; i++)
            {
                if (obstacles[i].active)
                {
                    // 해당 레인의 꽉 차는 너비로 그림
                    DrawRectangle(
                        obstacles[i].lane * laneWidth,
                        (int)obstacles[i].y,
                        laneWidth,
                        60, // 장애물 높이
                        RED
                    );
                }
            }

            // 점수나 상태 표시 (선택)
            DrawText("Dodge!", 10, 10, 20, DARKGRAY);

        } break;

        case ENDING:
        {
            // 게임 플레이 장면을 배경에 흐릿하게 남겨둘 수도 있지만, 여기서는 검은 배경에 텍스트만 출력
            const char* text = "GAME OVER";
            int textWidth = MeasureText(text, 60);
            DrawText(text, SCREEN_WIDTH / 2 - textWidth / 2, SCREEN_HEIGHT / 3, 60, RED);

            const char* sub = "Press SPACE to Return Menu";
            int subWidth = MeasureText(sub, 20);
            DrawText(sub, SCREEN_WIDTH / 2 - subWidth / 2, SCREEN_HEIGHT / 2, 20, WHITE);
        } break;
        default: break;
        }

        EndDrawing();
    }

    // 3. 종료
    CloseWindow();

    return 0;
}
````
