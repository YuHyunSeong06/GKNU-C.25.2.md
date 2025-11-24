## 포인터에 대한 복습 필요
### 1. swap 함수 구현 (포인터의 활용 / 보낼때 주소, 받을 때 포인터)
```c
#include <stdio.h>

void swap(int* a, int* b) {
	int t = *a;
	*a = *b;
	*b = t;
}

int main() {
	int a = 2, b = 3;
	swap(&a, &b);
	printf("%d %d", a, b);
	
}
```
### 2. 동적 정수 메모리 100개를 heap 영역에 값 1부터 100까지를 넣고, 출력하는 c코드를 작성하시오.
```c
#include <stdio.h>
#include <stdlib.h>   // malloc, free 사용 위해 필요

int main() {
    int n = 100;

    // 동적 메모리 할당 (int 100개)
    int* arr = malloc(n * sizeof(int));
    if (arr == NULL) {    // malloc 실패 시 체크
        printf("메모리 할당 실패\n");
        return 1;
    }

    // 값 1~100 저장
    for (int i = 0; i < n; i++) {
        arr[i] = i + 1;
    }

    // 출력
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    // 메모리 해제
    free(arr);

    return 0;
}

```
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int* buf;
	buf = (int*)malloc(sizeof(int*) * 100);
	for (int i = 0;i < 100;i++) {
		buf[i] = i + 1;
	}
	for (int i = 0;i < 100;i++) {
		printf("%d ", buf[i]);
	}
}
```
### 3. 이진 바이너리 구조체를 typedef로 정의하시오.
### 4. 동전을 1000번 던질 때 앞면 과 뒷면이 나올 회수를 시뮬레이션하는 코드를 작성하시오.
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void main() {
	int h[2] = { 0 };
	srand(time(NULL));
	for (int i = 0; i < 1000;i++) {
		int n = rand();
		n = n % 2;
		h[n] = h[n] + 1;
	}
	for (int j = 0;j < 2;j++) {
		printf("[%d]=%d\n", j + 1, h[j]);
	}
}
```
