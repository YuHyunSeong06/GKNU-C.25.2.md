# WSL 환경
## WSL 환경에서 두 수를 더하기
###### wsl -> nano test7.c
```c
#include <stdio.h> // printf();
#include <stdlib.h> // atoi(test 11 33) 11->11 atoi("11"); 11

void main(int argc, char* argv[]){
        int a,b,s;
        a = atoi(argv[1]);
        b = atoi(argv[2]);
        s = a + b;
        printf("%d\n",s);
}
```
##### ^x y enter를 통해 코드를 저장
##### more test7.c를 통해 코드 상태를 확인
##### gcc test7.c -> ./a.out 11 33 -> 44출력
##### gcc -o run test7.c -> ./run 11 33 -> 44출력
##### 두 가지 방식으로 사용이 가능하다

## swap 함수로 두 수를 교환하기
##### nano test.c
```c
#include <stdio.h> // printf();
#include <stdlib.h> // atoi(test 11 33) 11->11 atoi("11"); 11

void swap(int* a, int* b){ // 받을때는 포인터로 받기
        int p = *a;
        *a = *b;
        *b = p;
}

int main(void){
        int v[2]={11,33};
        swap(&v[0],&v[1]); // 보낼때는 주소로 보내기
        printf("%d %d\n",v[0],v[1]);
}
```
##### gcc -o run test7.c -> ./run test7.c -> 33 11 출력
# 알고리즘 
##### 수학적 알고리즘, 누적합, 정렬, 탑색, 재귀 등 
##### https://cafe.naver.com/jclang?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30916880%2526articleid%3D366%2526referrerAllArticles%3Dtrue
## psudo code 슈도 코드 
#### 이해하기쉽게 표현한 코드
##### 1부터 10까지 더하고 결과를 화면에 출력하는 슈도 코드
```
sum <- 0
for i <- 1 to 10
        sum <- sum + i
print sum
```
##### 1. 합계를 0으로 시작한다
##### 2. i를 1부터 10까지 하나식 늘려가며, 매번 합게에 i를 더한다.
##### 3. 반복이 끝나면 합계를 출력한다. (결과는 55)

## flow chart (순서도)
###### 타원형 : 시작과 끝
###### 마름모 : 판단
###### 사디리꼴, 아치형 : 출력

## 버블 소트
#### 이웃한 두 원소를 비교해가며 큰 값을 오른쪽 끝으로 떠올리는 (bubble up) 가장 기초적인 정렬 알고리즘
###### 1. 배열의 처음부터 끝까지 이웃한 쌍을 비교
###### 2. 왼쪽 값이 더 크면 두 값을 **교환**
###### 3. 한 바퀴(패스)가 끝나면 **가장 큰 값이 맨 끝**에 자리
###### 4. 끝에 확정된 부분을 제외하고 **남은 구간에 대해 반복**
###### 5. 어떤 패스에서 **교환이 한 번도 없으면** 이미 정렬된 것이므로 **조기 종료**
```c
#include <stdio.h>

// 버블 정렬 함수 정의
void bubble_sort(int a[], int n) {
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

    bubble_sort(a, n);

    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
    printf("\n");

    return 0;
}
```

## 퀵 쇼트
##### 1. 배열에서 기준점(pivot)을 하나 선택
##### 2. 기준보다 작은 값은 왼쪽, 큰 값들을 오른쪽으로 분할
##### 3. 양쪽 부분 배열에 대해 같은 작업(재귀)를 반복

##### 교수님의 코드
```c
#include <stdio.h>

void swap(int *a, int *b) {
    int t = *a; *a = *b; *b = t;
}

int partition(int arr[], int left, int right) {
    int pivot = arr[right];      // 피벗: 맨 오른쪽 원소
    int i = left - 1;
    for (int j = left; j < right; j++) {
        if (arr[j] <= pivot) {
            swap(&arr[++i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[right]);
    return i + 1;
}

void quicksort(int arr[], int left, int right) {
    if (left >= right) return;
    int p = partition(arr, left, right);
    quicksort(arr, left, p - 1);
    quicksort(arr, p + 1, right);
}

int main(void) {
    int arr[] = {5, 3, 8, 4, 2, 7, 1, 10, 6, 9};
    int n = sizeof(arr) / sizeof(arr[0]);

    quicksort(arr, 0, n - 1);

    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

##### 진행과정을 상세히 보여주는 퀵소트 예시 코드
```c
#include <stdio.h>

// 배열 상태를 출력하는 함수
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// 두 값을 교환하는 함수
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// 분할(Partition) 함수
int partition(int arr[], int low, int high, int n) {
    int pivot = arr[high];  // 마지막 원소를 피벗으로 선택
    int i = low - 1;        // i는 작은 원소들의 마지막 인덱스

    printf("\n[Partition 시작] low=%d, high=%d, pivot=%d\n", low, high, pivot);
    printf("초기 배열 상태: ");
    printArray(arr, n);

    for (int j = low; j < high; j++) {
        // 현재 요소가 pivot보다 작으면 왼쪽 영역으로 이동
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
            printf("  → arr[%d](%d)와 arr[%d](%d) 교환: ", i, arr[i], j, arr[j]);
            printArray(arr, n);
        }
    }

    // pivot을 올바른 위치로 이동
    swap(&arr[i + 1], &arr[high]);
    printf("  → pivot(%d)을 arr[%d] 위치로 이동: ", pivot, i + 1);
    printArray(arr, n);

    printf("[Partition 종료] pivot 최종 위치: %d\n", i + 1);
    printf("-----------------------------------------\n");

    return (i + 1); // 피벗의 최종 위치 반환
}

// 퀵 정렬(Quick Sort) 함수
void quick_sort(int arr[], int low, int high, int n, int depth) {
    if (low < high) {
        // 깊이에 따라 들여쓰기 출력 (시각적 구분용)
        for (int k = 0; k < depth; k++) printf("  ");
        printf("퀵 정렬 호출: low=%d, high=%d\n", low, high);

        int pi = partition(arr, low, high, n); // 피벗 정렬

        // 왼쪽 부분 배열 정렬
        quick_sort(arr, low, pi - 1, n, depth + 1);

        // 오른쪽 부분 배열 정렬
        quick_sort(arr, pi + 1, high, n, depth + 1);
    }
}

int main() {
    int arr[] = { 5, 3, 8, 4, 2, 7, 1, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("초기 배열: ");
    printArray(arr, n);
    printf("=========================================\n");

    quick_sort(arr, 0, n - 1, n, 0);

    printf("\n정렬 완료!\n최종 결과: ");
    printArray(arr, n);
    return 0;
}
```
