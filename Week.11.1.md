정렬: 리스트, 큐, 구조체, 트리, 스택
### WSLㅎ### WSLㅎ
```
main: main.o add.o sub.o
        gcc -o main main.o add.o sub.o
main.o: main.c
        gcc -c main.c
add.o: add.c
        gcc -c add.c
sub.o: sub.c
        gcc -c sub.c
run:
        ./main
```
### 명령행에서 곱셈과 덧셈
```c
#include <stdio.h>

void main(int argc, char* argv[]) {
	int a = atoi(argv[1]);
	char o = argv[2][0];
	int b = atoi(argv[3]);
	int r;

	switch (ch) {
	case'+':r = a + b;
		break;
	case'*':r = a * b;
		break;
	default:
		break;
	}
	printf("%d\n", r);
}
```
c:\>main 21 + 34
argv[0] : c:\>main
argv[1]: 21
argv[2]: +
argv[3]: 34
argv[1][0]=2
argv[1][1]=1
argv[1][2]='\0'=NULL
argv[2][0]=+

### 퀵소트
```c
#include <stdio.h>

void q(int* a, int l, int r) {
	if (l >= r)
		return;
	int p = a[r], i = l - 1, t;
	for(int j=l;j<r;j++)
		if (a[j] <= p) {
			t = a[++i];
			a[i] = a[j];
			a[j] = t;
		}
	t = a[i + 1];
	a[i + 1] = a[r];
	a[r] = t;
	q(a, l, i);
	q(a, i + 2, r);
}
int main(void) {
	int a[] = { 2,1,5,3,4 };
	q(a, 0, 4);
	for (int i = 0;i < 5;i++) {
		printf("%d ", a[i]);
	}
	return 0;
```
