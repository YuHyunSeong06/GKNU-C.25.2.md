
## 💥 C언어 벼락치기 요약 정리 (퀴즈 대비용)

---

### **1️⃣ 1부터 10까지 숫자를 더해서 화면에 출력하는 “슈도코드”**

**✅ 정답**

```
START
  sum ← 0
  FOR i ← 1 TO 10 DO
      sum ← sum + i
  END FOR
  PRINT sum
END
```

**💡핵심:**
반복문으로 1~10을 더해 `sum`에 누적 → 최종 출력

---

### **2️⃣ 1부터 10까지 숫자를 더하는 프로그램의 “플로우차트”**
<img width="420" height="348" alt="image" src="https://github.com/user-attachments/assets/8224a126-e8cb-4659-89a9-f6b30644bf4e" />
**✅ 텍스트형 플로우차트**

```
[시작]
   ↓
sum = 0, i = 1
   ↓
[i ≤ 10 ?]
 ├─ 예 → sum = sum + i
 │       i = i + 1
 │       ↺ (조건으로 돌아감)
 └─ 아니오
   ↓
PRINT sum
   ↓
[끝]
```

**💡핵심:**
조건 확인 → 더하기 → 증가 → 반복
(기본적인 for 루프 흐름 구조)

---

### **3️⃣ 1부터 10까지 중 3의 배수를 출력하는 코드**

**✅ 정답**

```c
#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 10; i++) {
        if (i % 3 == 0)
            printf("%d\n", i);
    }
    return 0;
}
```

**💡핵심:**
`%`는 나머지 → `i % 3 == 0`이면 3의 배수

---

### **4️⃣ Bubble Sort (버블 정렬)**

**✅ 코드**

```c
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main(void) {
    int arr[5] = {5, 2, 4, 1, 3};
    bubbleSort(arr, 5);

    for (int i = 0; i < 5; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

**💡핵심:**
옆의 원소끼리 비교 → 큰 값을 뒤로 보냄
한 바퀴 돌면 가장 큰 값이 맨 뒤로 이동 (거품처럼!)

---

### **5️⃣ Quick Sort (퀵 정렬)**

**✅ 핵심 원리 요약**

1. **피벗(pivot)** 하나 선택 (보통 마지막 값)
2. 피벗보다 **작은 값은 왼쪽**, **큰 값은 오른쪽**
3. 양쪽 부분 배열을 **재귀 호출**로 다시 정렬

**✅ 코드**

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int left, int right) {
    int pivot = arr[right];
    int i = left - 1;

    for (int j = left; j < right; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[right]);
    return i + 1;
}

void quickSort(int arr[], int left, int right) {
    if (left < right) {
        int pi = partition(arr, left, right);
        quickSort(arr, left, pi - 1);
        quickSort(arr, pi + 1, right);
    }
}

int main(void) {
    int arr[8] = {8, 2, 5, 1, 9, 3, 7, 6};
    int n = 8;

    quickSort(arr, 0, n - 1);

    printf("정렬 결과: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

**💡핵심 포인트:**
“피벗을 기준으로 왼쪽은 작게, 오른쪽은 크게”
재귀 호출로 정렬 완료.

---

### **6️⃣ WSL 명령행 매개변수로 두 수 더하기**

**✅ 코드**

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("사용법: %s <num1> <num2>\n", argv[0]);
        return 1;
    }

    int a = atoi(argv[1]);
    int b = atoi(argv[2]);
    printf("%d + %d = %d\n", a, b, a + b);
    return 0;
}
```

**✅ WSL 실행 예시**

```bash
$ gcc add.c -o add
$ ./add 11 22
11 + 22 = 33
```

**💡핵심:**

* `argc`: 인자 개수
* `argv[]`: 인자 값(문자열 배열)
* `atoi()`: 문자열을 정수로 변환

---

### **7️⃣ 공용체 (union)**

**✅ 정의:**
여러 변수가 **같은 메모리 공간**을 공유하는 자료형.

**✅ 예시**

```c
union Data {
    int i;
    float f;
    char c;
};
```

**✅ 특징**

* 한 시점에 **하나의 멤버만 유효**
* 메모리 절약 가능 (공유 메모리 구조)
* 마지막에 저장된 값만 정확히 읽힘

**💡주의:**
모든 멤버가 같은 메모리를 사용하기 때문에
이전에 넣은 값은 덮어써짐.

---

### **8️⃣ 열거형 (enum)**

**✅ 정의:**
관련된 상수들을 **의미 있는 이름으로 묶은 자료형**

**✅ 예시**

```c
enum Week { MON, TUE, WED, THU, FRI, SAT, SUN };
```

**✅ 특징**

* 기본값은 0부터 시작
* 코드 가독성 ↑
* 내부적으로는 **정수형**

**💡주의:**
서로 다른 enum 간에는 같은 이름 중복 불가.

---

### **9️⃣ 코드 결과 예측 문제**

**문제 코드**

```c
#include <stdio.h>
typedef enum { 
    RED, YELLOW, GREEN 
} TL;

int main(void) {
    TL light = GREEN;
    printf("%d\n", GREEN);
    switch (light) {
        case RED:    printf("멈춤!\n"); break;
        case YELLOW: printf("주의!\n"); break;
        case GREEN:  printf("출발!\n"); break;
        default: printf("오류");
    }
    return 0;
}
```

**✅ 출력 결과**

```
2
출발!
```

**💡이유**

* `RED=0, YELLOW=1, GREEN=2`
* `light=GREEN` → `case GREEN` 실행
  → `"출발!"` 출력

---

## 🚀 총정리 한눈 요약

| 번호 | 주제          | 핵심 키워드           |
| -- | ----------- | ---------------- |
| 1  | 1~10 합 슈도코드 | for문, 누적합        |
| 2  | 플로우차트       | 조건, 반복 구조        |
| 3  | 3의 배수 출력    | if, 나머지 연산       |
| 4  | 버블정렬        | 이웃 비교, 교환        |
| 5  | 퀵정렬         | 피벗, 분할, 재귀       |
| 6  | 명령행 매개변수    | argc, argv, atoi |
| 7  | 공용체         | 메모리 공유, 한 멤버만 유효 |
| 8  | 열거형         | 이름 있는 상수, 정수형    |
| 9  | enum 코드 결과  | 2, “출발!” 출력      |

---
