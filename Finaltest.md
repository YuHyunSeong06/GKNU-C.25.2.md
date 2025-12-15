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
---

### 2. wsl에서 두 함수 add.c sub.c를 main.c에서 호출하는 프로젝트의 make문을 작성하시오.
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
---

### 3. C언어의 대표적인 자료구조 5가지
```
리스트 스택 큐 트리 해터
```

---

### 4. 메모리에 두 수를 저장하고 그 중에 작은 수를 출력하는 "슈도 코드" 작성하시오.
```
a ← 7
b ← 3

IF a ≤ b THEN
    PRINT a
ELSE
    PRINT b
END IF
```
---

### 5. 메모리에 두 수를 저장하고 그 중에 작은 수를 찾는 "플로우 차트"를 그리시오.

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/8cd3d0a0-bf2a-45b6-9e06-310f899c8bcc" />

---

### 6. 1부터 50까지 중에 5의 배수를 출력하는 코드를 작성하시오.
```c
#include <stdio.h>

int main(void) {
    // 1부터 50까지 반복 (i < 51 이므로 50까지 포함됨)
    for(int i = 1; i < 51; i++) {
        if(i % 5 == 0) {
            printf("%d\n", i); // 숫자 뒤에 줄 바꿈(\n) 추가
        }
    }
    return 0; // main 함수 종료 시 0 반환 (좋은 습관)
}
```

---

### 7. 명령행 프롬프트에서 다음처럼 입력할때 '+' 와 '-' '*' '/' 가 실행되는 계산기 프로그램 구현
```
md c:/temp
cd c:/temp
notepad math.c
```
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char* argv[]) {
    int a = atoi(argv[1]);
    char op = argv[2][0];
    int b = atoi(argv[3]);
    int r = 0;

    switch (op) {
        case '+': r = a + b; break;
        case '-': r = a - b; break;
        case '*': r = a * b; break;
        case '/': r = a / b; break;
        default: break;
    }
    printf("결과: %d\n", r);
    return 0;
}
```
```
cl math.c
math 10 + 20
math 10 * 20
```
---

### 8.퀵소트 알고리즘을 완성하시오.
```c
#include <stdio.h>

void q(int* a, int l, int r) {
    if (l >= r) return;

    // 로무토 분할 (Lomuto Partition)
    int p = a[r]; // 피벗 (가장 오른쪽 요소)
    int i = l - 1; 
    int t; // 교환을 위한 임시 변수

    for (int j = l; j < r; j++) {
        if (a[j] <= p) {
            // 작은 요소를 발견하면 i를 증가시키고 교환
            t = a[++i];
            a[i] = a[j];
            a[j] = t;
        }
    }

    // 피벗(a[r])을 정렬 위치 (i+1)로 이동
    t = a[i + 1];
    a[i + 1] = a[r]; 
    a[r] = t;

    // 재귀 호출: 피벗을 제외한 왼쪽 부분 배열 정렬
    q(a, l, i); 
    
    // 재귀 호출: 피벗을 제외한 오른쪽 부분 배열 정렬
    q(a, i+2, r); 
}

int main() {
    int a[] = { 5, 2, 3, 1, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    // [수정] q(a, 0, n-1)로 올바른 인수를 전달
    q(a, 0, n - 1); 

    for (int i = 0; i < n; i++) {
        printf("%d ", a[i]);
    }
    printf("\n");
    
    return 0;
}
```
### 시뮬레이션 1문항
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void main() {
	int h[6] = { 0 };
	srand(time(NULL));
	for (int i = 0; i < 60;i++) {
		int n = rand();
		n = n % 6;
		h[n] = h[n] + 1;
	}
```
	for (int j = 0;j < 6;j++) {
		printf("[%d]=%d\n", j+1,h[j]);
	}
}
```
