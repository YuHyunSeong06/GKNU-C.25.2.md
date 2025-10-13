## WSL 환경에서 C언어를 컴파일하기

##### WSL 환경에서 첫번째로 해야할것
```wsl
ubuntu
~$ sudo apt-get update
~$ sudo apt-get update -y
```
##### 
```Linux
mkdir anu
cd anu
nano main.c
```
```Linux
ls
./a.out
gcc -o main main.c
./ main
```
```c
#include <stdio.h>
int add(int, int)
void main(){
  int a=22, b=33;
  printf("%d\n",add(a,b));
}
```
```
nano add.c
gcc -c *.c
gcc -o main main.o add.o
./main
```
```
nano makefile
```
```
  GNU nano 7.2                                            makefile *                                                    CC = gcc
all: test

test: main.o add.o
        $(CC) -o test main.o add.o
main.o: main.c
        $(CC) -c main.c
add.o: add.c
        $(CC) -c add.c
clean:
        rm -rf *.o
```
##### 명령줄 프롬포트를 통한 코딩
```
cl/c *.c
lib /OUT:my.lib add.obj
link main my.lib
```
## 주사위를 굴려 각 눈의 경우의 수
```c
// 프로토타입
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void main() {
	int h[6] = { 0 };
	srand(time(NULL));
	for (int i = 0; i < 60;i++) {
		int n = rand();
		n = n % 6;
		h[n] = h[n] + 1;
	}
	for (int j = 0;j < 6;j++) {
		printf("[%d]=%d\n", j+1,h[j]);
	}
}
```
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int h[6]; // 글로벌 초기화
void main() {
	srand(time(NULL));
	for (int i = 0; i < 60;i++) {
		h[rand() % 6]++;
	}
	for (int j = 0;j < 6;j++) {
		printf("[%d]=%d\n", j + 1, h[j]);
	}
}
```
