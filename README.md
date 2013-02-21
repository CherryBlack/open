open
====
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

typedef struct Node
{
    int data;
    struct Node* next;
}Node;
typedef struct Node* LinkList;
LinkList L;

//清空链表
void ClearList(LinkList L;)
{
    LinkList p,q;
    p=L->next;
    while(p)
    {
        q=p->next;
        free(p);
        p=q;
    }
    L->next=NULL;
}

//头插法建立单链表示例
void CreateListHead(int n)
{
    LinkList p;
    int i;
    srand(time(0));//初始化随机数种子LinkList L;
    ClearList();//清空链表，使每次“头插法”从表头开始
    for(i=0;i<n;i++)
    {
        p=(LinkList)malloc(sizeof(Node));//生成新节点
        p->data=rand()%100+1;//(1~100内的随机数)
        p->next=L->next;
        L->next=p;
    }
}

//插入数据
int InsertList(int i,int e)
{
    int j=1;
    LinkList p,s;
    p=L;
    while(p->next&&j<i)
    {
        p=p->next;
        j++;
    }
    if(!(p->next)||j>i)
    {
        printf("当前位置不存在，插入失败......\n\n");
        return 0;
    }
    else
    {
        s=(LinkList)malloc(sizeof(Node));
        s->data=e;
        s->next=p->next;
        p->next=s;
        printf("插入成功......\n\n");
        return 1;
    }
}

//删除数据
int DeleteList(int i)
{
    int j=1;
    LinkList p,q;
    p=L;
    while(p->next&&j<i)
    {
        p=p->next;
        ++j;
    }
    if(!(p->next)||j>i)
    {
        printf("当前位置不存在，删除失败......\n\n");
        return 0;
    }
    else
    {
        q=p->next;
        p->next=q->next;
        free(q);
        printf("删除成功......\n\n");
        return 1;
    }
}
void MiddleSearch()
{
LinkList p,q,r,s;
r=L;s=L;p=L;
if(LengthList()%2==0)
    {
        if(LengthList()!=0)
        {
            while(p->next)
            {
                q=r->next;
                p=s->next->next;
                s=p;
                r=q;
            }
            printf("链表中间元素为: %d %d\n\n",q->data,q->next->data);
        }
        else
            printf("链表为空,无中间元素......\n\n");
    }
else
    {
        while(p)
        {
            q=r->next;
            p=s->next->next;
            s=p;
            r=q;
        }
printf("链表中间元素为: %d\n\n",q->data);
    }
    }

/*计算链表长度*/
int LengthList()
{
    LinkList p,q;
    int j=0;
    p=L->next;
    while(p)
    {
        q=p->next;
        j++;
        p=q;
    }
    return j;
}


//查看当前链表
void PrintfList()
{
    LinkList p,q;
    p=L->next;
    while(p)
    {
        q=p->next;
        printf("%d ",p->data);
        p=q;
    }
    printf("\n\n");
}

void Menu()
{
    printf("链表的相关操作:\n\n");
    printf("1.创建链表\n2.插入数据\n3.删除数据\n4.链表长度\n5.查找中间元素\n6.清空链表\n0.退出\n\n");
  printf("请选择功能键: ");
}

void main()
{
    int k;
    char key;
    L=(LinkList)malloc(sizeof(Node));
    L->next=NULL;//创建空链表
    Menu();
    for(k=0;;k++)
    {
        key=getchar();
        if(key=='1')
        {
            int n;
            printf("请输入要创建列表的长度:");
            scanf("%d",&n);
            printf("\nthe List: ");
            CreateListHead(n);
            PrintfList();
            Menu();
        }

        if(key=='2')
        {
            int i,e;
            printf("请输入要插入的位置和数据:");
            scanf("%d%d",&i,&e);

            if(InsertList(i,e)==1)
               {
                   printf("the List: ");
                   PrintfList();
               }
            Menu();
        }

        if(key=='3')
        {
            int i;
            printf("请输入要删除的位置:");
            scanf("%d",&i);
            if(DeleteList(i)==1)
               {
                   printf("\nthe List: ");
                   PrintfList();
               }
            Menu();
        }

        if(key=='4')
        {
            int a;
            a=LengthList();
            printf("链表长度:%d\n\n",a);
            Menu();
        }
if(key=='5')
{
    MiddleSearch();
    Menu();
}
        if(key=='6')
        {
            ClearList();
            printf("链表已清空......\n\n");
            Menu();
        }

        if(key=='0')
            return;
	}
}
