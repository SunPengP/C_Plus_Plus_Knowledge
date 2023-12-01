# STL库

## <mark>容器</mark>

- **序列式容器**：强调值的排序，序列式容器中的每个值都有固定的位置
- **关联式容器**：二叉树结构，各元素之间没有严格的物理上的顺序关系

#### <mark>vector</mark>

- 访问一个容器`vector<数据类型>`需要创建一个迭代器`vector<数据类型>::iterator`，每个容器都有自己所属类型的迭代器

- ```python
  #include <iostream>
  #include <vector>
  #include <algorithm>
  
  void print_value(int val)
  {
  	std::cout << val << std::endl;
  }
  int main()
  {
  	// 创建了一个vector容器，数组
  	std::vector<int> v;
  	// 向容器中插入数据
  	v.push_back(10);
  	v.push_back(20);
  	v.push_back(30);
  	// 通过迭代器访问容器中的数据
  	// 起始迭代器，指向容器中第一个元素,v.begin()返回的是一个指针
  	std::vector<int>::iterator itBegin = v.begin(); 
  	// 结束迭代器，指向容器中最后一个元素的下一个位置,v.end()返回一个指针
  	std::vector<int>::iterator itEnd = v.end(); 
  	// 遍历容器
  	while (itBegin != itEnd)
  	{
  		std::cout << *itBegin << std::endl;
  		itBegin++;
  	}
  	std::cout << "使用for循环遍历容器" << std::endl;
  	for (std::vector<int>::iterator it = v.begin(); it != v.end(); it++)
  	{
  		std::cout << *it << std::endl;
  	}
  	// 使用标准算法遍历
  	std::cout << "使用标准算法遍历" << std::endl;
  	std::for_each(v.begin(), v.end(), print_value);
  	return 0;
  }
  ```

- vector容器中存放自定义的数据类型

  ```python
  class Person
  {
  public:
  	Person(std::string name, int age)
  	{
  		this->p_name = name;
  		this->p_age = age;
  	}
  	std::string p_name;
  	int p_age;
  };
  void test()
  {
  	std::vector<Person> v;
  	Person p1("he", 12);
  	Person p2("she", 13);
  	Person p3("it", 14);
  	v.push_back(p1);
  	v.push_back(p2);
  	v.push_back(p3);
  	for (std::vector<Person>::iterator it = v.begin(); it != v.end(); it++)
  	{
  		std::cout <<"姓名："<< (*it).p_name <<"；年龄："<< (*it).p_age << std::endl;
  	}
  }
  int main()
  {
  	test();
  	return 0;
  }
  ```

- 容器中嵌套容器

  ```python
  void test()
  {
  	std::vector<std::vector<int>> v;
  	// 创建内部容器
  	std::vector<int> v1;
  	std::vector<int> v2;
  	std::vector<int> v3;
  	// 向内部容器中插入数据
  	for (int i = 0; i < 3; i++)
  	{
  		v1.push_back(i);
  		v2.push_back(i+1);
  		v3.push_back(i+2);
  	}
  	// 将内部容器插入到外部容器中
  	v.push_back(v1);
  	v.push_back(v2);
  	v.push_back(v3);
  	for (std::vector<std::vector<int>>::iterator out_v = v.begin(); out_v != v.end(); out_v++)
  	{
  		for (std::vector<int>::iterator in_v = (*out_v).begin(); in_v != (*out_v).end(); in_v++)
  		{
  			std::cout << *in_v << std::endl;
  		}
  	}
  
  }
  ```

#### <mark>string</mark>

- string是c++风格的字符串，string`本质`上是一个类

- string内部<font  size=5><mark>`封装了char*`</mark></font>，管理这个字符串，是一个`char*`型的容器

- 字符串初始化

  ```python
  void test()
  {
  	std::string s1; // 默认构造
  	const char* str = "hello,world";
  	std::string s2(str); //c风格的字符串初始化string类型的字符串
  	std::string s3(s2); // string拷贝构造
  	std::string s4(10, 'a');// 10个元素全为a的字符串
  }
  ```

- 字符串赋值

  ```python
  std::string s1;
  	// 除了用"="好给字符串赋值，还可以使用assign
  s1.assign("hello,world");
  
  std::string s = "hello,world";
  std::string s2;
  	// 如果传入的是一个已经初始话后的string字符串，则是从第n个开始往后取值
  	// 如果直接是一个字符串，则是取前n个字符，作为返回结果
  s2.assign(s, 3);
  s2.assign("good,luck", 3);
  std::cout << s2 << std::endl;
  ```

- string字符串拼接

  ```python
  void test()
  {
  	// 用 + 号
  	std::string s1 = "hello";
  	s1 += ",world";
  	std::cout << s1 << std::endl;
  	// 用append函数
  	std::string s2 = "good";
  	s2.append(",luck");
  	std::cout << s2 << std::endl;
  
  	std::string s3;
  	// s3.append(s2, 3); //从下标索引为3的开始，包括3
  	// s3.append(s2,0,2); // 从索引0开始，截取2个字符
  	s3.append("good", 3); // 取前三个元素，索引0~2 
  	std::cout << s3 << std::endl;
  }
  ```

- string的查找和替换

  ```python
  void test()
  {
  	// 查找
  	std::string s1 = "hello,world";
  	/*
  	如果查找的元素存在，
  	则返回对应的下标索引；
  	当字符串中多次出现要查找的元素，
  	则返回第一次出现的位置；
  	如果不存在，则返回 -1
  	*/
  	int index = s1.find("ll");
  	// rfind是从右往左找
  	std::cout << index << std::endl;
  
  	// 替换
  	// 从下标1开始，到下标4，替换为给定的字符串
  	s1.replace(1, 4, "i");
  	std::cout << s1 << std::endl;
  }
  ```

- string的比较，`compare()`

  ```c++
  void test()
  {
  	std::string s1 = "hello";
  	std::string s2 = "world";
  	/*
  	相等返回 0 ；
  	大于返回 1 ；
  	小于返回 -1 ；
  	*/
  	int a = s1.compare(s2);
  	std::cout << a << std::endl;
  }
  ```

  

- 访问string字符串

  ```c++
  void test()
  {
  	std::string s = "hello";
  	std::cout << "第一种访问方法：";
  	for (int i = 0; i < s.size(); i++)
  		std::cout << s[i] << "\t";
  	std::cout <<"\n"<<"第二种访问方法：";
  	for (int i = 0; i < s.size(); i++)
  		std::cout << s.at(i) << "\t";
  }
  ```

- 字符串插入

  ```c++
  void test()
  {
  	std::string s = "hello";
  	std::cout << "第一种访问方法：";
  	for (int i = 0; i < s.size(); i++)
  		std::cout << s[i] << "\t";
  	std::cout <<"\n"<<"第二种访问方法：";
  	for (int i = 0; i < s.size(); i++)
  		std::cout << s.at(i) << "\t";
  	
  }
  ```

- 求子串

  ```c++
  std::string s ="hello, world";
  s_sub = s.substr(1,3); //根据下标索引取子串
  ```


#### <mark>vector</mark>: 支持随机访问

<mark>动态扩展：</mark> 不是在原空间之后续接新空间，而是寻找更大的内存空间，然后<mark><font color=red>将原数据拷贝到新空间，释放原空间</font></mark>

```c++
std::vector<int> v = {1,2,3,4};
// 插入元素
v.push_back(2); // 在尾端插入元素 2
v.pop_back(); // 删除最后一个元素
v.insert(iterator,ele); // 利用迭代器在指定位置插入元素 ele
v.insert(iterator, int count, ele); // 在迭代器指向的位置插入 cout 个元素 ele（插入的元素的值）
v.erase(iterator); // 删除迭代器指向位置的元素
v.erase(iterator_start, iterator_end); // 删除迭代器从 start到 end 之间的元素
v.clear(); // 删除容器中的所有元素

// 利用区间方式进行构造
std::vector<int> v2(v.begin(),v.end());
std::vector<int> v3(10,3); // v3的元素为10个3
std::vector<int> v4(v3);


// 赋值
v2 = v1;
v3.assign(v2.begin(),v2.end());
v4.assign(10,30); // 10个30

// 容量和大小
v.empty(); // 判断是否为空
v.capacity(); // 容器的容量
v.size(); // 返回容器中元素的个数；v.capacity()大于等于v.size()
v.resize(int num); // 重新指定容器的长度为 num，若容器变长，则以默认值填充新位置； 若容器变短，则末尾超出容器长度的值被删除 
v.resize(int num, elem); // 重新指定容器的长度为 num，若容器变长，则以 elem 填充新位置； 若容器变短，则末尾超出容器长度的值被删除 


// 数据存取
v.at(int idx); // 返回索引 idx 位置的数据
v.front(); // 返回容器中的首元素
v.back(); // 返回容器中的最后一个数据
v[idx]; // 类似于数组按下标取值

// 容器互换
v1.swap(v2); // v1与v2容器互换元素
std::vector<int>(v).swap(v); // 先用 v 初始化了一个匿名对象，再将 v 跟匿名对象进行交换，用来收缩内存

// 预留空间
v.reserve(int len); // 容器预留 len 个元素长度，预留位置不初始化，元素不可以访问
```

#### <mark>deque</mark>：双端数组，可以对头端进行插入删除操作；支持随机访问

- vector头部插入、删除效率低

- vector访问元素的速度 deque 快

- deque内部有个<mark>中控器</mark>，维护每一段缓冲区中的内容，缓冲区中存放真是的数据，<mark>中控器维护的是每个缓冲区的地址，</mark>使得使用deque时<mark>像</mark>一片连续的内存空间

- 形参是`const`时，`iterator`也要是`const iterator`

- 赋值方式与vector相同

- insert()与erase()操作也与vector相似

  ```c++
  void test()
  {
  	std::deque<int> d;
  	for (int i = 0; i < 6; i++)
  		d.push_back(i);
  	d.push_front(100);
  	d.pop_back();
  	d.pop_front();
  	for (std::deque<int>::iterator it = d.begin(); it != d.end(); it++)
  		std::cout << *it << std::endl;
  }
  // 
  ```

- deque的排序

  ```c++
  sort(d.begin(), d.end()); // sort算法默认从小到大
  ```

#### <mark>stack</mark>容器：先进后出（栈）

- 不允许遍历
- 只能访问栈顶元素
- <mark>入栈push()，出栈pop()</mark>

```c++
void test()
{
	std::stack<int> s;
	s.push(10);
	s.push(20);
	s.push(30);
	// 判断栈是否为空，空返回 1，不空返回 0
	std::cout << s.empty() << std::endl;
	// s.top()访问栈顶元素，返回栈顶元素
	std::cout << s.top() << std::endl;
	// s.size() 返回栈的大小
	std::cout << s.size() << std::endl;
	while (!s.empty())
		// 删除栈顶元素
		s.pop();
	std::cout << s.empty() << std::endl;
}
```

#### <mark>queue容器：</mark>先进先出（队）

- <mark>队头front()出pop()，队尾back()进push()</mark>
- 不允许遍历

#### <mark>list链表：</mark>物理存储单元非连续的存储结构；链表由一系列的<mark>结点</mark>组成；结点的组成包括了一个<mark>存储数据的数据域</mark>，和<mark>存储下一个结点地址的指针域</mark>；`STL中的链表是一个双向循环链表`

- <mark><font color=red>可以对任意的位置进行快速的插入或者删除操作</font></mark>
- 动态分配内存，不会造成内存浪费和溢出
- 遍历速度没有数组快；占用的空间比数组大
- 链表中的迭代器只支持前移和后移，属于**双向迭代器**

```c++
// 构造方式与 vector 类似
void print_elem(const std::list<int>& l)
{
	for (std::list<int>::const_iterator it = l.begin(); it != l.end(); it++)
		std::cout << *it << " ";
}
void test()
{
	std::list<int> L;
	for (int i = 0; i < 6; i++)
		L.push_back(i);
	print_elem(L);
	// 赋值 assign
	// 插入与删除
	// L.push_back(elem); L.pop_back(); 尾部的插入与删除
	// L.push_front(elem); L.pop_front(); 头部的插入与删除
	// L.insert(pos,elem); 在指定位置插入元素 elem的拷贝，返回新数据的位置
	// L.insert(pos,n,elem); 在 pos位置插入 n个elem数据，无返回值
	// L.insert(pos,begin,end); 在 pos位置插入[begin,end)区间的数据，无返回值
	// L.clear(); 移除容器中的所有数据
	// L.erase(begin,end); 删除[begin,end)区间的数据，返回下一个数据的位置
	// L.erase(pos); 删除pos位置的数据，返回下一个元素的位置
	// L.remove(elem); 删除容器中所有与elem值匹配的元素
	// 
	// 数据的存取
	// L.front(); 返回第一个元素
	// L.back(); 返回最后一个元素
	// L.reverse(); 容器反转
	// L.sort(); 容器排序，从小到大
}
```

```c++
class Person
{
public:
	Person(int age, int high, std::string name) :
		m_age(age), m_high(high), m_name(name)
	{

	}
	int m_age;
	int m_high;
	std::string m_name;
};
// 自定义排序规则
bool myCompare(const Person &p1, const Person &p2)
{
	if (p1.m_age == p2.m_age)
		return p1.m_high > p2.m_high;
	else
	{
		return p1.m_age < p2.m_age;
	}
}
void print_list(const std::list<Person>& L)
{
	for (std::list<Person>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		std::cout << it->m_age << " " << it->m_high << " " << it->m_name << std::endl;
	}
}
void test2()
{
	std::list<Person> L;
	L.push_back(Person(12, 170, "A"));
	L.push_back(Person(10, 173, "B"));
	L.push_back(Person(18, 160, "C"));
	L.push_back(Person(18, 169, "D"));
	L.push_back(Person(66, 180, "E"));
	std::cout << L.size() << std::endl;
	// 需要对sort的排序规则进行自定义，因为list的数据是Person类型
	L.sort(myCompare);
	print_list(L);
}
```

#### <mark>set容器（关联式容器）：</mark>所有元素都会在插入时自动排序

###### set和multiset的区别

- set<mark>不允许</mark>有重复的元素；set插入数据时，<mark>只有insert</mark>的方式，删除数据<mark>erase</mark>
- multiset<mark>允许</mark>有重复的元素

```c++
void test()
{
	std::set<int> s;
	// s.find(key); 查找key是否存在，若存在返回该键的元素的迭代器，若不存在，返回set.end()
	// s.count(key); 统计key的元素的个数，因为set不允许元素重复，所以返回的个数只能是 0 或 1
}
```

- 想要<mark>改变set的排序规则</mark>，需要在<mark>插入数据之前修改</mark>

  ```c++
  // 仿函数
  class MyCompare
  {
  public:
  	bool operator()(int a, int b)
  	{
  		return a > b;
  	}
  		
  };
  void test()
  {
  	// set的排序按照定义的MyCompare规则进行
  	std::set<int, MyCompare> s;
  }
  ```

  

#### <mark>pair对组：</mark>

- 成对出现的数据，利用对组可以返回两个数据

```c++
void test()
{
	// pair的创建
	std::pair<std::string, int> p1("hello", 18);
	std::pair<int, int> p2 = std::make_pair(18, 20);
	// 访问元素
	p1.first; // 第一个元素
	p1.second; // 第二个元素
}
```

#### <mark>map/multimap</mark>：属于关联式容器，底层结构是二叉树实现

- map中<mark>所有的元素都是</mark><font color=red face="微软雅黑">pair</font>

- pair中的第一个元素为key，起到索引作用，第二个元素为value

- 所有元素都会根据元素的键值自动排序

- map不允许有重复的key值出现，multimap允许容器中有重复的key

  ```c++
  // map插入数据
  	std::map<int, int> m;
  	m.insert(std::pair<int, int>(1, 10));
  	m.insert(std::make_pair(2, 20));
  	m.insert(std::map<int, int>::value_type(3, 30));
  	// 删除数据
  	// m.erase(key);按照key删除数据
  	m.erase(m.begin(),m.end());
  	m.clear();
  ```

***

***

***

---

***



## <mark>函数对象</mark>-

> 概念：
>
> - <mark>重载<font color=red>函数调用操作符</font></mark>的<font color=red size=4>类</font>，其<font color=red>对象</font>称为函数对象
> - 函数对象使用重载的<font color=red>()</font>时，行为类似函数调用，也叫<mark>仿函数</mark>
>
> 本质：
>
> - 函数对象（仿函数）是一个类，不是一个函数

- 函数对象在使用时，可以像普通函数那样调用，可以有参数，可以有返回值

- 超出普通函数的概念，函数对象可以有自己的状态

- 函数对象可以作为参数传递

- ```c++
  class MyAdd
  {
  public:
  	int operator()(int a, int b)
  	{
  		return a + b;
  	}
  };
  void test()
  {
  	// 创建函数对象
  	MyAdd myadd;
  	std::cout << myadd(1, 2) << std::endl;
  }
  ```

#### <mark>谓词：</mark>

- 返回bool类型的仿函数称为谓词

- 如果operator()接受一个参数，那么叫做**一元谓词**

  ```c++
  class MyAdd
  {
  public:
  	int operator()(int a, int b)
  	{
  		return a + b;
  	}
  };
  void test()
  {
  	// 创建函数对象
  	MyAdd myadd;
  	std::cout << myadd(1, 2) << std::endl;
  }
  ```

- 如果operator()接受两个参数，那么叫做**二元谓词**

***

***

## <mark>内建函数对象</mark>

- 使用时引入头文件`#include<functional>`

#### 算数仿函数

```c++
void test()
{
	// 创建内建函数对象，negate表示取反
	std::negate<int> n;
	std::cout << n(50) << std::endl;
	// plus表示相加
	std::plus<int> m;
	std::cout << m(10, 20) << std::endl;
	/*
	* minus表示相减
	* multiplies表示相乘
	* divides表示相除法
	* modulus表示取模
	*/
}
```

#### 关系仿函数

```c++
void test()
{
	/*
	* equal_to<>
	* not_equal_to<>
	* greater<>
	* greater_equal<>
	* less<>
	* less_equal<>
	*/
}
```

#### 逻辑仿函数

```c++
void test()
{
	/*
	* logical_or<>
	* logical_and<>
	* logical_not<>
	*/
}
```

***

***

***

## <mark>常用算法</mark>`#include <algorithm>`

#### <mark>常用的遍历算法</mark>

- `for_each`：遍历容器

  ```c++
  // 仿函数
  class print2
  {
  public:
  	void operator()(int a)
  	{
  		std::cout << a << std::endl;
  	}
  };
  void print_value(int val)
  {
  	std::cout << val << std::endl;
  }
  void test()
  {
  	std::vector<int> v;
  	for (int i = 0; i < 6; i++)
  	{
  		v.push_back(i);
  	}
  	std::for_each(v.begin(), v.end(), print_value);
  	std::cout << "==================================" << std::endl;
  	// print2()是一个匿名对象
  	std::for_each(v.begin(), v.end(), print2());
  	
  } `
  ```

- `transform`：搬运容器到另一个容器中，源容器中的数据不变

  ```c++
  class give_value
  {
  public:
  	int operator()(int val)
  	{
  		return val*10;
  	}
  };
  class print_value
  {
  public:
  	void operator()(int val)
  	{
  		std::cout << val << std::endl;
  	}
  };
  void test()
  {
  	std::vector<int> v;
  	for (int i = 0; i < 8; i++)
  	{
  		v.push_back(i+1);
  	}
  	std::vector<int> vTarget;
  	// 给目标容器开辟空间
  	vTarget.resize(v.size());
  	std::transform(v.begin(),v.end(),vTarget.begin(),give_value());
  	std::for_each(vTarget.begin(), vTarget.end(), print_value());
  }
  ```

#### <mark>查找算法：</mark>

- `find`：查找元素；找到第一个匹配的元素；返回的是第一个与要查找的元素匹配的元素在容器中的迭代器

- `find_if`：按条件查找元素

  ```c++
  class MyCompare
  {
  public:
  	bool operator()(int val)
  	{
  		return val > 5;
  	}
  };
  void test()
  {
  	int value = 6;
  	std::vector<int> v;
  	for (int i = 0; i < 8; i++)
  	{
  		v.push_back(i);
  	}
  	std::vector<int>::iterator it = std::find(v.begin(), v.end(), value);
  	if (it == v.end())
  	{
  		std::cout << "没有找到匹配的元素" << std::endl;
  	}
  	else if (it == v.begin())
  	{
  		std::cout << "成功找到了想要查找的元素，且find算法返回了容器的起始位置迭代器" << std::endl;
  	}
  	else
  	{
  		std::vector<int>::iterator that = v.begin();
  		for (int i = 1; i <= value; i++)
  		{
  			that++;
  		}
  		if (it == that)
  		{
  			std::cout << "返回的是第一个与要查找的元素匹配的元素在容器中的迭代器" << std::endl;
  		}
  	}
  	// 返回第一个满足条件的元素的迭代器
  	std::vector<int>::iterator i_t = std::find_if(v.begin(), v.end(), MyCompare());
  	std::cout << *i_t << std::endl;
  }
  ```

  

- `adjacent_find`：查找相邻重复元素，返回相邻元素第一个位置的迭代器

- `binary_search`：二分查找法，查找指定的元素是否存在，如果存在，返回true，否则返回false，`该方法在无序序列中不可以使用，元素的顺序是有序的`

- `count`：统计元素个数，返回`int`数据类型

- `count_if`：按条件统计元素个数

#### <mark>排序算法</mark>

- `sort`：升序排序
- `random_shuffle`：指定范围内的元素随机调整次序`random_shuffle(begin(),end());`
- `merge`：将两个容器的元素进行合并，并存储到另一个容器中`merge(v1.begin(),v1.end(),v2.begin(),v2.end(),v3.begin());`
- `reverse`：反转指定范围的元素`reverse(v.begin(),v.end());`

#### <mark>拷贝和替换算法</mark>

- `copy`：容器指定范围内的元素，拷贝到另一个容器中`copy(v1.begin(),v1.end(),v2.begin());`
- `replace`：将指定范围内的旧元素，替换为新元素`replace(v1.begin(),v1.end(),oldValue,newValue);`
- `replace_if`：将指定范围内满足条件的元素，替换为新元素`replace_if(v1.begin(),v1.end(),谓词,newValue);`
- `swap`：互换两个容器的元素 `swap(v1,v2);`      

#### <mark>算术生成算法</mark>：属于小型算法，头文件`#include <numeric>`

- `accumulate`：计算容器元素累计总和`accumulate(v.begin(),v.end(),value);`，value表示起始的累加值
- `fill `：向容器中指定区间添加元素`fill(v.begin(),v.end(),value);` value表示要填充的元素

#### <mark>集合算法：</mark>

- `set_intersection`：求两个容器的交集，`set_intersection(v1.begin(),v1.end(),v2.begin(),v2.end(),v3.begin());`返回存放交集元素的容器中，`最后一个交集元素位置的迭代器`
- `set_union`：求两个容器的并集，两个容器必须是有序的序列
- `set_difference`：求两个容器的差集，两个容器必须是有序的序列































 

