## 배열
###### 25.09.24 첫번째 수업
##### 배열의 기초
```c
#include <stdio.h>

void main() {
	int v[5] = { 5,4,3,2,1 }; // v[0]=5
	printf("%d\n", v[3]);
	v[3] == 33;
	printf("%d\n", v[3]);
}
```
```c
#include <stdio.h>

void main() {
	int v[5] = { 5,4,3,2,1 }; // v[0]=5

	int* p;
	p = v; // &v 로 할시 이상해진 값이 된다
	// p = &v[0]; = p = &v; 특별할 지정안할시 포인터는 항상 0의 인덱스 값을 나타낸다

	printf("%d\n", v[3]);
	// v[3] == 33;
	// printf("%d\n", v[3]);
}
```
##### 포인터의 기초
```c
#include <stdio.h>

void main() {
	int a = 3;
	int* p;
	p = &a;

	printf("%d\n", *p);
}
```
```c
#include <stdio.h>

void main() {
	int a = 33;
	int* p;
	p = &a;
	printf("%d\n", *p);
}
```
##### 포인터와 배열의 활용
```c
#include <stdio.h>

void main() {
	int a[5] = { 1,2,3,4,5, };
	int* p;
	p = a;

	printf("%d\n", *(p + 4));
	printf("%d\n", a[4]);
}
```
##### 배열의 응용
```c
#include <stdio.h>

void main() {
	int a[5] = { 11,22,33,44,55, };
	int* p;
	p = a;

	for (int i = 0;i < 5;i++) {
		printf("%d\n", *p);
		p++;
	}
}
```

##### 이차원 배열의 이해
```c
#include <stdio.h>

void main() {
	int a[3][3] = { {1,2,3},{4,5,6},{7,8,9} };

	int sum = 0;
	for (int i = 0; i < 3;i++) {
		for (int j = 0;j < 3;j++) {
			sum = sum + a[i][j];
			printf("%d ", a[i][j]);
		}
		printf("\n");
	}
	printf("%d\n", sum);
}
```
## 그래픽스와 이차원 배열의 응용
###### 25.09.24 두번째 수업
##### 동적메모리 malloc 활용
```c
#include <stdio.h>
#include <stdlib.h>

void main() {
	int* p;
	p = (int*)malloc(sizeof(int) * 2); // 동적메모리, 힙영역
	// sizeof byte 수를 나타내주는 연산자
	if (!p) {
		perror("malloc");
		return 1;
	}

	*(p+0) = 11;
	*(p+1) = 22;

	printf("%d %d\n", p[0], p[1]);
	free(p);
}
```
##### 그래픽스를 통한 초록색 원 그리기
```c
#include "raylib.h"

int main(void) {
	InitWindow(800, 600, "GKNU");
	while (!WindowShouldClose()) {
		BeginDrawing();
		ClearBackground(BLACK);
		DrawCircle(400, 300, 150, GREEN);
		EndDrawing();
	}
	CloseWindow();
}
```

