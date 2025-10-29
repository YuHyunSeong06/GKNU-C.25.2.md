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
## 구조체의 이해

##### 미션1: 2명 학생 학번, 이름 및 3과목(Kor, Math, Eng) 성적을 구조체로 초기화 하고, my.txt에 저장하시오.
```c
#include <stdio.h>

typedef struct {
    int id;           // 학번
    char name[32];    // 이름
    int kor, math, eng; // 국어, 수학, 영어
} Student;

int main(void) {
    Student s[2] = {
        {20251234, "Kim", 95, 88, 91},
        {20251235, "Lee", 82, 90, 86}
    };

    FILE *fp = fopen("my.txt", "w");
    if (!fp) {
        perror("my.txt open failed");
        return 1;
    }

    // CSV 형식: ID,Name,Kor,Math,Eng
    fprintf(fp, "ID,Name,Kor,Math,Eng\n");
    for (int i = 0; i < 2; ++i) {
        fprintf(fp, "%d,%s,%d,%d,%d\n",
                s[i].id, s[i].name, s[i].kor, s[i].math, s[i].eng);
    }

    fclose(fp);
    return 0;
}
```
```
ID,Name,Kor,Math,Eng
20251234,Kim,95,88,91
20251235,Lee,82,90,86
```
##### 미션2: my.txt 데이터를 읽고 개인별 평균을 화면에 출력하시오.
```C
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("my.txt", "r");
    if (!fp) {
        perror("my.txt open failed");
        return 1;
    }

    char line[256];
    // 헤더 한 줄 건너뛰기
    if (!fgets(line, sizeof(line), fp)) {
        fprintf(stderr, "파일이 비어 있습니다.\n");
        fclose(fp);
        return 1;
    }

    // 데이터 읽기
    while (fgets(line, sizeof(line), fp)) {
        int id, kor, math, eng;
        char name[64];

        // CSV 파싱: ID,Name,Kor,Math,Eng
        if (sscanf(line, "%d,%63[^,],%d,%d,%d", &id, name, &kor, &math, &eng) == 5) {
            double avg = (kor + math + eng) / 3.0;
            printf("ID:%d  이름:%s  평균: %.2f\n", id, name, avg);
        }
        // 형식이 맞지 않는 줄은 자동 건너뜀
    }

    fclose(fp);
    return 0;
}
```
```
ID:20251234  이름:Kim  평균: 91.33
ID:20251235  이름:Lee  평균: 86.00
```
##### my.txt로 부터 읽고, 다음과 같은 형식의 오른쪽 끝에는 개인 평균, 아래쪽에는 과목 평균을 나타내시오. 
```
ID,Name,Kor,Math,Eng
20251234,Kim,95,88,91
20251235,Lee,82,90,86
```
