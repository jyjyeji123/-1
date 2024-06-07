### 스택 구현 ###
```
#include<stdio.h>
#include<stdlib.h> //동적 메모리 할당 및 유틸리티 함수를 사용하기 위해 포함

#define MAX 100 //스택의 최대 크기를 100으로 정의

//스택 구조체의 정의

typedef struct { //새로운 구조체 타입을 정의
    int top; // 스택의 가장 상단 요소의 인덱스를 저장
    int items[MAX]; //스택 요소들을 저장할 배열
} Stack;

//스택 초기화

void initStack(Stack *s) { //스택을 초기화하는 함수
    s->top = -1; //스택이 비어있음을 나타내기 위해 top을 -1로 설정
}

//스택이 비어있는지 확인

int isEmpty(Stack *s) { //스택이 비었는지 확인하는 함수
    return s->top == -1; //top이 -1이면 스택이 비어있음을 의미
}

//스택이 비어있는지 확인

int isFull(Stack *s) { //스택이 비었는지 확인하는 함수
    return s->top == MAX - 1; //top이 -1이면 스택이 비어있음을 의미
}

//스택에 요소를 추가

void push(Stack *s, int item) { //스택에 요소를 추가하는 함수
    if(isFull(s)) { //스택이 가득 찼는지 확인
        printf("Stack is full\n");
    } else {
        s->items[++s->top] = item; //top을 증가시키고 새로운 요소를 추가
    }
}

//스택에서 요소를 제거

int pop(Stack *s) { //스택에서 요소를 제거하는 함수
    if(isEmpty(s)) { //스택이 비었는지 확인
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top--]; //현재 top 요소를 반환하고 top을 감소
    }
}

//스택의 최상단 요소를 확인

int peek(Stack *s) { //스택의 최상단 요소를 확인하는 함수
    if(isEmpty(s)) { //스택이 비었는지 확인
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top]; //현재 top 요소를 반환
    }
}

```

### 큐 구현 ###
```
#include<stdio.h>
#include<stdlib.h>

#define MAX 100

//큐 구조체 정의

typedef struct { //새로운 구조체 타입을 정의.
    int items[MAX]; //큐 요소들을 저장할 배열.
    int front; //큐의 첫 번째 요소의 인덱스를 저장.
    int rear; //큐의 마지막 요소의 인덱스를 저장.
} Queue;

//큐 초기화

void initQueue(Queue *q) { //큐를 초기화하는 함수.
    q->front = -1; //큐가 비어있음을 나타내기 위해 front를 -1로 설정.
    q->rear = -1; //큐가 비어있음을 나타내기 위해 rear를 -1로 설정.
}

//큐가 비었는지 확인

int isEmpty(Queue *q) { //큐가 비었는지 확인하는 함수.
    return q->rear == q->front; //front가 -1이면 큐가 비어있음을 의미.
}

//큐가 가득 찼는지 확인

int isFull(Queue *q) { //큐가 가득 찼는지 확인하는 함수.
    return q->rear == MAX - 1; //rear가 MAX - 1이면 큐가 가득 찼음을 의미.
}

//큐에 요소를 추가

void enqueue(Queue *q, int item) { //큐에 요소를 추가하는 함수.
    if(isFull(q)) { //큐가 가득 찼는지 확인.
        printf("Queue is full\n");
    } else {
        if (q->front == -1) //큐가 비어있으면 front를 0으로 설정.
            q->front = 0;
        q->items[++q->rear] = item; //rear를 증가시키고 새로운 요소를 추가.
    }
}

//큐에서 요소를 제거

int dequeue(Queue *q) { //큐에서 요소를 제거하는 함수.
    if (isEmpty(q)) { //큐가 비었는지 확인.
        printf("Queue is empty\n");
        return -1; // 오류 값을 반환
    } else {
        int item = q->items[q->front]; //front의 요소를 저장.
        if (q->front >= q->rear) { //큐가 비어있는지 확인.
            q->front = -1; //큐가 비어있으면 front와 rear를 -1로 설정.
            q->rear = -1; //제거된 요소를 반환.
        } else {
            q->front++; //// front를 증가시켜 다음 요소를 가리킴.
        }
        return item;
    }
//큐의 첫 번째 요소를 확인

}
int peek(Queue *q) { //큐의 첫 번째 요소를 확인하는 함수
    if (isEmpty(q)) { //큐가 비었는지 확인.
        printf("Queue is empty\n");
        return -1; // 오류 값을 반환
    } else {
        return q->items[q->front]; //front의 요소를 반환.
    }
}
```

### 동적배열 구현 ###
```
#include<stdio.h>
#include<stdlib.h>

//벡터 구조체 정의

typedef struct { //새로운 구조체 타입을 정의.
    int *items; //벡터 요소들을 저장할 동적 배열.
    int size; //현재 벡터의 크기.
    int capacity; //벡터의 총 용량.
} Vector;

//벡터 초기화

void initVector(Vector *v) { //벡터를 초기화하는 함수.
    v->capacity = 4; //초기 용량을 4로 설정.
    v->size = 0; //현재 크기를 0으로 설정.
    v->items = (int*)malloc(sizeof(int) * v->capacity); //초기 용량만큼 메모리 할당.
}

//벡터 크기 조정

void resize(Vector *v, int capacity) { //벡터의 크기를 조정하는 함수.
    int *items = (int*)realloc(v->items, sizeof(int) * capacity); //새로운 용량만큼 메모리 재할당.
    if (items) { //메모리 재할당이 성공했는지 확인.
        v->items = items; //새로운 메모리 주소를 벡터에 저장.
        v->capacity = capacity; //벡터의 용량을 업데이트.
    }
}

//벡터에 요소 추가

void add(Vector *v, int item) { //벡터에 요소를 추가하는 함수.
    if (v->size == v->capacity) { //벡터가 가득 찼는지 확인.
        resize(v, v->capacity * 2); // 용량이 부족할 경우 2배로 증가
    }
    v->items[v->size++] = item; //요소를 추가하고 크기를 증가.
}

//delete : 주어진 인덱스의 요소를 삭제

void delete(Vector *v, int index) {
    if (index < 0 || index >= v->size) return; //index < 0: 인덱스가 0보다 작으면 유효하지 않습니다, index >= v->size: 인덱스가 벡터의 현재 크기보다 크거나 같으면 유효하지 않습니다 = 인덱스가 유효하지 않은 경우 함수는 아무 작업도 하지 않고 종료합니다.
    for (int i = index; i < v->size - 1; i++) { // 루프는 삭제할 인덱스 이후의 모든 요소를 한 칸씩 앞으로 이동시킵니다.
        v->items[i] = v->items[i + 1]; //현재 위치의 요소를 다음 위치의 요소로 덮어씁니다.
    }
    v->size--; //요소를 삭제했으므로 벡터의 크기를 1 감소시킵니다.
    if (v->size > 0 && v->size == v->capacity / 4) { //v->size > 0: 벡터가 비어 있지 않은지 확인합니다, v->size == v->capacity / 4: 벡터의 크기가 용량의 1/4인 경우 용량을 절반으로 줄입니다.
        resize(v, v->capacity / 2); //벡터의 용량을 절반으로 줄이는 함수입니다.
    }
}

//get : 벡터에서 주어진 인덱스의 요소를 반환

int get(Vector *v, int index) {
    if (index < 0 || index >= v->size) { //index < 0: 인덱스가 0보다 작으면 유효하지 않습니다, index >= v->size: 인덱스가 벡터의 현재 크기보다 크거나 같으면 유효하지 않습니다.
        printf("Index out of bounds\n");
        return -1; //인덱스가 유효하지 않으면 "Index out of bounds" 메시지를 출력하고 -1을 반환합니다.
    }
    return v->items[index]; //유효한 인덱스인 경우 해당 인덱스의 요소를 반환
}
```

