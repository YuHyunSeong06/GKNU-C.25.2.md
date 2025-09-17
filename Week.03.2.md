## 프로그래밍 심화
###### 25.09.17 첫번째 수업

##### 함수의 프로토타입을 통해 선언하고 두 수를 더하기
```c
#include <stdio.h>

int add(int, int);
void main() {
	int a, b;
	a = 11, b = 22;
	printf("%d\n", add(a, b));
}

int add(int a, int b) {
	int t;
	t = a + b;
	return t;
}
```
##### 1부터 100까지 짝수의 합
```c
#include <stdio.h>

int main() {
	int sum = 0;
	for (int i = 0;i <= 100;i++) {
		if (i % 2 == 0) {
			sum = sum + i;
			// sum+=i;
		}
	}
	printf("%d\n", sum);
}
```

##### 1부터 100까지 홀수의 합
```c
#include <stdio.h>

int main() {
	int sum = 0;
	for (int i = 1;i <= 100;i+=2) {
		sum+=i;
	}
	printf("%d\n", sum);
}
```
