# ✅ QUIZ

---

## **1. Visual Studio 환경에서 my.lib 생성 및 main.c에서 호출**

```
cl /c *.c
lib /OUT:my.lib add.obj sub.obj
link main my.lib
```

---

## **2. WSL Makefile**

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

## **3. 대표적인 C 자료구조 5가지**

* 리스트(List)
* 스택(Stack)
* 큐(Queue)
* 배열(Array)
* 구조체(Struct)

---

## **4. 작은 수를 출력하는 슈도코드**

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

## **5. 작은 수를 찾는 플로우차트**

(사용자 버전 유지 — 필요하면 그림으로 다시 만들어 드릴게요.)

---

## **6. 1부터 50까지 5의 배수 출력 코드**

```c
#include <stdio.h>

int main(void) {
    for (int i = 5; i <= 50; i += 5)
        printf("%d\n", i);
}
```

---

## **7. switch를 이용한 명령행 계산기**

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char* argv[]) {
    int a = atoi(argv[1]);
    char op = argv[2][0];
    int b = atoi(argv[3]);
    int r = 0;

    switch (op) {           // 연산자에 따라 분기
        case '+': r = a + b; break;
        case '*': r = a * b; break;
        default: break;
    }

    printf("%d\n", r);
    return 0;
}
```

---

## **8. 퀵정렬 알고리즘 (핵심 주석 버전)**

```c
#include <stdio.h>

void q(int* a, int l, int r) {
    if (l >= r) return;          // 원소 1개 이하 → 종료

    int i = l - 1, pivot = a[r], t;

    // partition 과정: pivot보다 작은 값들은 왼쪽으로 이동
    for (int j = l; j < r; j++) {
        if (a[j] < pivot) {
            t = a[++i];
            a[i] = a[j];
            a[j] = t;
        }
    }

    // pivot을 제자리에 배치
    t = a[i + 1];
    a[i + 1] = a[r];
    a[r] = t;

    q(a, l, i);         // pivot 기준 왼쪽
    q(a, i + 2, r);     // pivot 기준 오른쪽
}

int main(void) {
    int v[] = {4, 5, 1, 2, 3};
    int n = sizeof v / sizeof *v;

    q(v, 0, n - 1);

    for (int i = 0; i < n; i++) printf("%d ", v[i]);
    return 0;
}
```

---

## **9. 버블 정렬 (핵심 주석 버전)**

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

## **10. enum, struct, union이 포함된 코드 (핵심 주석 버전)**

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

## **11. 피보나치 수열 (메모이제이션, 핵심 주석만)**

```c
#include <stdio.h>

int dp[50];

int fibonacci(int n) {
    if (n == 1 || n == 2) return 1;   // 기본값

    if (dp[n] != 0)                   // 이미 계산한 값이면 재사용
        return dp[n];

    return dp[n] = fibonacci(n-1) + fibonacci(n-2);  // 값 저장
}

int main(void) {
    printf("%d\n", fibonacci(5));
    return 0;
}
```

---

# 📌 추가 설명 — **enum과 union 개념**

## ✅ **enum (열거형)**

* "정수 상수에 이름을 붙여주는" 자료형
* 코드 가독성 상승
* 내부적으로는 **정수(int)** 로 저장됨

예:

```c
enum Color { RED, GREEN, BLUE };
```

→ `RED=0, GREEN=1, BLUE=2` 자동 부여
(값을 직접 지정할 수도 있음)

✔ 사용 이유

* 상태, 옵션, 종류 등을 정해진 값으로 표현할 때 좋음
* 코드 의미가 명확해짐

---

## ✅ **union (공용체)**

* **여러 멤버가 ‘같은 메모리 공간’을 공유**
* struct와의 차이:

  * struct → 멤버 각각 **다른 공간**
  * union → 모든 멤버가 **같은 공간 공유**

예:

```c
union Data {
    int i;
    float f;
    char* s;
};
```

✔ 특징

* "오직 하나의 멤버 값만 유효"
* 메모리 절약할 때 유용
* 실제로 어떤 멤버가 유효한지는 **사용자가 따로 표시해야 함**

그래서 enum과 함께 자주 사용됨:

```c
enum { TYPE_INT, TYPE_STR };
struct {
    int type;
    union {
        int i;
        char* s;
    } u;
};
```

즉:
**“지금 union 안에는 어떤 데이터가 들어있는지 enum으로 표시하는 방식”**

---

