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
### 2.
