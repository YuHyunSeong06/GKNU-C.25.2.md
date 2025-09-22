## 퀴즈시험

##### 1. 프람프트에서 명령행 매개 변수로 +, -, *, / 를 구현하는 소스코드를 적으시오
ex)calc 10+20
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char* argv[]) // main() 안에 있는 매개변수는 
{
    int a, b, c;
    char ch;
    a = atoi(argv[1]);
    b = atoi(argv[3]);
    ch = argv[2][0];
    switch (ch)
    {
    case '+': c = a + b; break;
    case '-': c = a - b; break;
    case '*': c = a * b; break;
    case '/': c = a / b; break;
    }
    printf("%d %c %d = %d\n", a, ch, b, c);
}
```
##### 2. C언어 소스코드를 비쥬얼 스튜디오 기반에서 어떤 명령을 적어서 실행하는지 과정 및 명령어를 적으시오.
```
도구 -> 명령줄 -> 개발자 명령 프롬포트 -> cls 입력해서 화면 지우기
-> notepad main.c -> 소스코드 작성 -> cl main.c를 통해 컴파일
-> lib /OUT:my.lib main.obj를 통해 라이브러리 생성
-> cl main.c my.lib 링크해서 exe 파일 만들기
-> main.exe를 통해 실행
```
##### 3. C언어 소스코드를 WSL 기반에서 어떻게 컴파일하고 실행 하는지 과정 및 명령어를 적으시오.
```
1) 필수 패키지 설치
sudo apt update
sudo apt install buil-essential

2) 코드 작성 및 컴파일 실행
nano main.c
(코드 작성)
gcc main.c -o main
./main
```
##### 4. 두 멤버 변수를 가지는 구조체를 선언하고, 값을 부여한 후 이 구조체를 함수에 전달한 값을 리턴하시오.
#####    그리고 이 값을 화면에 출력하고 하드디스크에 "my.txt"로 저장하시오
```c
#include <stdio.h>

typedef struct {
	int a;
	int b;
}Data;

int add(Data d) {
	return d.a + d.b;
}

int main() {
	Data d;
	d.a = 10;
	d.b = 20;

	int sum = add(d);

	FILE* fp = fopen("my.txt", "w");
	if (fp == NULL) return 1;

	fprintf(fp, "합계 : %d\n", sum);
	fclose(fp);

	return 0;
}
```
