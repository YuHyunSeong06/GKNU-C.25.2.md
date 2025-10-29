## 명령프롬포트를 활용하여 코딩
##### cd \(경로 이동) -> mkdir anu -> cd anu -> notepad add.c
```c
// add.c로 모든 파일로 저장
int add(int a, int b){
  return a + b;
}
```
```c
// sub.c로 모든 파일로 저장
int sub(int a, int b){
  return a - b;
}
```
```c
// mul.c로 모든 파일로 저장
int mul(int a, int b){
  return a * b;
}
```
```c
// idv.c 모든 파일로 저장
int div(int a, int b){
  return a / b;
}
```
```c
#include <stdio.h>

int add(int, int);
int sub(int, int);
int mul(int, int);
int div(int, int);

void main(int argc, char* argv[]){
	int a,b;

	a=atoi(argv[1]);
	b=atoi(argv[2]);

	printf("%d\n",add(a,b));
	printf("%d\n",sub(a,b));
	printf("%d\n",mul(a,b));
	printf("%d\n",div(a,b));
}
```
##### cl /c *.c (모든 C파일 컴파일)
##### lib /OUT:math.lib add.obj sub.obj mul.obj div.obj (각각의 파일들을 math의 라이브러리에 포함)
##### cl 

## enum
##### 신호기를 enum을 사용해서 숫자를 문자로 출력
```c
#include <stdio.h>

// typedef 없이 enum 정의
enum TL { RED, YELLOW, GREEN };

int main(void) {
    // enum 키워드로 변수 선언
    enum TL light = RED;

    switch (light) {
        case RED:
		    printf("멈춤!\n");
			break;
        case YELLOW:
			printf("주의!\n");
			break;
        case GREEN:
  			printf("출발!\n");
			break;
		default:
			printf("오류\n");
			break;
    }
    return 0;
}
```
##### 응용
```c
#include <stdio.h>

// typedef 없이 enum 정의
typedef enum { 
    RED, 
    YELLOW, 
    GREEN 
}TL;

int main(void) {
    // enum 키워드로 변수 선언
    TL light = GREEN;
    printf("%d\n", GREEN);
    switch (light) {
    case RED:
        printf("멈춤!\n");
		break;
    case YELLOW:
        printf("주의!\n");
		break;
    case GREEN:
        printf("출발!\n");
		break;
    default:
        printf("오류\n");
    }
    return 0;
}
```
## union
```c
#include <stdio.h>

union Number {
    int   i;
    float f;
};

int main(void) {
    union Number n;

    n.i = 42;                        // 같은 메모리를 int로 사용
    printf("int로 저장: i=%d, f=%f\n", n.i, n.f);

    n.f = 3.14f;                     // 같은 메모리를 float로 다시 사용(덮어씀)
    printf("float로 저장: f=%f, i=%d\n", n.f, n.i);

    printf("union 크기: %zu 바이트\n", sizeof(union Number));
    return 0;
}
```
