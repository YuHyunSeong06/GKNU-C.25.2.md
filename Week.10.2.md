# 퀴즈 2 내용
##### 1. 1부터 10까지 숫자를 더해서 화면에 출력하는 “슈도코드”를 작성하시오.
```
sum ← 0
for i ← 1 to 10
    sum ← sum + i
print sum 
```
##### 2. 1부터 10까지 숫자를 더하는 프로그램의 “플로우 차트”를 그리시오.\
<img width="420" height="348" alt="image" src="https://github.com/user-attachments/assets/8224a126-e8cb-4659-89a9-f6b30644bf4e" />

##### 3. 1부터 10까지 중에 3의 배수를 화면에 출력하는 C언어 코드를 작성하시오.
##### 4. {3,4,1,5,2}를 함수에 전달하고 최댓값을 구하는 C언어 코드를 작성하시오
###### 함수 전달 ver
```c
#include <stdio.h>

#define MAX(a, b) ((a) > (b) ? (a) : (b)) // 매크로 함수

int main(void) {
    int a[] = {3, 1, 2, 5, 4};
    int n = sizeof(a) / sizeof(a[0]);
    int max = a[0];

    for (int i = 1; i < n; i++) {
        max = MAX(max, a[i]);
    }

    printf("최댓값: %d\n", max);
    return 0;
}
```
###### 반복문 이용
```c
#include <stdio.h>

int main(void) {
    int a[] = {3, 1, 2, 5, 4};
    int n = sizeof(a) / sizeof(a[0]);  // 원소 개수
    int max = a[0];                    // 첫 원소로 초기화

    for (int i = 1; i < n; i++) {
        if (a[i] > max) {
            max = a[i];
        }
    }

    printf("최댓값: %d\n", max);
    return 0;
}
```
