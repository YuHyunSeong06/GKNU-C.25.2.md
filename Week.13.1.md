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
```
