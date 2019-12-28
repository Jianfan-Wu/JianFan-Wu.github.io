---
title: Tree
date: 2019-12-28 16:40:50
tags:
---
## **Tree**



##### 知识框架

![框架](images\树.png)

##### 树

1. **基本性质—树**

   1) 树是一种逻辑结构，适用于数据元素之间含有层次关系，即一对多；

   2) 树中的节点数等于所有结点的度加1；

   3) 度为m的树中第i层上至多有m<sup>i-1</sup>个结点（ i≥1）；

   4) 高度为h的m叉树至多有(m<sup>h</sup>-1)/(m-1)个结点；

   5) 具有n个结点的m叉树的最小高度为 log<sub>m</sub>(n(m-1)+1) 向上取整；

2. **存储结构—树**

   1) **双亲表示法**：采用一组连续空间来存储每个结点，同时在结点中设置伪指针，指向其双亲结点在数组中的位置，指针域-1表示为根结点。不利于找孩子结点

   <img src="images\9.png" style="zoom:67%;" />
   
   存储结构
   
   ```c++
   typedef char ElemType;
typedef struct TNode
   {
    ElemType data; //结点数据
       int parent;    //该结点双亲在数组中的下标
   } TNode;           //结点数据类型
   
   #define Maxsize 100
   typedef struct
   {
       TNode nodes[MaxSize]; //结点数组
       int n;                //结点数量
   } Tree;                   //树的双亲表示结构
   ```
   
   2) **孩子表示法**：把每个结点的孩子结点排列起来存储成一个单链表。所以n个结点就有n个链表；如果是叶子结点，那这个结点的孩子单链表就是空的；  不利于找双亲
   
   ![](images\10.png)
   

存储结构

```c++
typedef char ElemType;
typedef struct CNode
   {
    int child;          //该孩子在表头数组的下标
       struct CNode *next; //指向该结点的下一个孩子结点
   } CNode， *Child;       //孩子结点数据类型
   
   typedef struct
   {
       Elemtype data;    //结点数据域
       Child firstchild; //指向该结点的第一个孩子结点
   } TNode;              //孩子结点数据类型
```

   3) **孩子兄弟表示法**：顾名思义就是要存储孩子和孩子结点的兄弟，就是设置两个指针，分别指向该结点的第一个孩子结点和这个孩子结点的右兄弟结点。 即左兄弟右孩子。不利于找双亲

<img src="images\14.png" style="zoom:67%;" />

存储结构

```c++
typedef char ElemType;
typedef struct CSNode
   {
       ElemType data;                        //该结点的数据域
       struct CSNode *firstchild, *rightsib; //指向该结点的第一个孩子结点和该结点的右兄弟结点
   } CSNode;                                 // 孩子兄弟结点数据类型
```


3. **森林与树的转换**

   1) **森林<==>二叉树**：先转化为树，再转化为二叉树；逆过程为根结点的右孩子断开为树；

   2) **树==>二叉树**：①兄弟加连线；②保留第一个子结点的连线，其余擦除；③旋转；

   ![树==>二叉树](https://img-blog.csdn.net/20130916192154203 "树==>二叉树")

   3) **二叉树==>树**：①连线——右孩子加线；②擦线；③旋转；

   ![二叉树==>树](https://img-blog.csdn.net/20130916192205156 "二叉树==>树")

4. **并查集**

   

5. **遍历**（详细参考二叉树的遍历）

   1) **先序遍历**：先访问根结点，再访问根结点的每棵子树。注：方法和二叉树一致；

   2) **后序遍历**：先访问根结点的每棵子树，再访问根结点。 访问子树也是按照先序的要求

   3) **对应关系**：

   |  **树**  | **森林** | **二叉树** |
   | :------: | :------: | :--------: |
   | 先根遍历 | 先序遍历 |  先序遍历  |
   | 后跟遍历 | 中序遍历 |  中序遍历  |

##### 二叉树

   1. **基本性质**
   
      1) 非空二叉树上叶子结点数等于度为2的结点数加1；
   
      2) 非空二叉树上第K层上至多有2<sup>k-1</sup>个结点（ K≥1）  
   
      3) 高度为H的二叉树至多有2<sup>h</sup> - 1个结点（ h≥1）  
   
      4) 具有N个（ N>0）结点的完全二叉树的高度为 log<sub>2</sub> (n+1) 或 （log<sub>2</sub> n） +1  
   
   2. **存储结构**
   
      1) **顺序存储**：用一组地址连续的存储单元依次自上而下、 自左至右存储完全二叉树上的结点元素，其中0表示结点为空；存储密度较小；
   
      | **Index** | **0** | **1** | **2** |   **3**   | **4** | **5** |
      | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
      |   **元素**   |   A   |   B   |     C     | 0 | D | E |
      
      
      
      2) **链式存储**：二叉树每个结点最多两个孩子，所以设计二叉树的结点结构时考虑两个指针指向该结点的两个孩子；二叉树的主要存储法
      
      | **lchild** | data | rchild |
      | :---: | :---: | :---: |
      | B | A | C |
      
      ```c++
      typedef struct BiTNode
      {
          ElemType data;                   //数据域
          struct BiTNode *lchild, *rchild; //指向该结点的左、右孩子指针
      } BiTNode, *BiTree;                  //二叉树结点结构
      ```
      
      
   
   3. **遍历**
   
      1) **先序遍历**：NLR
   
      ```c++
      //递归遍历法
      void PreOrder(BiTree T)
      {
          if (T != NULL)
          {
              printf("% c", T->data)   //访问根结点
              PreOrder(T->lchild);     //递归遍历左子树
              PreOrder(T->rchild);     //递归遍历右子树
          }
      }
      //非递归遍历
      Void PreOrderTraverse(BiTree b)
      {
          InitStack(S);
          BiTree p = b; //工作指针p
          while (p || !IsEmpty(S))
          {
              while (p)
              {
                  printf("% c", p->data); //先序先遍历结点
                  Push(S, p);             //进栈保存
                  p = p->lchild;
              }
              if (!IsEmpty(S))
              {
                  p = Pop(S);
                  p = p->rchild;
              }
          }
      }
      ```
   
      
   
      2) **中序遍历**：LNR
   
      ```c++
      //递归遍历法
      void InOrder(BiTree T)
      {
          if (T != NULL)
          {
              PreOrder(T->lchild);     //递归遍历左子树
              printf("% c", T->data)   //访问根结点
              PreOrder(T->rchild);     //递归遍历右子树
          }
      }
      //非递归算法
      Void PreOrderTraverse(BiTree b)
      {
          InitStack(S);
          BiTree p = b;           //工作指针p
          while (p || !IsEmpty(S))
          {
              while (p)
              { 
                  Push(S, p);     //中序先将结点进栈保存
                  p = p->lchild;
              } 
              p = Pop(S);         //遍历到左下角尽头再出栈访问
              printf("% c", p->data);
              p = p->rchild;      //遍历右孩子
          } 
      }
      ```
   
      
   
      3) **后序遍历**：LRN
   
      ```c++
      //递归遍历法
      void PostOrder(BiTree T)
      {
          if (T != NULL)
          {
              PreOrder(T->lchild);     //递归遍历左子树
              PreOrder(T->rchild);     //递归遍历右子树
              printf("% c", T->data)   //访问根结点
          }
      }
      //非递归遍历
      Void PostOrderTraverse(BiTree b)
      {
          InitStack(S);
          BiTree p = b， r = NULL; //工作指针p 辅助指针r
          while (p || !IsEmpty(S))
          {
              				 	//1.从根结点到最左下角的左子树都入栈
              if (p)
              {
                  Push(S, p);
                  p = p->lchild;
              }
              				 	//2.返回栈顶的两种情况
              else
              {
                  GetTop(S, p); 	  //取栈顶 注意不是出栈！
                  			 	 //①右子树还未访问，而且右子树不空，第一次栈顶
                  if (p->rchild && p->rchild != r)
                      p = p->rchild;
                  			 	 //②右子树已经访问或为空，接下来出栈访问结点
                  else
                  {
                      Pop(S, p);
                      printf("% c", p->data);
                      r = p;    	  //指向访问过的右子树根结点
                      p = NULL; 	  //使p为空从而继续访问栈顶
                  }
              }
          }
      }
      ```
   
      
   
      4) **层序遍历**：  若树为空，则什么都不做直接返回。否则从树的第一层开始访问， 从上而下逐层遍历，在同一层中，按从左到右的顺序对结点逐个访问。需借助队列完成，每访问一个结点就把它的子节点入队。  
   
      ```c++
      void LevelOrder(BiTree b)
      {
          InitQueue(Q);
          BiTree p;
          EnQueue(Q, b);          //根结点进队
          while (!IsEmpty(Q))
          {                       //队列不空循环
              DeQueue(Q， p)      //队头元素出队
                  printf("% c", p->data);
              if (p->lchild != NULL)
                  EnQueue(Q, p->lchild);
              if (p->rchild != NULL)
                  EnQueue(Q, p->rchild);
          }
      }
      ```
   
   4. **线索化**：对二叉树以某种次序遍历使其变为线索二叉树的过程就叫做线索化；

      1) **结点结构**

      ![image-20191105145805555](images\image-20191105145805555.png)
      
      ```c++
      typedef struct ThreadNode
      {
          ElemType data;
          struct ThreadNode *lchild, *rchild;
          int ltag, rtag;             //标志
      } ThreadNode, *ThreadTree;      //线索链表
      ```
      
      2) **规则**
      
        			ltag为0时指向该结点的左孩子，为1时指向该结点的前驱；
      
        			rtag为0时指向该结点的右孩子，为1时指向该结点的后继；
      
      
      
      3) **线索化**
      
      ![image-20191105151440508](images\image-20191105151440508.png)
      
      ```c++
      /*pre指向遍历时上一个访问过的结点 初值为NULL
        pre->rchild == NULL 中序遍历中前驱的右孩子如果为空，则访问完前驱下一个肯定访问该结点
        中序遍历对二叉树线索化的递归算法*/
      void InThread(ThreadTree &p, ThreadTree &pre)
      {
          if (p)  //p为根结点
          {
              InThread(p->lchild, pre);
              if (p->lchild == NULL)
              {
                  p->lchild = pre;
                  p->ltag = 1;
              }
              if (pre != NULL && pre->rchild == NULL)
              {
                  pre->rchild = p;
                  pre->rtag = 1;
              }
              pre = p;
              InThread(p->rchild, pre);
          }   
      }
      ```
      
      4) **遍历线索树**
      
      ```c++
      void InOrderTraverse(ThreadTree T)
      {
          ThreadTree p = T； 
          while (p)
          {
              while (p->ltag == 0)                //找到最左下角的结点
                  p = p->lchild;
              printf("%c", p->data);              
              while (p->rtag == 1 && p->rchild)   //按后继线索输出
              {
                  p = p->rchild;
                  printf("%c", p->data);
              }
              p = p->rchild;
          }
      }
      ```
      
      

##### 排序树

1. **基本定义**：二叉排序树(Binary Search Tree 二叉搜索树)或者是一棵空树，是二叉树；

2. **性质**：左小右大

   ​		1) 若左子树不空，则左子树上所有结点的值均小于它的根结点的值。

   ​		2) 若右子树不空，则右子树上所有结点的值均大于它的根结点的值。

   ​		3) 它的左右子树也是一棵二叉排序树。 

   注：对二叉排序树进行中序遍历可以得到一个递增的有序序列；二叉排序树的目的，不是为了排序，而是为了提高**查找**和**插入删除**关键字的速度

3. **存储结构**

   ```c++
   //和二叉树一致
   typedef struct BiTNode
   {                                    //二叉排序树结点结构
       int data;                        //结点数据
       struct BiTNode *lchild, *rchild; //指向该结点左右孩子的指针
   } BiTNode, *BiTree;
   ```

   1) **构造**

   ```c++
   //可以理解为从空树开始插入
   void Creat_BST(BiTNode *&t, ElemType key[], int n)
   {
                   //t是二叉排序树的根结点指针 key是关键字数组 n是关键字数量
       t = NULL;   //初始时t为空树
       int i = 0;
       while (i < n)
       {
           BST_Insert(t, key[i]);
           i++;
       }
   }
   ```

   2) **查找**

   ```c++
   //递归代码
   BiTNode *BST_Search(BiTNode *t, ElemType key)
   {
       if (t == NULL)
           return NULL;            //如果树为空则 返回空值
       else
       {
           if (t->key == key)      //查找成功
               return t;
           else if (key < t->key)
               return BST_Search(t->lchild, key);
           else
               return BST_Search(t->rchild, key);
       }
   }
   //非递归代码
   BiTNode *BST_Search(BiTNode *t, ElemType key)
   {
       BiTNode *p = t;         //工作指针 初值指向二叉排序树根结点
       while (p != NULL && key != p->data)
       {                       //p不为空且没有找到key
           if (key < p->data)
               p = p->lchild;  //如果key值比p指向结点值小，则查找左子树
           else
               p = p->rchild;  //如果key值比p指向结点值大，则查找右子树
       }
       return p;               //查找成功返回指向值为key值的结点的指针 查找失败返回NULL
   }
   ```

   3) **插入**

   ```c++
   int BST_Insert(BiTNode *&t, ElemType k)
   { //插入操作是要对树进行修改，所以是引用类型的指针
       if (t == NULL)
       {                                           //原树为空，新插入的记录为根结点
           t = (BiTNode *)malloc(sizeof(BiTNode)); 
           t->key = k;                             //该结点的关键字值赋值为k
           t->lchild = t->rhild = NULL;            //根结点初始化左右孩子为空
           return 1;                               //返回1，表示成功
       }
       else if (k == t->key)   //树中存在相同关键字的结点 插入失败
           return 0;
       else if (k < t->key)    //插入到t的左子树中
           return BST_Insert(t->lchild, k);
       else                    //插入到t的右子树中
           return BST_Insert(t->rchild, k);
   }
   ```

   4) **删除**：若是叶结点直接删除；若非叶结点则找左右子树中最小的接替即可

4. **折半查找树**（见查找一章）

   

##### AVL

1. **定义**：任意结点的左、右子树高度差的绝对值不超过1。目的：避免树的高度增长过快，降低二叉排序树的性能。注：首先实二叉排序树其次才是AVL；

   1) **平衡因子（BF）**：BF(T)=HL-HR, 其中HL、HR为T的左右子树的高度；

   2) **性质**：给定结点数为 n的AVL树的最大高度为O(log2n) ；（由斐波那契数列证得）

2. **调整**

   1) **相关词汇**：发现者==>最靠近插入结点且|BF|>1；破坏者==>刚插入结点；

   2) **LL旋转**：破坏者在发现者的左子树的左边

   例： “发现者”是Mar， “破坏者” Apr 在发现者左子树的左边，需要LL 旋转（左单旋）  

   <img src="images\image-20191106162244311.png" alt="image-20191106162244311" style="zoom:67%;" />

   理论模型：

   <img src="images\image-20191106162401070.png" alt="image-20191106162401070" style="zoom:67%;" />

   2) **RR旋转**：破坏者在发现者的右子树的右边

   例：“发现者”是Mar， “破坏者” Nov 在发现者右子树的右边，因而叫 RR 插入，需要RR 旋转（右单旋）

   ![image-20191106162021840](images\image-20191106162021840.png)  

   理论模型

   <img src="images\image-20191106161936649.png" alt="image-20191106161936649" style="zoom:67%;" />

   2) **LR旋转**：破坏者在发现者的左子树的左边

   例：  “发现者”是May， “破坏者” Jan在左子树的右边，需要LR 旋转，抓出现失衡的May,Aug,Mar; 其中Mar上升，Aug和May根据大小排在Mar的两边。May和Aug的子结点做相应的调整。

   <img src="images\image-20191106162524656.png" alt="image-20191106162524656" style="zoom:67%;" />

   理论模型：

   <img src="images\image-20191106162609485.png" alt="image-20191106162609485" style="zoom:67%;" />

   2) **RL旋转**：破坏者在发现者的左子树的左边

   例： “发现者”是Aug， “破坏者” Dec(或Feb)在右子树左边，需要RL旋转。注意要点同LR，关键抓出现失衡的三个结点。

   <img src="images\image-20191106163223255.png" alt="image-20191106163223255" style="zoom:67%;" />

   理论模型：

   <img src="images\image-20191106163634332.png" alt="image-20191106163634332" style="zoom:67%;" />

#####   Huffman

1. **定义**：最小带权路径长度(WPL)最小的二叉树(最优二叉树) ;

   1) **平均带权路径**：wi为第i个叶结点所带的权值，li为该叶结点到根结点的路径长度；
   $$
   WPL=\sum_{{1\le i\le n}} w_{i}l_{i}
   $$

2.  **构造**

   1) 将这N个结点分别作为N棵仅含一个结点的二叉树，构成森林F ;

   2) 构造一个新结点，并从F中选取两棵根结点权值最小的树作为新结点的左、右子树，并且将新结点的权值置为左、右子树上根结点的权值之和;

   3) 从F中删除刚才选出的两棵树，同时将新得到的树加入F中。重复上述步骤直至合并成一颗树； 
   
   例题：设给定权集w={5,7,2,3,6,8,9},试构造关于w的一颗哈夫曼树，并求出WPL；
   
   ​			WPL=4 *(2+3)+3 *(5+6+7)+2 *(8+9)=108 
   
   <img src="images\H.jpg" alt="题解" title="题解" style="zoom:33%;" />
   
   3. **代码实现* **
   
      ```c++
      typedef struct
      {
         int weight;
         int parent, lchild, rchild;
      } HTNode, *HuffmanTree; // 动态分配数组存储哈夫曼树;
      
      typedef struct
      {
         int weight;          // 结点的权值
         char bit[MAXBIT];    // 存放编码序列的数组
         int start;           // 编码的起始下标
      } HTCode, *HuffmanCode; // 动态分配数组存储哈夫曼编码
      
      void HuffmanTreeing(HuffmanTree &HT, int *w, int n)
      { // w中存放n个权值,构造n个叶子结点的哈夫曼树HT
         int i, s1, s2;
         HT = (HuffmanTree)malloc((2 * n - 1) * sizeof(HTNode)); // 分配哈夫曼树的存储空间
         for (i = 0; i < 2 * n - 1; i++)                         // 数组初始化
         {
            if (i < n)
               HT[i].weight = w[i]; // 赋权值
            else
               HT[i].weight = 0;
            HT[i].parent = -1; // 双亲域为空
            HT[i].lchild = -1; // 左孩子域为空
            HT[i].rchild = -1; // 右孩子域为空
         }
         for (i = n; i < 2 * n - 1; i++) // 构造哈夫曼树的n-1个非叶子结点
         {
            select(HT, i, s1, s2); // 选择两根结点权值最小和次小的两棵二叉树
                                   // 新二叉树存放在数组的第i个分量中,其权值是s1和s2的权值之和
            HT[i].weight = HT[s1].weight + HT[s2].weight;
            HT[i].lchild = s1; //新二叉树的左右孩子分别是s1和s2
            HT[i].rchild = s2;
            HT[s1].parent = HT[s2].parent = i; // 数组的第i个分量是s1和s2的双亲
         }
      } // HuffmanTreeing
      ```
   
      4. **哈夫曼编码**
   
         1) **定义**：根据所给条件构建哈夫曼树，然后将哈夫曼树的左右边分别0,1标记，‘0’转向左孩子，‘1’转向右孩子。访问各个结点根据路径的标记得到该结点编码；
   
         ![编码](images\image-20191106153802865.png)
   
         如图所示，A结点编码为：01；B结点编码为：000
   
         2) **补充**：计算某结点所在层数
   
         ```c++
         int level(bitree bt, bstnode *t)
         {                             //在二叉树t中查找指针t指向的给定结点
            int n = 0;                 //统计查找次数
            Bitree t = p;              //p为二叉树中工作指针
            if(bt != null)
            {
               n++;
               while(p->data != t->data)
               {                       //当工作指针所指向的结点不等于给定节点时
                  if(p->data < t->data)
                      p = p->lchild;   //在左子树查找
                  else
                      p = p->rchild;   //在右子树查找
                  n++;                 //层次加1
               }
            }
         }
         ```
   
         
   
   
   
   



