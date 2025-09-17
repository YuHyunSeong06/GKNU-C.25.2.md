## 프로그래밍 심화
###### 25.09.17 첫번째 수업

#### 함수의 프로토타입을 통해 선언하고 두 수를 더하기
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
#### 1부터 100까지 짝수의 합
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

#### 1부터 100까지 홀수의 합
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
#### 구조체를 이용한 세 수의합
```c
#include <stdio.h>

typedef struct Math {
	int a, b, c;
}M;

int add(M m) {
	return m.a + m.b + m.c;
}

void main() {
	M m = { 1,2,3 };
	printf("%d\n", add(m));
	printf("KIM DDILBBANG BABO");
}
```
#### 중간고사 예상 문제
```c
#include <stdio.h>

typedef struct Math {
	int a, b, c;
}M;

int add(M* m) {
	return m->a + m->b + m->c; // 함수에서 매개변수로 포인터를 보내면 주소로 받는다
}

void main() {
	M me = { 1,2,3 };
	printf("%d\n", add(&me));
}
```
#### 나이를 입력받아 판정하기
```c
#include <stdio.h>

void main() {
	int age;

	while (1) {
		printf("Enter your Age (0 to quit) : ");
		scanf("%d", &age);

		if (age == 0)
			break;

		else if (age >= 18 && age < 60)
			printf("Adult\n");

		else if (age >= 60)
			printf("we can do it\n");

		else if (age <= 18)
			printf("Youth\n");
	}
	
}
```
###### 25.09.17 두번째수업
#### 성적을 입력받아 판정하기-if문
```c
#include <stdio.h>

void main() {
	int s;
	char p;
	for (;;) {
		puts("Score?");
		scanf("%d", &s);
		if (s >= 90) 
			p = 'a';
		else if (s >= 70) 
			p = 'b';
		else if (s >= 50) 
			p = 'c';
		else if (s >= 20) 
			p = 'd';
		else 
			p = 'f';

		printf("%c\n", toupper(p)); // touppper 소문자를 대문자로 tolower 대문자를 소문자로
	}
}
```
#### 성적을 입력받아 판정하기-case문
```c
#include <stdio.h>

void main() {
	int s;

	char p;

	for (;;) {
		puts("Score?");
		scanf("%d", &s);

		switch (s / 10) {
		case 10:
		case 9:
			p = 'a';
			break;
		case 8:
		case 7:
			p = 'b';
			break;
		case 6:
		case 5:
		case 4:
			p = 'c';
			break;
		default: p = 'F';
		}
		printf("%c\n", toupper(p)); // touppper 소문자를 대문자로 tolower 대문자를 소문자로
	}
}
```
#### 재귀함수의 기초형
```c
#include <stdio.h>

int add(int a) {
	if (a > 1) return a + add(a - 1);
}
void main() {
	printf("%d\n", add(3));
}
```
