#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <malloc.h>

typedef struct node
{
    int num;
    struct node * pNext;
} NODE,*PNODE;

typedef struct team
{
    PNODE front;
    PNODE rear;
} TEAM,* PTEAM;


void init(PTEAM pt);
void insert(PTEAM pt);
void put(PTEAM pt);
void traverse(PTEAM pt);



int main (void)
{
    TEAM t;
    init(&t);
    insert(&t);
    traverse(&t);
    put(&t);
    traverse(&t);


    return 0;
}

void init(PTEAM pt)
{
    PNODE pNew = (PNODE)malloc(sizeof(NODE));
    if(pNew == NULL)
    {
        printf("内存不足，分配失败！");

        exit(-1);
    }
    pt->front = pNew;
    pt->rear = pNew;
    pNew->pNext = NULL;
    return;
}


void insert(PTEAM pt)
{
    int i, n, val;
    printf("请输入你要加入队列元素的个数：");
    scanf("%d",&n);
    PNODE p = pt->front;

    for(i = 0; i<n; ++i)
    {
        printf("请输入第%d个元素的数字：",i+1);
        scanf("%d",&val);
        PNODE pNew = (PNODE)malloc(sizeof(NODE));
        if(pNew == NULL)
        {
            printf("内存不足，分配失败！");
            exit(-1);
        }
        p->pNext = pNew;
        pNew->num = val;
        pNew->pNext = NULL;
        pt->rear = pNew;
        p = p->pNext;
    }
    pt->front = pt->front->pNext;


    return;
}


void put(PTEAM pt)
{
    int i = 0, n;
    printf("请输入要删除元素的个数：");
    scanf("%d",&n);
    PNODE p = pt->front;
    if(p == NULL)
    {
        printf("队列个数为零，不能删除！");
        return;
    }
    for(i = 0; i<n&&p != NULL; ++i)
    {
        PNODE q = p;
        p = p->pNext;
        pt->front = p;
        free(q);
        q = NULL;
    }

    return;
}


void traverse(PTEAM pt)
{
    PNODE p = pt->front;
    while(p != NULL)
    {
        printf("%d ",p->num);
        p = p->pNext;
    }
    printf("\n");
    return;
}
