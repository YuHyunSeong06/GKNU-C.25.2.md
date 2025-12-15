## A-1
```c
#include <raylib.h>
#include <stdio.h>

// 원의 기본 속성 정의
#define CIRCLE_RADIUS 30.0f
#define MOVEMENT_SPEED 5.0f

int main(void)
{
    // 1. 초기화 (Initialization)
    // 창 크기 설정
    const int screenWidth = 800;
    const int screenHeight = 450;

    // raylib 창 초기화
    InitWindow(screenWidth, screenHeight, "raylib - Moving Circle Example");

    // 원의 초기 위치: 화면 중앙
    Vector2 circlePosition = { 
        (float)screenWidth / 2.0f, 
        (float)screenHeight / 2.0f 
    };

    // 게임 루프 실행을 위한 프레임 속도 설정 (선택 사항이지만 부드러운 움직임에 도움됨)
    SetTargetFPS(60); 

    // 2. 메인 게임 루프 (Main Game Loop)
    // 창 닫기 버튼을 누르거나 ESC 키를 누르기 전까지 루프 반복
    while (!WindowShouldClose())
    {
        // 3. 업데이트 (Update)
        // 방향키 입력 처리
        if (IsKeyDown(KEY_RIGHT)) {
            circlePosition.x += MOVEMENT_SPEED;
        }
        if (IsKeyDown(KEY_LEFT)) {
            circlePosition.x -= MOVEMENT_SPEED;
        }
        if (IsKeyDown(KEY_UP)) {
            circlePosition.y -= MOVEMENT_SPEED; // raylib에서 Y축은 아래로 증가
        }
        if (IsKeyDown(KEY_DOWN)) {
            circlePosition.y += MOVEMENT_SPEED;
        }

        // 화면 경계를 벗어나지 않도록 제한
        // X축 제한
        if (circlePosition.x < CIRCLE_RADIUS) {
            circlePosition.x = CIRCLE_RADIUS;
        } else if (circlePosition.x > screenWidth - CIRCLE_RADIUS) {
            circlePosition.x = screenWidth - CIRCLE_RADIUS;
        }

        // Y축 제한
        if (circlePosition.y < CIRCLE_RADIUS) {
            circlePosition.y = CIRCLE_RADIUS;
        } else if (circlePosition.y > screenHeight - CIRCLE_RADIUS) {
            circlePosition.y = screenHeight - CIRCLE_RADIUS;
        }
        
        // 4. 그리기 (Drawing)
        BeginDrawing();

        // 배경을 검은색으로 설정
        ClearBackground(BLACK);

        // 현재 위치에 초록색 원을 그림
        DrawCircleV(circlePosition, CIRCLE_RADIUS, LIME);

        // 현재 원의 좌표를 화면에 표시 (디버깅용)
        DrawText(TextFormat("Pos: (%.0f, %.0f)", circlePosition.x, circlePosition.y), 10, 10, 20, WHITE);
        DrawText("Use Arrow Keys to Move", 10, screenHeight - 30, 20, WHITE);


        EndDrawing();
    }

    // 5. 종료 (De-Initialization)
    // 창 및 OpenGL 컨텍스트 닫기
    CloseWindow();

    return 0;
}
```
## C-1
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
```
## C-2
```c
#include "raylib.h"
#include <stdlib.h>
#include <time.h>
#include <stdio.h>
#include <math.h>

#define SCREEN_WIDTH 800
#define SCREEN_HEIGHT 600

typedef struct {
    Color color;
    int score;
} BlockColor;

BlockColor blockColors[100];

// 게임 초기화 함수
void InitGame(int difficulty, Rectangle* paddle, Vector2* ball, Vector2* speed, int* score, int* lives, double* startTime, int* blockCount, float* paddleSpeed) {
    switch (difficulty) {
    case 1: // HARD
        paddle->width = 80;
        *speed = (Vector2){ 6, -6 };
        *blockCount = 48;
        break;
    case 2: // MEDIUM
        paddle->width = 100;
        *speed = (Vector2){ 5, -5 };
        *blockCount = 36;
        break;
    case 3: // EASY
        paddle->width = 120;
        *speed = (Vector2){ 4, -4 };
        *blockCount = 12;
        break;
    default:
        paddle->width = 100;
        *speed = (Vector2){ 5, -5 };
        *blockCount = 36;
        break;
    }

    *paddleSpeed = 8.0f;
    paddle->height = 20;
    paddle->x = SCREEN_WIDTH / 2.0f - paddle->width / 2.0f;
    paddle->y = SCREEN_HEIGHT - 30.0f;

    *ball = (Vector2){ SCREEN_WIDTH / 2.0f, SCREEN_HEIGHT / 2.0f };
    *score = 0;
    *lives = 3;
    *startTime = GetTime();

    // 블록 색상 및 점수 설정
    for (int i = 0; i < *blockCount; i++) {
        blockColors[i].score = 0;
        int colorIndex = rand() % 6;
        switch (colorIndex) {
        case 0: blockColors[i].color = RED; blockColors[i].score = 10; break;
        case 1: blockColors[i].color = ORANGE; blockColors[i].score = 7; break;
        case 2: blockColors[i].color = YELLOW; blockColors[i].score = 5; break;
        case 3: blockColors[i].color = GREEN; blockColors[i].score = 3; break;
        case 4: blockColors[i].color = BLUE; blockColors[i].score = 2; break;
        case 5: blockColors[i].color = PURPLE; blockColors[i].score = 1; break;
        }
    }
}

// 모든 블록이 제거되었는지 확인하는 함수
bool AreAllBlocksCleared(int blockCount) {
    for (int i = 0; i < blockCount; i++) {
        if (blockColors[i].score > 0) return false;
    }
    return true;
}

int main() {
    InitWindow(SCREEN_WIDTH, SCREEN_HEIGHT, "Block Breaker - Basic");
    SetTargetFPS(60);
    InitAudioDevice();

    srand((unsigned int)time(NULL));

    Rectangle paddle = { 0 }; // 초기화 추가
    Vector2 ball = { 0 };     // 초기화 추가
    Vector2 speed = { 0 };    // 초기화 추가
    int score = 0;
    int lives = 3;
    int gameState = 0; // 0: Menu, 1: Gameplay, 2: GameOver, 3: Win
    double startTime = 0;
    double totalTime = 0;
    int blockCount = 36;
    float paddleSpeed = 8.0f;
    bool flawless = true;

    // 리소스 로드
    Music bgm = LoadMusicStream("bgm.mp3");
    Sound hitSound = LoadSound("hit.wav");

    // IsMusicReady 제거 (구버전 호환성 및 링크 에러 해결)
    PlayMusicStream(bgm);

    while (!WindowShouldClose()) {
        // --- 메뉴 화면 ---
        if (gameState == 0) {
            BeginDrawing();
            ClearBackground(BLACK);
            DrawText("START PRESS KEY 1", SCREEN_WIDTH / 2 - 130, SCREEN_HEIGHT / 2 - 20, 20, WHITE);
            DrawText("QUIT PRESS KEY 0", SCREEN_WIDTH / 2 - 130, SCREEN_HEIGHT / 2 + 20, 20, WHITE);
            EndDrawing();

            if (IsKeyPressed(KEY_ONE)) {
                int difficulty = 0;
                while (difficulty < 1 || difficulty > 3) {
                    if (WindowShouldClose()) break;

                    BeginDrawing();
                    ClearBackground(BLACK);
                    DrawText("Select Level:", SCREEN_WIDTH / 2 - 100, SCREEN_HEIGHT / 2 - 40, 20, WHITE);
                    DrawText("HARD: 1, MEDIUM: 2, EASY: 3", SCREEN_WIDTH / 2 - 100, SCREEN_HEIGHT / 2, 20, WHITE);
                    EndDrawing();

                    if (IsKeyPressed(KEY_ONE)) difficulty = 1;
                    if (IsKeyPressed(KEY_TWO)) difficulty = 2;
                    if (IsKeyPressed(KEY_THREE)) difficulty = 3;
                }

                if (difficulty != 0) {
                    InitGame(difficulty, &paddle, &ball, &speed, &score, &lives, &startTime, &blockCount, &paddleSpeed);
                    flawless = true;
                    gameState = 1;
                }
                else {
                    break;
                }
            }
            if (IsKeyPressed(KEY_ZERO)) break;
        }

        // --- 게임 플레이 화면 ---
        if (gameState == 1) {
            // IsMusicReady 제거
            UpdateMusicStream(bgm);

            if (IsKeyDown(KEY_LEFT)) paddle.x -= paddleSpeed;
            if (IsKeyDown(KEY_RIGHT)) paddle.x += paddleSpeed;

            if (paddle.x < 0) paddle.x = 0;
            if (paddle.x > SCREEN_WIDTH - paddle.width) paddle.x = SCREEN_WIDTH - paddle.width;

            ball.x += speed.x;
            ball.y += speed.y;

            if (ball.x < 0 || ball.x > SCREEN_WIDTH) speed.x *= -1;
            if (ball.y < 0) speed.y *= -1;

            if (ball.y > SCREEN_HEIGHT) {
                lives--;
                flawless = false;
                ball = (Vector2){ SCREEN_WIDTH / 2.0f, SCREEN_HEIGHT / 2.0f };
                if (lives <= 0) gameState = 2;
            }

            if (CheckCollisionCircleRec(ball, 10, paddle)) {
                speed.y *= -1;
                ball.y = paddle.y - 10 - 1;
            }

            for (int i = 0; i < blockCount; i++) {
                if (blockColors[i].score > 0) {
                    // C4244 경고 해결: (float) 형변환 추가
                    Rectangle blockRect = {
                        (float)(20 + (i % 12) * 63),
                        (float)(50 + (i / 12) * 30),
                        60.0f,
                        20.0f
                    };

                    if (CheckCollisionCircleRec(ball, 10, blockRect)) {
                        score += blockColors[i].score;
                        blockColors[i].score = 0;
                        speed.y *= -1;

                        // IsSoundReady 제거
                        PlaySound(hitSound);

                        break;
                    }
                }
            }

            if (AreAllBlocksCleared(blockCount)) {
                totalTime = GetTime() - startTime;
                gameState = 3;
            }

            BeginDrawing();
            ClearBackground(BLACK);
            DrawRectangleRec(paddle, WHITE);
            DrawCircleV(ball, 10, WHITE);

            for (int i = 0; i < blockCount; i++) {
                if (blockColors[i].score > 0) {
                    DrawRectangle(20 + (i % 12) * 63, 50 + (i / 12) * 30, 60, 20, blockColors[i].color);
                }
            }

            DrawText(TextFormat("SCORE: %d", score), SCREEN_WIDTH - 150, 10, 20, WHITE);
            DrawText(TextFormat("LIFE: %d", lives), 10, 10, 20, WHITE);

            double elapsedTime = GetTime() - startTime;
            int minutes = (int)(elapsedTime / 60);
            int seconds = (int)fmod(elapsedTime, 60);
            DrawText(TextFormat("TIME: %02d:%02d", minutes, seconds), SCREEN_WIDTH - 150, SCREEN_HEIGHT - 30, 20, WHITE);
            EndDrawing();
        }

        // --- 게임 오버 ---
        else if (gameState == 2) {
            BeginDrawing();
            ClearBackground(BLACK);
            DrawText("GAME OVER!!! RESTART PRESS 'r' QUIT PRESS 'Esc'", SCREEN_WIDTH / 2 - 250, SCREEN_HEIGHT / 2, 20, WHITE);
            EndDrawing();

            if (IsKeyPressed(KEY_R)) gameState = 0;
            if (IsKeyPressed(KEY_ESCAPE)) break;
        }

        // --- 승리 ---
        else if (gameState == 3) {
            BeginDrawing();
            ClearBackground(BLACK);
            DrawText("CONGRATULATIONS! YOU WIN!", SCREEN_WIDTH / 2 - 180, SCREEN_HEIGHT / 2 - 60, 20, WHITE);
            if (flawless && totalTime <= 60.0) {
                DrawText("FLAWLESS", SCREEN_WIDTH / 2 - 120, SCREEN_HEIGHT / 2 - 10, 40, GOLD);
            }
            DrawText("RESTART PRESS 'r'  |  QUIT PRESS 'Esc'", SCREEN_WIDTH / 2 - 200, SCREEN_HEIGHT / 2 + 40, 20, WHITE);
            EndDrawing();

            if (IsKeyPressed(KEY_R)) gameState = 0;
            if (IsKeyPressed(KEY_ESCAPE)) break;
        }
    }

    // IsMusicReady, IsSoundReady 제거
    UnloadMusicStream(bgm);
    UnloadSound(hitSound);
    CloseAudioDevice();
    CloseWindow();

    return 0;
}
```
