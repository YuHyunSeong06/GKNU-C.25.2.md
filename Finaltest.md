# 기말고사 준비
###### 자료구조 5가지
###### 스택(LIFO), 리스트, 큐(FIFO), 이진 트리, 해시(hash)
###### 알고리즘 5가지
###### 퀵소트 구현
###### 연결리스트 구현

### 1. Visual Studio 환경에서 두 함수 add.c sub.c를 my.lib로 만들고 main.c에서 호출할 때 사용하는 명령을 차례대로 적으시오.
```
notepad add.c
(코드 작성)
notepad sub.c
(코드 작성)
notepad main.c
(코드 작성)
cl /c add.c // cl /c는  "Compile only, do not link"
cl /c sub.c
cl /c main.c
lib /OUT:my.lib add.obj sub.obj
cl main.c my.lib
main.exe
```
### 2.wsl에서 두 함수 add.c sub.c를 main.c에서 호출하는 프로젝트의 make문을 작성하시오.
```
main: main.o add.o sub.o
	gcc -o main main.o add.o sub.o

main.o: main.c
	gcc -c main.c

add.o: add.c
	gcc -c add.c

sub.o: sub.c
	gcc -c sub.c
```

### 3.C언어의 대표적인 자료구조 5가지
```
리스트 스택 큐 트리 해시
```

### 4.메모리에 두 수를 저장하고 그 중에 작은 수를 출력하는 "슈도 코드를 작성하시오."
```
a ← 7
b ← 3
IF a ≤ b THEN
    PRINT a
ELSE
    PRINT b
END IF
```

### 5.메모리에 두 수를 저장하고 그 중에 작은 수를 찾는 플로우 차트를 그리시오.
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/b531c9c0-5b09-48b9-97ac-3f9060d03920" />

### 6.1부터 50까지 중에 5의 배수를 출력하는 코드를 작성하시오
```c
#include <stdio.h>

int main(void) {
	for(int i=1;i<51;i++){
		if(i%5==0){
			printf("%d ",i);
		}
	}
}
```
