## C언어 데이터형
##### 1. char -128 ~ 0 ~ 127 / 256개를 나타냄
##### 2. int
##### 3. float
##### 4. double
##### 5. unsigned int
##### 6. unsigned char 0 ~ 255 // 256개
##### 7. long int
##### 8. short int
##### 8. unsigned long int
##### sizeof(char);
##### sizeof(unsigned long int)
__________________________________________
### 배열 int v[60];
### 구조체 
```c
struct USER{
  int age;
  char name[20];
};
```
### 공용체(union) : 자료형이 달라도 값이 메모리를 공유한다.
```c
union DATA{
  char a;
  int i;
  double d;
};
```
###### https://cafe.naver.com/jclang?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30916880%2526articleid%3D359%2526referrerAllArticles%3Dtrue
참고
