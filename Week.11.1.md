# WSL
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
clean:
        rm -rf *.o
        rm ./main
```
