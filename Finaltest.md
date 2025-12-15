# 기말고사 준비
###### 자료구조 5가지
###### 스택(LIFO), 리스트, 큐(FIFO), 이진 트리, 해시(hash)
###### 알고리즘 5가지
###### 퀵소트 구현
###### 연결리스트 구현
---
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

### 2. WSL에서 두 함수 add.c sub.c를 main.c에서 호출하는 프로젝트의 make문을 작성하시오.
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
리스트 스택 큐 트리 해시 포인터 구조체 배열
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
---
### 9. 순서정렬 알고리즘을 코딩하시오
```c
#include <stdio.h>

// 인접한 두 값을 비교하여 큰 값을 뒤로 보내는 정렬
void bubble(int a[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - 1 - i; j++)
            if (a[j] > a[j + 1]) {
                int t = a[j];
                a[j] = a[j + 1];
                a[j + 1] = t;
            }
}

int main(void) {
    int a[] = {5, 1, 4, 2, 8};
    int n = sizeof(a) / sizeof(a[0]);

    bubble(a, n);

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
    return 0;
}
```
---
### 10. 다음 C언어 코드에 적합한 키워드를 넣으시오.
```c
#include <stdio.h>

typedef enum { RES_OK, RES_ERR } ResKind;   // 상태 구분

typedef struct {
    ResKind kind;    // 현재 상태
    union {          // 같은 메모리를 공유
        int value;           // 성공 시 값
        const char* msg;     // 실패 시 메시지
    } u;
} Result;

int main(void) {
    Result ok  = { RES_OK,  .u.value = 123 };
    Result err = { RES_ERR, .u.msg = "oops" };

    if (ok.kind == RES_OK)
        printf("OK: %d\n", ok.u.value);
    else
        printf("ERR: %s\n", ok.u.msg);

    return 0;
}
```
---

### 자료구조 1문항
```c
#include <stdio.h>

typedef struct Node {
	int data;
	struct Node* next;
}Node;

int main(void) {
	Node n1, n2, n3;

	n1.data = 3; n2.data = 2; n3.data = 1;
	n1.next = &n2; n2.next = &n3; n3.next = NULL;

	Node* head = &n1; // head는 3을 가리키도록
	Node* p = head;

	while (p != NULL) {
		printf("%d -> ", p->data);
		p = p->next;
	}
	printf("NULL\n");
	return 0;
}
```
---

### 알고리즘 1문항
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
```
```c
재귀함수
#include <stdio.h>
int fact(int n) {
    if(n == 1) return 1;
    return n * fact(n-1);}
int main() {
    printf("5!: %d\n", fact(5));
    return 0;
}
```
---

### 시뮬레이션 1문항
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
	int heads = 0;
	int tails = 0;
	srand(time(NULL));
	for (int i = 0; i < 1000;i++) {
		if (rand() % 2 == 0)
			heads++;
		else
			tails++;
	}
	printf("앞면 : %d회 \n뒷면 : %d회", heads, tails);
}
```
