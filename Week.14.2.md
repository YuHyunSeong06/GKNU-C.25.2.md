## 함수의 총정리

```c
#include <stdio.h>

int add(int a, int b);		// 함수 선언(프로토타입)
int main(void) {
	int result = add(3, 5); // 함수 호출
	printf("결과: %d\n", result);
}
int add(int a, int b) {		// 함수 정의
	return a + b;			//반환
}
```
```c
#include <stdio.h>

int foo(int a);		// 함수 선언(프로토타입)
int main(void) {
	int a = 3;
	int result = foo(a); // 함수 호출
	printf("결과: %d\n", result);
}
int foo(int a) {		// 함수 정의
	a = 33;
	return a;			//반환
}
```
```c
#include <stdio.h>

void foo(int a);		// 함수 선언(프로토타입)
int a = 3;				// 전역 변수
int main(void) {
	int a = 3;
	foo(a); // 함수 호출
	printf("결과: %d\n", a);
}
void foo(int a) {		// 함수 정의
	a = 33;
	return a;			//반환
}
```
```c
#include <stdio.h>

void foo(int* a) {		// 함수 정의
	*a = 33;			//반환
}		// 전역 변수
int main(void) {
	int a = 3;
	foo(a); // 함수 호출
	printf("결과: %d\n", a);
}
```
