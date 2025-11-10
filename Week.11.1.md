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
c:\>main 22 + 33
argv[0] : c:\>main
argv[1]: 22
argv[2]: +
argv[3]: 33
```c
#include <stdio.h>

void main(int argc, char* argv[]) {
	int a = atoi(argv[1]);
	char o = argv[2][0];
	int b = atoi(argv[3]);
}
```
