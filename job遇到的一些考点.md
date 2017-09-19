---
title: job遇到的一些考点
tags: 数据结构,算法
grammar_cjkRuby: true
---

 1. **C语言指针操纵** 9
 2. **C语言++i define 等指令** 
 3. **图的遍历最小路径等问题**
 4. **排序算法**
 5. **算法书上的一些东西**
 ### 数组和链表的区别
 分析的思路，先分析个是什么，然后再由是什么得到优缺点。
  数组,在内存上给出了连续的空间
  链表,内存地址上可以是不连续的,每个链表的节点包括原来的内存和下一个节点的信息
  数组优于链表的: 
1.内存空间占用的少,因为链表节点会附加上一块或两块下一个节点的信息.但是数组在建立时就固定了.所以也有可能会因为建立的数组过大或不足引起内存上的问题. 
2.数组内的数据可随机访问.但链表不具备随机访问性.这个很容易理解.数组在内存里是连续的空间.比如如果一个数组地址从100到200,且每个元素占用两个字节,那么100-200之间的任何一个偶数都是数组元素的地址.可以直接访问.链表在内存地址可能是分散的.所以必须通过上一节点中的信息找能找到下一个节点. 
3.查找速度上.这个也是因为内存地址的连续性的问题.不罗索了. 
链表优于数组的: 
1.插入与删除的操作.如果数组的中间插入一个元素,那么这个元素后的所有元素的内存地址都要往后移动.删除的话同理.只有对数据的最后一个元素进行插入删除操作时,才比较快.链表只需要更改有必要更改的节点内的节点信息就够了.并不需要更改节点的内存地址. 
2.内存地址的利用率方面.不管你内存里还有多少空间,如果没办法一次性给出数组所需的要空间,那就会提示内存不足,磁盘空间整理的原因之一在这里.而链表可以是分散的空间地址. 
3.链表的扩展性比数组好.因为一个数组建立后所占用的空间大小就是固定的.如果满了就没法扩展.只能新建一个更大空间的数组.而链表不是固定的,可以很方便的扩展.

   数组与链表的优缺点；    
    数组:

    优点：使用方便 ，查询效率 比链表高，内存为一连续的区域 

    缺点：大小固定，不适合动态存储，不方便动态添加
    链表：

     优点：可动态添加删除   大小可变   
     缺点：只能通过顺次指针访问，查询效率低
 ### 指针
``` cpp?linenums
int (*p)(int,int) //表示指向函数的指针
int (*p)[4] //表示指向一维数组的指针
//http://www.jb51.net/article/54220.htm
```
### sizeof 
[sizeof 结构体][1]
sizeof修饰数组和指针得到的结果是不是一样的，函数传惨得到的是指针
### const 关键字
#### 修饰常量
用const修饰的变量是不可变的，以下两种定义形式在本质上是一样的：
``` cpp
const int a = 10;
int const a = 10;
```
#### 修饰指针
如果const位于\*的左侧，则const就是用来修饰指针所指向的变量，即指针指向为常量；
如果const位于\*的右侧，const就是修饰指针本身，即指针本身是常量。
因此，推荐使用int const\* p，而不是使用const int\* p（虽然两者意义完全一样），这样更容易理解。

``` cpp
int a = 10;
const int* p = &a;            // 指针指向的内容不能变
int const* p = &a;            // 同上
int* const p = &a;            // 指针本身不能变
const int* const p = &a;      // 两者都不能变
int const* const p = &a;      // 同上
//可以这样理解，const在*前面const修饰的是*p，因此是p是一个指向一个常量的指针，* const p 可以理解为const修饰的是p，那么p就是一个常指针，p不能够变。
```
### virtual
类Base中加了Virtual关键字的函数就是虚拟函数（例如函数print），于是在Base的派生类Derived中就可以通过重写虚拟函数来实现对基类虚拟函数的覆盖。当基类Base的指针point指向派生类Derived的对象时，对point的print函数的调用实际上是调用了Derived的print函数而不是Base的print函数。这是面向对象中的多态性的体现 

``` cpp
class Base
{
public:Base(){}
public:
       virtual void print(){cout<<"Base";}
};
 
class Derived:public Base
{
public:Derived(){}
public:
       void print(){cout<<"Derived";}
};
 
int main()
{
       Base *point=new Derived();
       point->print();
}
```
struct A
{
char a;　　　//内存位置:  [0]
double b;　  // 内存位置: [8]...[15]
int c;　　　　// 内存位置: [16]...[19]　　----　　规则1
};　
32位编译器：32位系统下指针占用4字节
      char ：1个字节
      char\*（即指针变量）: 4个字节（32位的寻址空间是2^32, 即32个bit，也就是4个字节。       同理64位编译器）
      short int : 2个字节
      int：  4个字节
      unsigned int : 4个字节
      float:  4个字节
      double:   8个字节
      long:   4个字节
      long long:  8个字节
      unsigned long:  4个字节
64位编译器：64位系统下指针占用8字节
      char ：1个字节
      char\*(即指针变量): 8个字节
      short int : 2个字节
      int：  4个字节
      unsigned int : 4个字节
      float:  4个字节
      double:   8个字节
      long:   8个字节
      long long:  8个字节
      unsigned long:  8个字节



 ### define ++ i ,  i++
```cpp?linenums
// 前缀形式 ++i：
int& int::operator++() //这里返回的是一个引用形式，就是说函数返回值也可以作为一个左值使用
{//函数本身无参，意味着是在自身空间内增加1的
  *this += 1;  // 增加
  return *this;  // 取回值
}

//后缀形式 i++:
const int int::operator++(int) //函数返回值是一个非左值型的，与前缀形式的差别所在。
{//函数带参，说明有另外的空间开辟
  int oldValue = *this;  // 取回值
  ++(*this);  // 增加
  return oldValue;  // 返回被取回的值
} 
```
后缀形式返回的是零时变量不能够作为左值


``` cpp?linenums
#define Add(a,b) a+b;
c * Add(a,b) * d
c*a + b*d
```
define只是简答的替换,很多操作不安全，typedef 是安全的的
typedef int (*p) [5]  PP 

### 二叉树的遍历
**概念**

 1. 前序遍历（先根遍历），没颗子树都按照 `根节点->左子树->右子树` 的顺序来递归访问
 2. 中序遍历（中根遍历），没颗子树都按照 `左子树->根节点->右子树` 的顺序来递归访问
 3. 后序遍历（后根遍历），没颗子树都按照 `左子树->右子树->根节点` 的顺序来递归访问
前序遍历`10,6,4,8,14,12,16`
中序遍历`4,6,8,10,12,14,16`
后续遍历`4,8,8,12,16,14,10`
 ![二叉树的遍历][2]
 已知两种求另外一种一般先画树，然后求出另外一种。
 关键点在与找根节点，中序遍历中`10`为根节点，左边为左子树，右边为右子树。然后确定左子树的根，左子树的左子树的根...
#### 代码
**递归**
前序遍历（递归）代码如下，中序遍历，后序遍历简答的改一下if中语句的先后顺序即可

``` java?linenums
    public static void preOrderTraverse(Treenode rootnode){
        Treenode p = rootnode;
        if(p!=null){
            System.out.println(p.value);  //表示访问了
            preOrderTraverse(p.leftchild); //
            preOrderTraverse(p.rightchild);
        }
        else return;
    }
```
**前序遍历递推**

由于没有parent指针，所有非递归形式一定要借助栈
先让根进栈。只要栈不为空，就可以弹栈。每次弹出一个节点，要把它的左右节点进栈（左边后进去，先访问）

``` java?linenums
// 传入树的根节点
public static void preOrderNonrecur(Treenode rootnode){
	if(rootnode==null){
		return;
	}
	Treenode p = rootnode;
	Stack<Treenode> stack = new Stack<Treenode>();
	stack.push(p);
	while(stack.isEmpty()!=true){
		p = stack.pop();
		System.out.println(p.value);  // 这个地方相当于访问了
		if(p.rightchild != null ){
			stack.push(p.rightchild);
		}
		if(p.leftchild != null){
			stack.push(p.leftchild);  
		}
	}
}
```
**中序遍历（递推）**

 1. current = root;
 2. 把current, current的左孩子，current的左孩子的左孩子都入栈,直至current = null -> 跳到step 3
 3. （current = current.left, push(current)）

``` javascript?linenums
public static void inOrderNonrecur(Treenode rootnode){
	if(rootnode==null){
		return;
	}

	Treenode current = rootnode;
	Stack<Treenode> stack = new Stack<Treenode>();
	while(current != null||stack.isEmpty()!=true){
		while(current!=null){
			stack.push(current);
			current = current.leftchild;
		}
		if(current==null){
			Treenode node = stack.pop();
			System.out.println(node.value);
			current = node.rightchild;
			}
	}   
}
```
**后序遍历（递推）**

``` java?linenums
public static void postOrderNonrecur(Treenode rootnode){
	if(rootnode==null){
		return;
	}   
	Stack<Treenode> stack = new Stack<Treenode>();
	Treenode current = rootnode;
	while(current !=null || stack.isEmpty()!=true){     
		//step 1 
		while(current!=null){   
			if(current.rightchild!=null){
				stack.push(current.rightchild);
			}
			stack.push(current);
			current = current.leftchild;
		}

		// step2 既然出栈了，该节点肯定没有左孩子。
		current = stack.pop();
	if(current.rightchild!=null && !stack.isEmpty() && current.rightchild == stack.peek())  {
				stack.pop(); //出栈右孩子
				stack.push(current);
				current = current.rightchild;
		}
		else{
			System.out.println(current.value);
			current = null;
		}
	}
}
```

## 图的操作
### 最段路径

### 图的搜索
**广度搜索**

广度搜是一个分层搜索的过程
如下图，其广度优先遍历的顺序为`1->2->3->4->5->6->7->8`
![实例][3]


 

``` python?linenums
waitlist=[] # 存放待入邻节点的节点的队列
traverlist=[] # 存放遍历顺序的队列

origin=0 # 初始节点

# 将初始节点标记为已访问
waitlist.append(origin)


while len(waitlist)!=0:
    front=waitlist.pop() # 最前面的出队列  
    frontNeighbourList=front.getNeighbourList() #获取邻居集合
    for note in frontNeighbourList:
        # 访问note
        traverlist.append(note)
        waitlist.append(note)
# 事实上出队列的顺序就是访问的顺序代码可以改写如下，两者是等价的
waitlist.append(origin)
while len(waitlist)!=0:
    front=waitlist.pop() # 最前面的出队列  事实上出队列的顺序就是访问的顺序
	traverlist.append(front)    #
    frontNeighbourList=front.getNeighbourList() #获取邻居集合
    for note in frontNeighbourList:
        # 访问note
        waitlist.append(note)
```
**深度搜索**
首先访问第一个邻接结点，然后再以这个被访问的邻接结点作为初始结点，访问它的第一个邻接结点。如下图深度优先遍历顺序为`1->2->4->8->5->3->6->7`
![图2][4]

``` python?linenums
waitStack=[] # 存放已访问顶点的新栈
traverlist=[] # 存放遍历顺序的队列

origin=0 # 初始节点

# 将初始节点标记为已访问
waitStack.insert(0,origin) # 入栈
traverlist.append(origin) # 已经访问

while len(waitStack)!=0: # 栈非空
    top=waitStack[-1] #栈顶元素
    frontNeighbourList=top.getNeighbourList() #获取邻居集合
    if frontNeighbourList - traverlist !=0: # 集合减法，如果里面有为访问过的点
        nextNote= frontNeighbourList中未被访问的元素
        traverlist.append(nextNote) # 标记为已访问
		waitStack.push(nextNote)
    else: # 没有未被访问的邻居集合则出栈
        waitStack.pop()
```
## 图的最短距离


  [1]: http://blog.csdn.net/ls5718/article/details/51207330
  [2]: ./images/1099130089-550974a69a5bc_articlex.png "1099130089-550974a69a5bc_articlex"
  [3]: ./images/1895528507-5530c8a42d51e_articlex.png "1895528507-5530c8a42d51e_articlex"
  [4]: ./images/1895528507-5530c8a42d51e_articlex.png