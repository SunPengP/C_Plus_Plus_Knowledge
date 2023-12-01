# C++

> <mark>vector<T> size_type</mark>，其中size_type是一种类型，确保能够保存可能存在的最大可变数组中的所有元素

<mark>new 关键字指向分配的内存的指针</mark>

>- int: 一个整数是四个字节，一个字节是8个比特，那么一个整数就是32个字节
>- char: 一个字节的数据
>- short： 两个字节的数据
>- long long : 八个字节的数据
>- float: 四个字节的数据（使用float数据时，如果不在数值后加‘F’或者'f'，编译软件会自动识别为double类型）
>- double: 八个字节的数据
>- bool：一个字节(byte)的数据（实际上bool类型的数据只占用一个bit的存储，但是由于在寻址内存时，无法查找只有一个bit的数据，所以给bool类型的数据分配一个字节的内存，一个字节(byte)的内存可以存储8个bool类型的数据）

> 括号是直接初始化； “=”是拷贝初始化
>
> 全局变量、静态变量、字符串常量存储在全局区中



> 空指针定义为  `const char* ptr = nullptr;`
>
> 数组名指向数组首元素的地址；数组就是<mark>内存块</mark>，处理内存的简单方法是使用指针
>
> 用new创建的数据存储在**堆**上，需要用delete删除
>
> ```c++
> int* example = new int[5]; //int类型的大小为5的数组，名字为example
> delete[] example; // 删除为数组example，释放分配的内存
> ```





##### 字符串就是字符数组

```c++
#include<string> // 在标准库中调用string
#include<stdlib.h>
std::string name1 = "Cherno";
name1.find("no"); // 查找字符所在位置
name1.size(); // 字符串大小
// 字符串相加
name1 += "Hello";
std::string name1 = std::string("cherno") + "hello";
 
const char* name = "Google";
const wchar_t* name = L"Hello";
const char16_t* name = u"Hello";
const char32_t* name = U"hello";
strlen(name); // 用 const char* 定义的字符串查看长度的方式
char name[7] = {'G','o','o','g','l','e'.'\0'};
```

### string与const char*

- <mark>string是类类型，可以使用函数string.size()来判断字符串的大小，但const char* 不可以使用size()函数；  string与const char*都可以使用下标索引的方式获取字符串中的元素</mark>

```c++
// string转换成const char*
// string.length(); 
// string.data(); 获取字符串的内容
#include <string>
char _c[] = "hello world";
std::string s = "abc";
// 将 string类型的字符串转换为const char* 使用c_str()函数将string转换为c风格的字符串
const char* c_s = s.c_str();
// const char*转string
const char* c_s = "abc";
std::string s(c_s); // 直接赋值（此处使用的是拷贝赋值）
```



### const指针

```c++
// const指针可以改变指向的地址，但不能改变指向的内容
const int* a = new int;

// const指针可以改变指向的内容，但不能改变指向的地址
int* const a = new int;
```

###### 将类成员标记为mutable，表示类中的const方法可以改变这个成员

#### c++宏常量`#define Day 7`

数据类型存在的意义：给变量分配合适的内存空间

sizeof获得变量占用的内存大小

字符型变量用<mark>单引号</mark>

当做<mark>值传递</mark>时，函数的形参发生改变，并不会影响函数的实参

#### goto语句

```c++
std::cout<<"1";
std::cout<<"2";
goto FLAG; // goto语句会执行给定的标记后的程序
std::cout<<"3";
FLAG:
std::cout<<"标记"；
```



#### 使用标准库创建数组：

```c++
#include <array>
std::array<int,5> example;
std::cout<<example.size()<<std::endl; // 得到数组的大小
```



```c++
// endl 在每行最后插入换行符
// sizeof() 函数用来获取各种数据类型的大小: sizeof(int)

typedef type newname; // 为已有类型设置一个新名字

typedef int N;
N n = 10; // n表示的是int类型的数据，值为10
```

```c++
enum color{
    blue,
    red,
    black
}c; // 默认情况下，第一个名称的值为 0，第二个名称的值为 1，第三个名称的值为 2
// 也可以给名称赋予一个初始值
enum color{
    blue,
    red=5,
    black
}c; // 此时blue的值为0，red的值为5，black的值为6
c = blue; 

// 变量声明
extern int a, b;
extern int c;
extern float f; // 可以多次声明一个变量，但是变量只能在某个文件、函数或代码中被定义一次 
```



```c++
using namespace std;//可以放在int main()之前，也可以放在之后
int a;
int b;
int c;
a = b = c = 25;//C++可以连续使用赋值运算符
```

- 一个函数，由函数头和函数体组成
- const对象一旦被创建后，其值不能被改变



**在函数体内部不能初始化一个由extern关键字标记的变量，否则会引发错误**



##### 关于字符串的函数

**字符串是由常量字符构成的数组**

```C++
#include <iostream>
#include <cstring>
char a[] = "hello,world";
cout<<strlen(a)<<endl; // 输出字符串的长度，不包括结束符
cout<<sizeof(a)<<endl; // 输出字符串的长度，包括结束符

```

##### 每次读取一行字符串输入

```C++
cin.getline(name,size);// name:数组名； size：数组大小
cin.getline(name,size).getline(name,size);

// 如果使用cin.get()
// 如果连续使用cin.get(name,size)，cin.get只能获得第一次的结果
// 如果想像cin.getline(name,size)那样，则可以按如下方式：
										// cin.get(name,size);
										// cin.get();
										// cin.get(name,size);
  										// 或者：cin.get(name,size).get();
// getline()使用起来简单，但是get()检查错误更方便
```

##### 空行问题

```C++
int year;
cin >> year;
char name[20];
cin.getline(name, 20); 
// 用户没有机会输入name，因为cin 读取完year后，将回车符生成的换行符留在了输入队列，cin.getline()看到换行符之后，认为是一个空行，将空行赋值给了name

// 解决方法
cin >> year;
cin.get(); 
cin.getline(name,20); // 或者 (cin >> year).get(); 或者(cin >> year).get(ch);
```



> 不能将一个数组赋值给另一个数组，但可以将一个string对象赋值给另一个string 对象。



##### 字符串拼接

```C++
string str1 = "hello";
string str2 = " world";
string str3 = str1+str2; // str1 += str2;
// 输出：hello world

// 确定字符串中字符数的方法
str1.size()
strlen(str1)
```

##### 读取一行string对象到代码中

```C++
# include<string>
string str1;
getline(cin,str1);
```

##### 类的成员函数：是指把定义和原型写在类定义内部的函数；成员函数可以定义在类定义内部，或者单独使用范围解析运算符`::`来定义，在类定义中定义的成员函数把函数声明为内联的；成员函数内部可以调用该类的成员变量

```c++
double Box::getVolume(void)
{
    return length*height*breadth;
} // 如果单独使用范围解析运算符定义成员函数，则必须在::运算符之前使用类名
```

##### 类访问修饰符

1. public、private、protected称为访问说明符

> public: 公有成员变量或函数在类外部可以访问 
>
> private:私有成员变量或函数在类外部不可被访问
>
> protected: 在派生类中可以访问
>
> .  : “.”运算符只能用于类类型的对象



## 引用与指针

##### 引用与指针都是符合类型；指针是对象，而常量不是

#### 引用：

>- 引用必须初始化；
>- 必须是一个对象，不能是数值；
>- 引用一旦定义，只能绑定其一开始绑定的对象，无法更改
>- 所谓引用只是给对象一个别名

#### 指针

>- 引用不是对象，没有实际的地址，所以不能定义指向引用的指针
>- 指针的值是地址



##### 常量表达式

>- 一个对象（或表达式）是不是常量表达式，由它的数据类型和初始值共同决定
>- constexper把它所定义的对象置为了顶层const

##### auto

>- auto让编译器通过初始值来推算变量的类型；
>- auto定义的变量必须要有初始化
>- 不能为非常量引用绑定字面值

#### 标准类型String

>- 直接初始化与拷贝初始化
>
>  ```python
>  #include<string>
>  using namespace std::string
>  int main(){
>      string s1 = 'hello world'; //拷贝初始化
>      string s2("good luck"); //直接初始化
>  }
>  ```
>
>- getline()：按行读取字符串，包括空白符；

#### 标准库类型vector

> 1. `列表初始化vector对象`
>
>    ```python
>    #include <vector>
>    #include <string>
>    using namespace std::vector;
>    using namespace std::string;
>    {
>        vector<string> articles = {"a", "an", "the"};
>    }
>    ```

#### 迭代器

###### `如果容器为空，则begin和end返回的是通过一个迭代器，都是尾后迭代器``

> - 但凡使用了迭代器的循环体，都不要向迭代器所属的容器添加元素



### 数组

>- 在使用数组下标时，通常将其定义为**size_t**类型
>- 不允许拷贝数组；使用数组时，会将其转换成指针



###### 成员访问运算符

>- “  . ” 运算符与“ ->”运算符代表成员访问运算符
>
>  ```python
>  ptr -> mem 等价于 （*ptr）.mem
>  ```



## 函数

1. 函数形参分别为**指针**与**引用**时：

   ```python
   -> 形参为指针时，实参需传入地址 
   
   -> 形参为引用时，实参传入对应的变量即可
   
   ```

2. 当某种类型不支持拷贝时，函数只能通过引用形参访问该类型对象

```c++
// i 此时是顶层const，只能读取i，不能改变i的值
const int i = 5 ;
```

3. 如果函数的实参数量未知，但是全部实参的类型相同，则可以使用**initializer_list**类型的形参

   ```c++
   initializer_list<T> lst; // 默认初始化，T类型元素的空列表
   initializer_list<T> lst{a,b,c,...}; // lst的元素数量和初始值一样多，lst的元素是对应初始值的副本，列表中的元素是const
   lst2(lst); // lst2 = lst ; 拷贝或赋值一个initializer_list对象不会拷贝列表中的元素；拷贝后，原始列表和副本共享元素
   lst.size(); // 列表中元素的数量
   lst.begin(); // 返回指向lst中首元素的指针
   lst.end(); // 返回指向lst中尾元素下一位置的指针
   ```

   - initializer_list中的元素永远是常量值，不可以改变



## 函数重载

- 函数重载时，不允许除了返回类型外，其他所有成分都相同



#### IO

- IO对象无拷贝或赋值



#### 头文件

> 如果源文件中有多个cpp文件，其中一个cpp文件定义了一个函数，如果另一个文件想要调用该函数，就需要对该函数先进行声明再调用；
>
> `也可以在头文件中对该函数进行声明，然后在该文件中直接include头文件就可以直接调用`
>
> 头文件中的`#pragma once`用来监督头文件，避免头文件在被链式调用时，重复创建而出错



#### 指针

- 指针是一个整数，用来存储内存地址的数字、

- 空指针定义为  `const char* ptr = nullptr或者是NULL;`

- 指针&引用

  ```c++
  int a = 5;
  int* ptr_a = &a; //指针
  int& ref_a = a; //引用
  ```




### std::array

- ```c++
  #include <array>
  std::array<int, 5> data;
  ```

- 



#### 函数指针

```c++
// 假设有函数“HelloWorld”
// 可以通过auto将函数的地址赋值给变量
auto a = HelloWorld; // auto a = &HelloWorld;

#include <iostream>

void HelloWorld(int a)
{
	std::cout << "hello world"<< a << std::endl;
}

int main()
{
    // 指向对应类型函数的指针
	typedef void(*HelloWorldFunction)(int);
	HelloWorldFunction function = HelloWorld;
	function(8);

	std::cin.get();
}
```

```c++
#include <iostream>
#include <vector>

// 打印函数
void PrintValue(int value)
{
	std::cout << "value:" << value << std::endl;
}
// 打印每个值的函数
// 参数值包含了函数指针
void ForEach(const std::vector<int>& values, void(*Func)(int))
{
	for (int value : values)
		Func(value);
}
int main()
{
	std::vector<int> values = { 1,2,3,4,5 };
    // 传参时，根据对应的指针类型传入符合要求的函数地址
	ForEach(values, PrintValue);
	std::cin.get();

}
```



### 多维数组

```c++
#include <iostream>

int main()
{
	int* array = new int[50]; // 只是在分配内存
	int** a2d = new int*[50]; // a2d是指向整型指针的指针
	for (int i = 0; i < 50; i++)
		// a2d[i]代表第i个指针指向的一维数组
		// 数组中的每个位置都存储在 a2d[i]中
		a2d[i] = new int[50];

	std::cin.get();
}
```

### 排序

```c++
#include <iostream>
#include <algorithm> // 因为调用了 sort()
#include <vector>
#include <functional> // 因为调用了 greater<int>()/less<int>()
int main()
{
	std::vector<int> values = { 3,4,1,2,6,5,7 };
	// 如果只传入需要排序的内容的起始位置，则默认从小到大排序
	std::sort(values.begin(), values.end());
    // 从大到小排序
    std::sort(values.begin(), values.end(),std::greater<int>());
    
    // 用false与true来控制排序的顺序，根据传入的lambda表达式的int a 与 int b，如果根据指定的判断返回的是false，则将前面的值后移，后面的值前移；如果返回的是 true，则保留对应的顺序
    std::sort(values.begin(), values.end(), [](int a, int b) {
		if (a == 1)
			return false;
		if (b == 1)
			return true;
		return a < b;
		
		});
    
    // 从小到大排序
    std::sort(values.begin(), values.end(),std::less<int>());
	for (int value : values)
		std::cout << value << std::endl;

	std::cin.get();
}
```

### union

> union的所有成员共享同一个内存位置，其内存大小始终是足以存储最大成员的内存



#### 强制类型转换

`强制类型转换运算符<要转换到的类型>（待转换的表达式）;`

- static_cast：
  - 不能用于存在不同指针类型之间的转换
  - 不能用于整型和指针之间的转换
  - 不能用于不同类型的引用之间的转换
- dynamic_cast
  - 虚基类可以使用(或抽象类)可以使用dynamic_cast
  - 实现虚基类到派生类的强制转换
  - 派生类到虚基类的转换不管使不使用dynamic_cast都可以
  - 只能用于含有虚函数的类

- reinterpret_cast
  - 不同类型的指针之间
  - 不同类型的引用之间
- const_cast
  - 用于去除const属性的转换



### std::tuple

- tuple不支持迭代访问，只能通过<mark>索引</mark>或<mark>tie</mark>解包（讲元组中的每一个元素提取到指定变量中）

```c++
#include <string>
#include <tuple>
int f_1 = 10;
// 引用
int& a = f_1; // a是f_1别名
int sec_2 = 10;
// tuple初始化
std::tuple<std::string, int> name("hello",10);
// tuple 初始化
std::tuple<int, int> second = std::make_tuple(f_1,sec_2);
std::tuple<int, int> first(10,30);
// 对tuple进行索引
auto a = std::get<0>(first);
// 获取元组中某个元素的数据类型 std::tuple_element<index,tuple> index代表元组中元素的索引，tuple代表哪个元组; decltype自动推导变量的类型
std::tuple_element<index,decltype<tuple>>::type vairl;
// std::tie用来对元组进行解包，讲元组的元素赋值给对应的变量类型
std::tuple<std::string,int> third("hello",30);
std::string s("");
int a = 0;
std::tie(s,a) = thrid;
// std::tuple_cat() 讲两个元组进行拼接
```

### 函数的分文件编写

- 在<mark>.h</mark>头文件中写<mark>函数的声明</mark>
- 在<mark>.cpp</mark>源文件中写<mark>函数的定义</mark>



### <mark>const</mark>修饰指针

- <mark>常量指针：</mark>

  - ```c++
    const int* p = &a; // 常量指针
    ```

  - 指针指向的地址可以修改

  - 指针指向的<mark>值<font color=red>不可以</font></mark>修改

- <mark>指针常量：</mark>

  - ```c++
    int * const p = &a;
    ```

  - 指针的<mark>指向不可以修改</mark>，但是指针指向的值可以修改

- const既修饰指针，又修饰常量：

  - ```c++
    const int * const p = &a;
    ```

  - 指针的指向以及值<mark><font color=red>都不可以修改</font></mark>

###### 结构体数组

```c++
struct Student
{
  std::string name;
  int age;
};
Student s1[3] = {{...},{...},{...}}
s1[1].name;
```

##### 结构体指针

- 通过指针访问结构体中的成员

- 利用操作符`->`可以通过结构体指针访问结构体的属性

- ```c++
  struct Student* p = &s1;
  p->name; // 指针访问结构体属性
  ```



***

***

***

### 文件操作

##### 写文件操作步骤

- #include <fstream>
- 创建流对象： ofstream ofs;
- 打开文件： ofs.open("文件路径", 打开方式);
- 写数据： ofs<<"写入的数据";
- 关闭文件：ofs.close();

##### 读文件

- #include <fstream>

- 创建流对象： ifstream ifs;

- 打开文件： ifs.open("文件路径", 打开方式);

- ifs.is_open(); 判断文件是否成功打开，若成功打开，则返回true

- 读数据： 

  - ```c++
    char buf[1024] = {0};
    while(ifs >> buf)
    {
        std::cout << buf << std::end;
    }
    
    while(ifs.getline(buf,sizeof(buf))) //按行读取文件中的数据，读入到buf中
    {
        std::cout << buf << std::endl;
    }
    
    std::string buf;
    while(getline(ifs,buf))
    {
        std::cout << buf << std::endl;
    }
    
    char c;
    // EOF：end of file
    while((c=ifs.get())!=EOF)
    {
        std::cout << c << std::endl;
    }
    ```

  - 

- 关闭文件：ifs.close();

###### 二进制写文件

- 包含头文件

- 创建流对象`ofstream ofs("文件路径"，ios::out | ios::binary);` 

- ```c++
  Person p={"zhang san",18};
  ofs.write((const char*)&p, sizeof(Person));
  ```

- ofs.close();

##### 二进制读文件

- 包含头文件
- 创建流对象：`ifstream ifs`
- `ifs.open("文件路径", ios::in | ios::binary)`
- ifs.is_open();
- ifs.read((char*)&p, sizeof(Person));



### 类模板

```python
#include <iostream>

template<class NameType, class AgeType>
class Person
{
public:
	Person(NameType name, AgeType age) {
		this->name = name;
		this->age = age;
	}
	AgeType age;
	NameType name;
	void print_info()
	{
		std::cout << this->name << this->age << std::endl;
	}
};
void test()
{
	// <std::string, int>表示模板参数列表，分别传给NameType和AgeType
	// ( )中的内容传递给name, age参数
	Person<std::string, int> p1("张三",16);
	p1.print_info();
}
int main()
{
	test();
	return 0;
}
```

- <font color=red>只有</font>类模板中可以有默认参数

- 类模板无法使用自动类型推导

  ```c++
  // Person p1("张三",16); 错误，类模板无法自动推导类型
  Person<std::string, int> p1("张三",16);
  ```

- <mark>普通类的成员函数一开始就创建</mark>

- <mark>类模板的成员函数，在调用时才会创建</mark>

###### 类模板对象做函数参数

- 指定参数类型

  ```c++
  void test(Person<std::string, int>& p)
  {
  	
  }
  ```

- 参数模板化

  ```c++
  template<class NameType, class AgeType>
  void test(Person<NameType,AgeType>& p)
  {
  	
  }
  ```

- 整个类模板化 

  ```c++
  template<class T>
  void test(T &p)
  {
  	
  }
  ```

###### 类模板与继承

- 当子类继承的父类是类模板时，子类在声明时，需要指出父类中T的类型

  ```c++
  template<class T>
  class Base
  {
  	T m;
  };
  class Son :public Base<int> // 指定出父类中的T类型
  {
  
  };
  ```

- 如果不指定，编译器无法给子类分配内存

- 如果想灵活指定出父类中的T类型，子类也需要变为模板类

  ```c++
  template<class T>
  class Base
  {
  	T m;
  };
  template<class T1, class T2>
  class Son :public Base<T1> // 指定出父类中的T类型
  {
  public:
  	T2 n;
      // 获得 T1 的类型
  	std::cout << typeid(T1).name() << std::endl;
  };
  ```

- 类模板成员函数的类外实现

  ```c++
  Son<T1,T2>::Son(T1 name, T2 age)
  {
  	this->name = name;
  	this->age = age;
  }
  ```

###### 类模板分文件编写

<mark>解决的问题：</mark>类模板中的成员函数，在调用时才被创建，导致份文件编写时链接不到

<mark><font color=red>解决：</font></mark>

1. 直接包含<mark>.cpp</mark>文件
2. 将声明和实现写在同一个文件中，并更改后缀名为<mark>.hpp</mark>
