## 포인터에 대한 복습
### swap 함수 구현 (포인터의 활용 / 보낼때 주소, 받을 때 포인터)
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
### 동적 정수 메모리 100개를 heap 영역에 값 1부터 100까지를 넣고, 출력하는 c코드를 작성하시오.
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
