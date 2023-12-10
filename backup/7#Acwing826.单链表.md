# Acwing826.单链表

#### 题解地址：https://www.acwing.com/solution/content/217971/
-----------
## Acwing826.单链表

### 题目链接

https://www.acwing.com/activity/content/problem/content/863/

----------
#### python3 代码
```
N=100010
e=[0]*N
ne=[0]*N

#初始化
head=-1
idx=0


#将x插到头结点
#idx,head,ne[idx]都是地址（指针）
#idx始终指向当前要增加的地方
def add_to_head(x):
    global idx
    global head
    e[idx]=x
    ne[idx]=head
    head=idx
    idx+=1
    
#将x插到下标是k（idx=k）的点后面
#idx始终指向当前要删除的地方
def add(k,x):
    global idx
    e[idx]=x
    ne[idx]=ne[k]
    ne[k]=idx
    idx+=1

#将下标为k的点的下一个点删除
def delete(k):
    tmp=ne[k]#可以不要
    ne[k]=ne[ne[k]]
    ne[tmp]=-1#可以不要


m=int(input())
while m>0:
    m-=1
    a=list(input().split())
    if a[0]=='H':
        add_to_head(int(a[1]))
    elif a[0]=='D':
        if int(a[1])==0:
            tmp=head#可以不要
            head=ne[head]
            ne[tmp]=-1#可以不要
        else:
            delete(int(a[1])-1)
    elif a[0]=='I':
        add(int(a[1])-1,int(a[2]))
        
i=head
res=[]
while i!=-1:
    res.append(e[i])
    i=ne[i]
print(' '.join(map(str,res)))

```

----------
### 附y总c++代码
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
-------------
#### 链接

#### https://www.acwing.com/activity/content/code/content/42977/
-------------

---

* Link: https://github.com/zjljy/Algorithm/issues/7
* Labels: `数据结构`, `单链表`, `算法基础课`
* Creation Date: 2023-12-10T15:18:13Z
