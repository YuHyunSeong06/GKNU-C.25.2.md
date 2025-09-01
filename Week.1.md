# 프로그래밍 심화

###### - 통합 컴파일러 Dev-C++ 및 Visual Studio, VC++을 잘 활용할 수 있다.
###### - Github의 C언어 작성 된 코드를 이해하고 수정할 수 있다.
###### - C언어로 주사위 시뮬레이션 코딩을 할 수 있다.
###### - 파일에서 데이터를 읽고 특정한 내용을 C언어로 검색할 수 있다.
###### - 알고리즘(순서정렬 등)을 C언어로 구현할 수 있다.
###### - 데이터 구조(스택 등)를 C언어로 구현할 수 있다.
###### - OpenGL을 활용한 그래픽스를 C언어로 연동할 수 있다.
###### - C언어 응용 라이브러리를 작성 할 수 있다.
###### - 리눅스 환경에서 C언어를 make를 사용하여 컴파일 할 수 있다.

### 성적 산출
##### 출석 10% 시험 50% ( 퀴즈1 5%, 중간고사 20%, 퀴즈2 5%, 기말고사 20% 리포트, 실습기타 40%, 태도 10%)

###### 25.09.01 첫번째 교시
### 기초적인 Welcome GKNU! 출력
```c
#include <stdio.h>

void main() {
	printf("Welcome GKNU!\n");
}
```

### OpenGL 기반의 raylib를 통한 창 띄우기
##### - NuGet에서 raylib를 다운받을 수 있다. 
##### - 프로젝트 -> 속성 -> 링커 -> 시스템 ( 창 window) -> 고급 -> 진입점(mainCRTStarup)
```c
#include "raylib.h"

int main(void)
{
    InitWindow(800, 450, "raylib [core] example - basic window");

    while (!WindowShouldClose())
    {
        BeginDrawing();
        ClearBackground(GREEN);
        DrawText("Congrats! You created your first window!", 150, 200, 35, BLACK);
        EndDrawing();
    }

    CloseWindow();

    return 0;
}

```

### OpenGL 기반의 raylib를 통해서 하얀 배경에 원 그리기
```c
#include "raylib.h"

int main(void)
{
    InitWindow(800, 450, "GKNU");

    while (!WindowShouldClose())
    {
        BeginDrawing();
        ClearBackground(RAYWHITE);
        DrawCircle(400, 225, 150, GREEN);
        /*DrawText("Congrats! You created your first window!", 150, 200, 35, BLACK);*/
        EndDrawing();
    }

    CloseWindow();

    return 0;
}
```
###### 25.09.01 두번째 교시

### 명령줄 프롬포트를 이용하여 메모장을 통한 코딩
##### 도구 -> 명령줄 -> 개발자 명령 프롬포트 -> 콘솔창에 cls(화면 지우기) 입력 -> notepad add.c를 통해 메모장 생성
```c
#include <stdio.h>

void main(){
	printf("GKNU\n");
}
```
##### 다음 코드를 입력 -> dir 입력해 디렉토리 확인 -> cl add.c 입력해 컴파일러 생성 -> 코드 변경
##### GKNU를 5번 출력하고 각 순번을 뒤에 매기는 코드
```c
#include <stdio.h>

void main(){
	int i;
	for(i=1;i<=5;i++){
		printf("GKNU%d\n",i);
	}
}
```
##### 변형 1
```c
#include <stdio.h>

void main(){
	int i=1;
	for(;;i++){
		printf("GKNU%d\n",i);
		if(i>5) break;
	}
}
```
##### 변형 2
```c
#include <stdio.h>

void main(){
	int i=1;
	for(;;){
		printf("GKNU%d\n",i);
		if(++i>5) break;
	}
}
```
##### while을 통한 변형 1
```c
#include <stdio.h>

void main(){
	int i=0;
	while(i++<5){
		printf("GKNU%d\n",i);
	}
}
```
