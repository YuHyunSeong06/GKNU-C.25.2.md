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
