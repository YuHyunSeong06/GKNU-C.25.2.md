## 중앙 제곱법 - 난수 생성
```c
#include <stdio.h>
void main(void)
{
    int seed = 1234;  // 초기값 (0~9999)
    long x;
    for (int i = 0; i < 10; i++) {
        x = seed;
        x = x * x;          // 제곱
        x = (x / 100) % 10000; // 가운데 4자리
        seed = (int)x;
        printf("%04d\n", seed);
    }
}
```
## linked list
#### 
##### 3-> 2-> 1 을 저장하고 출력하기
```c
#include <stdio.h>

struct Node {
	int data;
	struct Node* next;
};

int main(void) {
	struct Node n1, n2, n3;
	struct Node* head;
	struct Node* p;

	n1.data = 3; n2.data = 2; n3.data = 1;
	n1.next = &n2; n2.next = &n3; n3.next = NULL;
	head = &n1;
	p = head;
	while (p != NULL) {
		printf("%d", p->data);
		if (p->next != NULL) {
			printf("->");
		}
		p = p->next;
	}
}
```
## raylib 활용
### 이미지 출력
```c
#include "raylib.h"
int main(void) {
	InitWindow(800, 600, "raylib");

	Texture2D t = LoadTexture("cat.png");
	SetTargetFPS(60);
	
	while (!WindowShouldClose()) {
		BeginDrawing();
		DrawTexture(t, 0.8, 0.6, WHITE);
		EndDrawing();
	}
	UnloadTexture(t);
	CloseWindow();
	return 0;
}
```
## tree
```c
#include <stdio.h>
#include <stdlib.h>

/* 이진 트리 노드 */
typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
} Node;

/* 새 노드 생성 */
static Node* make_node(int value) {
    Node* n = (Node*)malloc(sizeof(Node));
    if (!n) { perror("malloc"); exit(1); }
    n->data = value;
    n->left = NULL;   // 왼쪽 자식(없으면 NULL)
    n->right = NULL;  // 오른쪽 자식(없으면 NULL)
    return n;
}

/* 중위 순회: (왼) -> (자기) -> (오) */
void inorder(const Node* r) {
    if (!r) return;
    inorder(r->left);
    printf("%d ", r->data);
    inorder(r->right);
}

/* 전체 해제 */
void free_tree(Node* r) {
    if (!r) return;
    free_tree(r->left);
    free_tree(r->right);
    free(r);
}

int main(void) {
    /* 가장 단순한 트리: 3노드
           2
          / \
         1   3
       (NULL 잎 포함)
    */
    Node* root = make_node(2);              // 루트 2 (left=NULL, right=NULL)
    root->left  = make_node(1);             // 왼쪽 1  -> (left=NULL, right=NULL)
    root->right = make_node(3);             // 오른쪽 3 -> (left=NULL, right=NULL)

    printf("Inorder: ");
    inorder(root);                           // 1 2 3
    printf("-> NULL\n");

    free_tree(root);
    return 0;
}
```
