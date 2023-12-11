# Acwing827.双链表

[//]: # (推荐题解模板，请替换blablabla等内容 ^^)

## 双链表
#### 题目地址：
#### https://www.acwing.com/problem/content/829/
----------
#### 题解地址：
#### https://www.acwing.com/user/myspace/solution/update/217975/
----------

#### python3 代码
```
N=100010
l=[0]*N
r=[0]*N
e=[0]*N

#初始化
#头结点下标为0，尾节点下标为1，都不存数据
idx=2
r[0]=1
l[1]=0

#在下标为k的结点的右边插入一个数
def insert(k,x):
    global idx
    e[idx]=x
    l[r[k]]=idx
    r[idx]=r[k]
    r[k]=idx
    l[idx]=k
    idx+=1

#删除下标为k的结点
def delete(k):
    r[l[k]]=r[k]
    l[r[k]]=l[k]
    r[k]=-1#可以不要，-1表示空结点下标
    l[k]=-1#可以不要，-1表示空结点下标
    
m=int(input())
while m>0:
    m-=1
    a=input().split()
    if a[0]=='L':
        insert(0,int(a[1]))
    elif a[0]=='R':
        insert(l[1],int(a[1]))
    elif a[0]=='D':
        delete(int(a[1])+1)
    elif a[0]=='IL':
        insert(l[int(a[1])+1],int(a[2]))#第k个插入的数的下标已经是k+1了
    elif a[0]=='IR':
        insert(int(a[1])+1,int(a[2]))
        

res=[]
i=r[0]
while i!=1:
    res.append(e[i])
    i=r[i]
print(' '.join(map(str,res)))
    
```

----------
#### y总c++代码
```
#include <iostream>

using namespace std;

const int N = 100010;


// head 表示头结点的下标
// e[i] 表示节点i的值
// ne[i] 表示节点i的next指针是多少
// idx 存储当前已经用到了哪个点
int head, e[N], ne[N], idx;

// 初始化
void init()
{
    head = -1;
    idx = 0;
}

// 将x插到头结点
void add_to_head(int x)
{
    e[idx] = x, ne[idx] = head, head = idx ++ ;
}

// 将x插到下标是k的点后面
void add(int k, int x)
{
    e[idx] = x, ne[idx] = ne[k], ne[k] = idx ++ ;
}

// 将下标是k的点后面的点删掉
void remove(int k)
{
    ne[k] = ne[ne[k]];
}

int main()
{
    int m;
    cin >> m;

    init();

    while (m -- )
    {
        int k, x;
        char op;

        cin >> op;
        if (op == 'H')
        {
            cin >> x;
            add_to_head(x);
        }
        else if (op == 'D')
        {
            cin >> k;
            if (!k) head = ne[head];
            else remove(k - 1);
        }
        else
        {
            cin >> k >> x;
            add(k - 1, x);
        }
    }

    for (int i = head; i != -1; i = ne[i]) cout << e[i] << ' ';
    cout << endl;

    return 0;
}
```
-----
#### 链接：
#### https://www.acwing.com/activity/content/code/content/42977/
-----

---

* Link: https://github.com/zjljy/Algorithm/issues/8
* Labels: 
* Creation Date: 2023-12-11T13:17:14Z
