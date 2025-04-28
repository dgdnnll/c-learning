# 第一章、STL

## 1.pair

### 1.1 定义和结构

pair类可以存储两个不同类型的参数，并进行调用，可以进行==和！=操作。

成员变量：first、second

头文件：utility或者直接bits\stdc++.h

```c++
int main() {
	pair<int,char> p1(1,'A');
	pair<int,char> p2(1,'C');
	if(p1 == p2)
	cout<<p1.first<<","<<p2.second<<"\n";
	return 0;
}

int main() {
	pair<int,char> p1(1,'A');
	pair<int,char> p2(1,'C');
	if(p1.first == p2.first)
	cout<<p1.first<<","<<p2.second<<"\n";
	return 0;
}
```

### 1.2 可嵌套使用

```c++
int main() {
	pair<int,pair<int,char> > p1(1,make_pair(2,'A'));//两个> >之间需要一个空格
	cout<<p1.first<<","<<p1.second.second<<"\n";
	return 0;
}
```

### 1.3 自带排序

**排序规则：**

​	按照first成员进行升序排序；

​	如果first成员相等，则按照second成员升序排序

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <utility>
using namespace std;

int main() {
	vector<pair<int, int> > v;

	v.push_back(make_pair(3, 2));
	v.push_back(make_pair(1, 2));
	v.push_back(make_pair(1, 3));

	sort(v.begin(), v.end());
	for (const auto& p : v) {
		cout << p.first << "," << p.second << "\n";
	}

	return 0;
}
```

## 2.vector（重要）

### 2.1 定义和特性

在c++中，vector是一个**动态数组**容器，可以存储一系列**相同**类型的元素；

头文件：vector

**容器大小：**自动调整大小，动态分配空间

**元素访问**：索引从0开始，最后一个元素是size()-1。访问可以用[ ]或者at()函数

**元素添加和删除**：

​	push_back( )在末尾添加元素

​	pop_back( )在末尾删除元素,

​	insert( )在指定位置插入元素,

​	erase( )在指定位置删除元素。

**容器大小管理**：

​	size( )获取容器元素数量，

​	empty( )检查是否为空，

​	resize( )调整容器大小。

**迭代器：**

​	提供迭代器，用于遍历容器中的元素，begin( )指向第一个元素的迭代器，end( )执行那个**最后一个元素之后**位置的迭代器。 

### 2.2 vector的常用函数

```c++
vector<int> vec = {10,20,30};
for(auto it = vec.begin() ;it != vec.end();it++){
    cout << * it << " ";
}
```

### 2.3 vector排序去重

```c++
int main() {
	vector<int> vec = { 1,0,20,30,9 };
	
    sort(vec.begin(), vec.end());
	
    for (const auto &i :vec) {
		cout << i << " ";
	}

	return 0;
}
```

unique（）函数去重，属于头文件<algorithm>

返回值：一个指向重复值位置的迭代器

```c++
int main() {
	vector<int> vec = { 1,0,0,1,20,30,9 };

	sort(vec.begin(), vec.end());
	
	auto a = unique(vec.begin(), vec.end());

	vec.erase(a, vec.end());
	for (const auto &i :vec) {
		cout << i << " ";
	}

	return 0;
}
```

### 2.4 各类函数试用

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main() {
	vector<int> vec = { 1,0,0,1,6,5,9 };
	//末尾加值
	vec.push_back(5);
    //末尾出值
	vec.pop_back();
	cout << "原始值：" << endl;
	for (const auto& i : vec) {
		cout << i << " ";
	}
	cout << endl;

//擦除重复值
	sort(vec.begin(), vec.end());
	auto a = unique(vec.begin(), vec.end());
	vec.erase(a, vec.end());
	cout << "擦除重复值：" << endl;
	for (const auto &i :vec) {
		cout << i << " ";
	}
	cout << endl;
//插入值
	vec.insert(vec.begin() + 2, 3);
	cout << "插入值：" << endl;
	for (const auto& i : vec) {
		cout << i << " ";
	}
	cout << endl;
//删除值
	cout << "删除值：" << endl;
	vec.erase(vec.begin() + 4);
	for (const auto& i : vec) {
		cout << i << " ";
	}
	cout << endl;
//输出向量的大小
	cout << "向量的大小：" << endl;
	cout << vec.size() << endl;
//清空向量
	vec.clear();
//判断是否为空
	if (vec.empty()) {
		cout << "向量为空" << endl;
	}
	else
		cout << "向量不为空" << endl;
	return 0;
}


原始值：
1 0 0 1 6 5 9
擦除重复值：
0 1 5 6 9
插入值：
0 1 3 5 6 9
删除值：
0 1 3 5 9
向量的大小：
5
向量为空
```

## 3. list（考的不多）

```c++
#include <bits/stdc++.h>
using namespace std;
    
int main()
{
    list<int> mylist;
	
	for(int i=1;i<=5;i++){
		mylist.push_back(i);
	}  
	for(const auto &i : mylist)
	cout << i << ' ';
	cout<<'\n';
	reverse(mylist.begin(),mylist.end());
	for(const auto &i : mylist)cout<<i<<' ';
	cout<<'\n';
	
	mylist.insert(++ mylist.begin(),0);
	for(const auto &i : mylist){
		cout<< i <<' ';
	} 
	cout<<'\n';
	mylist.erase(++ ++ mylist.begin(),-- mylist.end());
	
	cout<<"链表大小为："<<mylist.size()<<'\n';
	for(const auto &i : mylist)cout<<i<<' ';
	cout<<'\n';
    return 0;
}

//输出：
1 2 3 4 5
5 4 3 2 1
5 0 4 3 2 1
链表大小为：3
5 0 1
```

## 4. stack

stack是一种**后进先出（LIFO）**的数据结构，

头文件<stack>

常用函数：

前三个都是在栈顶插入、弹出、返回栈顶元素；检查是否为空、返回栈中元素个数。

​	push()、pop()、top()、empty()、size()。

```c++
int main()
{
    stack<int> myStack;
	
	myStack.push(1);
	myStack.push(2);
	myStack.push(3);
	myStack.push(4);
	
	cout<<"栈顶元素："<<myStack.top()<<endl;
	
	myStack.pop();
	cout<<"弹出后栈顶元素："<<myStack.top()<<endl; 
	
	if(myStack.empty())
	cout<<"为空"<<endl;
	else
	cout<<"不为空"<<endl; 
	
	cout<<"栈的大小："<<myStack.size()<<endl; 
    return 0;
}
```

## 5. queue

### 5.1 queue队列

先进先出（FIFO）的数据结构；

函数：

push()、pop()、front(返回队首)、back(返回队尾)、empty()、size()。

### 5.2 priority_queue优先队列（重要）

不同点：按照优先级排序，默认情况从大到小排序，最大的在最前面。

常用函数：push()、pop()、top()、empty()、size()。



## 6. map（重要）

### 6.1 map

关联容器，存储一组键值对，<key,  value>

**根据键值对自动进行排序**

使用的是红黑树数据结构来实现。

**有顺序的，且是从小到大排序**。

| 函数        | 功能                                                         |
| ----------- | ------------------------------------------------------------ |
| insert      | 插入元素                                                     |
| erase       | 删除元素                                                     |
| find        | 查找元素                                                     |
| count       | 用于检查某个 **key 是否存在**，并返回 key 出现的次数。由于 `map` **不允许键重复**，所以 `map.count(key)` 的返回值**只能是 0 或 1**。 |
| size        | 返回元素个数                                                 |
| begin       | 返回指向容器起始位置的迭代器                                 |
| end         | 返回指向容器末尾位置的迭代器                                 |
| clear       | 清空容器                                                     |
| empty       | 判断是否为空                                                 |
| lower_bound | 返回指向第一个不小于指定键的元素位置=                        |
| upper_bound | 返回指向第一个大于指定键的元素位置                           |

```c++
int main()
{
    map<int,string> mymap = {{1,"Apple"},{2,"Banana"},{3,"Orange"},{5,"Apple"}};
    
    mymap.insert(make_pair(4,"Grapes"));
    
    cout<<"根据键值查找元素："<<mymap[1]<<endl;
    //有vector属性，可以使用迭代器遍历 
    for(const auto& i:mymap){
    	cout<<"key: "<<i.first<<"value: "<<i.second<<'\n';
    }
    //删除元素 
    mymap.erase(3);
    if(mymap.count(3)==0){
    	cout<<"Key 3 not found."<<endl;
    
    }
    //清空容器 
    mymap.clear();
    if(mymap.empty()){
    	cout<<"map is empty."<<endl;
    }
    return 0;
}

//输出
根据键值查找元素：Apple
key: 1value: Apple
key: 2value: Banana
key: 3value: Orange
key: 4value: Grapes
key: 5value: Apple
//有顺序的，且是从小到大排序
Key 3 not found.
map is empty.
```



### 6.2 unordered_map

存储一组键值对，每个键都是唯一的。

**不会排序**所以不保证元素的顺序，而是使用哈希函数将键映射到存储桶中。

| 函数   | 功能   |
| ------ | ------ |
| insert | 一样的 |
| erase  |        |
| find   |        |
| count  |        |
| size   |        |
| empty  |        |
| clear  |        |

```c++
unordered_map<int,string> mymap = {{1,"Apple"},{2,"Banana"},{3,"Orange"},{5,"Apple"}};
//。。。。其他不变，只改数据结构名称

//输出
根据键值查找元素：Apple
key: 4value: Grapes
key: 5value: Apple
key: 3value: Orange
key: 2value: Banana
key: 1value: Apple
//无顺序，你怎么插入的，就怎么展示，是栈插入，先进去的后出来
Key 3 not found.
map is empty.

```

### 6.3 unordered_set

无序集合，只存唯一的Key。

### 6.4 注意

map、pair分别访问键和值用`map(pair).first`和`map(pair).second`不用加()。

### 6.5 例题

小明又新学了一个概念，叫做完美序列。一个仅包含数字序列被称为完美序列，当且仅当数字序列中每个数字出现的次数等于这个数字。比如 (1)(1)，(2,2,3,3,3)(2,2,3,3,3)。空序列也算。现在小明得到了一个数字序列，他想知道最少要删除多少个数字才能使得这个数字序列成为一个完美序列。

**输入格式**

输入包括两行。

第一行输入一个整数 n，表示数字序列中数字的个数。

第二行，包括 n个整数，是数字序列中具体的每个数字。

**输出格式**

输出一个整数，表示最少要删除的数字个数。

**样例输入**

```text
6
3 3 3 1 13 15 
```

**样例输出**

```text
2
```

**评测数据规模**

对于所有评测数据，1≤n≤105,ai≤1091≤*n*≤105,*a**i*≤109。

#### 错误原因

误认为13、15这种数需要拆分为2个数字，比如13拆分为1，3，然后加入0-9的数之中，以为数字只包括0-9，刚好这题按这个逻辑答案也是2，没想到13、15不用拆分，直接算一个数。

### 6.6 map\unordered_map\unordered_set的区别（重要）

| 特性         | `unordered_set`  | `unordered_map`            | `map`                          |
| ------------ | ---------------- | -------------------------- | ------------------------------ |
| 底层结构     | 哈希表           | 哈希表                     | 红黑树（平衡二叉搜索树）       |
| 数据存储     | 只存 key         | 存储键值对（key -> value） | 存储键值对（key -> value）     |
| 是否有序     | ❌ 无序           | ❌ 无序                     | ✅ 自动按 key 排序（升序）      |
| 访问效率     | O(1) 平均        | O(1) 平均                  | O(log n)                       |
| 是否允许重复 | ❌ 不允许重复元素 | ❌ key 不可重复             | ❌ key 不可重复                 |
| 是否支持区间 | ❌ 不支持区间查找 | ❌ 不支持区间查找           | ✅ 支持区间、lower_bound 等操作 |
| 是否自动排序 | ❌ 无             | ❌ 无                       | ✅ key 自动排序                 |

**注意**：

- `unordered_*` 的 key 类型必须能哈希，比如 `int`、`string` 没问题，`pair` 或自定义类型要自定义哈希函数。

- `map` 可以对复杂类型做排序，只要你提供 `<` 运算符。

```python
unordered_set<int> s;

s.insert(10);        // 插入元素
s.erase(10);         // 删除元素
s.count(10);         // 是否存在（返回0或1）
s.find(10);          // 返回迭代器，找不到返回 s.end()
s.size();            // 元素数量
s.empty();           // 是否为空
s.clear();           // 清空

```



```python
unordered_map<string, int> m;

m["Tom"] = 18;       // 插入或更新
m.at("Tom");         // 访问键（不存在会抛异常）
m.erase("Tom");      // 删除键
m.count("Tom");      // 是否存在 key
m.find("Tom");       // 返回迭代器，找不到返回 m.end()
m.size();            // 当前元素个数
m.empty();           // 是否为空
m.clear();           // 清空

for (auto& [k, v] : m) {
    cout << k << " : " << v << endl;
}

```



```python
map<int, string> mp;

mp.lower_bound(2);   // 返回 >=2 的第一个迭代器
mp.upper_bound(2);   // 返回 >2 的第一个迭代器

mp.begin();          // 最小 key 的元素
mp.rbegin();         // 最大 key 的元素
mp.end();            // 尾后迭代器（不含）

```

