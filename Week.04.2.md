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



