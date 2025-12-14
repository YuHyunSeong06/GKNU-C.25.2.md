# 기말고사 준비
###### 자료구조 5가지
###### 스택(LIFO), 리스트, 큐(FIFO), 이진 트리, 해시(hash)
###### 알고리즘 5가지
###### 퀵소트 구현
###### 연결리스트 구현

### 1. Visual Studio 환경에서 두 함수 add.c sub.c를 my.lib로 만들고 main.c에서 호출할 때 사용하는 명령을 차례대로 적으시오.
```
notepad add.c
(코드 작성)
notepad sub.c
(코드 작성)
notepad main.c
(코드 작성)
cl /c add.c // cl /c는  "Compile only, do not link"
cl /c sub.c
cl /c main.c
lib /OUT:my.lib add.obj sub.obj
cl main.c my.lib
main.exe
```
### 2.wsl에서 두 함수 add.c sub.c를 main.c에서 호출하는 프로젝트의 make문을 작성하시오.
```
main: main.o add.o sub.o
	gcc -o main main.o add.o sub.o

main.o: main.c
	gcc -c main.c

add.o: add.c
	gcc -c add.c

sub.o: sub.c
	gcc -c sub.c
```

### 3.C언어의 대표적인 자료구조 5가지
```
리스트 스택 큐 트리 해시
```

### 4.메모리에 두 수를 저장하고 그 중에 작은 수를 출력하는 "슈도 코드"를 작성하시오
```
a ← 7
b ← 3

IF a ≤ b THEN
    PRINT a
ELSE
    PRINT b
END IF
```

### 5.메모리에 두 수를 저장하고 그 중에 작은 수를 찾는 "플로우 차트"를 그리시오.
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/dc0ecd95-459d-45de-baa7-0806da255570" />

### 6.1부터 50까지 중에 5의 배수를 출력하는 코드를 작성하시오.
```c
#include <stdio.h>

int main(void) {
    // 1부터 50까지 반복 (i < 51 이므로 50까지 포함됨)
    for(int i = 1; i < 51; i++) {
        if(i % 5 == 0) {
            printf("%d\n", i); // 숫자 뒤에 줄 바꿈(\n) 추가
        }
    }
    return 0; // main 함수 종료 시 0 반환
}
```

### 7. 명랭행 프롬포트에서 다음처럼 입력할 때 +와 -, *, /가 실행 된는 계산기 프로그램을 switch 문으로 구현하시오
```
c:\temp\>math 10 + 20
c:\temp\>math 10 * 20
```
```
md c:\temp
cd c:\temp
notepad math.c
```
```c
#include <stdio.h>
#include <stdlib.h> // atoi 함수 사용을 위해 필요

int main(int argc, char* argv[]) {
    // (프로그램 이름, 숫자1, 연산자, 숫자2) => 총 4개

    // 명령줄 인수를 숫자로 변환
    int a = atoi(argv[1]);     // 첫 번째 인수 (숫자1)
    char op = argv[2][0];      // 두 번째 인수 (연산자, 첫 글자만 사용)
    int b = atoi(argv[3]);     // 세 번째 인수 (숫자2)
    int r = 0;

    switch (op) {
        case '+':
            r = a + b;
            break;
        case '-': 
            r = a - b;
            break;
        case '*':
            r = a * b;
            break;
        case '/': 
	    r = a / b;
            break;
        default:
            break;
    }

    printf("결과: %d\n", r);
    return 0; // 정상 종료
}
```
```
cl math.c
math 10 + 20
math 10 * 20
```
