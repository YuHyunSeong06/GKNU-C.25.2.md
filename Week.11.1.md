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
1.
도구 -> 명령행 -> 명령자 개발 프롬포트

cl/c *.c
lib /OUT:my.lib add.obj sub.obj
link main my.lib

2.                      
main: main.o add.o sub.o
        gcc -o main main.o add.o sub.o
main.o: main.c
        gdd -c main.c
add.o: add.c
        gcc -c add.c
sub.o: sub.c
        gcc -c sub.c

3. 
리스트, 스택, 큐, 배열, 구조체

4. 
a <- 7
b <- 3
IF a <= b THEN
  PRINT a
ELSE
  PRINT b
END IF

5. 플로우차트

6.
#include <stdio.h>

int main(void) {
    int i;
    for (i = 5; i <= 50; i += 5) {
        printf("%d\n", i);
    }
}

7. 

#include <stdio.h>
void main(int argc, char* argv[]) {
   int a = atoi(argv[1]);
   char ch = argv[2][0];
   int b = atoi(argv[3]);
   int r;

   switch (ch) {
   case '+': r = a + b; break;
   case '*': r = a * b; break;
   default: break;
   }
   printf("%d\n", r);
}

8.
#include <stdio.h>
void q(int* a, int l, int r) {
   if (l >= r)return;
   int p = a[r], i = l - 1, t;
   for(int j=l;j<r;j++)
      if (a[j] <= p) { t = a[++i]; a[i] = a[j]; a[j] = t; }

   t = a[i + 1]; a[i + 1] = a[r]; a[r] = t;
   q(a, l, i); q(a, i + 2, r);
}

int main(void) {
   int a[] = { 2,1,3,4,5 };
   q(a, 0, 4);
   for (int i = 0;i < 5;i++) printf("%d ", a[i]);
}


9. 버블쇼팅
#include <stdio.h>
void bubble(int a[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - 1 - i; j++)
            if (a[j] > a[j + 1]) {
                int t = a[j]; a[j] = a[j + 1]; a[j + 1] = t;
            }
}
int main(void) {
    int a[] = { 5, 1, 4, 2, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    bubble_sort(a, n);

    for (int i = 0; i < n; i++) printf("%d ", a[i]);
    printf("\n");
    return 0;
}

10.
typedef enum (둘 다 같음)
typedef struct (서로 다른 두개를 하나의 타입으로)
union (서로 다른 두개)
