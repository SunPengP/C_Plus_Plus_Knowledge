# C++

```c++
# 用g++编译两个cpp文件，并指定可执行的文件名
g++ *.cpp *.cpp -o name
```



### C++的特性

- 抽象
- 封装
- 继承
- 多态

1. C++ 区分大小写

### 数据类型

- bool
- int
- char
- float
- double
- void
- wchar_t : 宽字符型

## 存储类型

- auto：局部变量默认的存储类别，只能用在函数内，只能修饰局部变量
- register
- static
- extern
- mutable

**typedef : 为已有类型定义新的名字（typedef int hello：将hello定义为int类型的另一个名称）**

```c++
enum animals {dog,cat,pig} c;
int f = 3, d = 5;
char x = 'x';
```

**左值(Lvalues)：指向内存位置的表达式被称为左值**

**右值(Rvalues): 指存储在内存位置中某些地址的数值**

**局部变量和全局变量的名称可以相同，但是在函数内，局部变量的值会覆盖全局变量的值；局部变量被定义时，系统不会对其进行初始化，全局变量在定义时，系统会自动初始化**

### 定义常量的两个方式

- #define : ( #define name value )
- const: ( const type name = value)

***goto语句一个很好的作用是退出深嵌套循环***

```c++
#include<iostream>
#include<cmath> // 调用数学函数库
#include<ctime> // 调用系统的时间函数库
// 使用 rand() 生成伪随机数之前，必须先使用 srand()
#include<iomanip>
using std::setw; // setw()函数可以格式化输出
// 例： cout << "element" << setw(13) << "values" << endl; 在element和values之间间隔13个空格
using namespace std;
int sum(int,int);
int main()
{  
    return 0;
}
int sum(int a, int b)
{

}

```

`函数内部的参数称为形式参数`

### 数组

>  数组是一系列连续的内存地址
>
> 数组名是一个指向数组中第一个元素的常量指针   
>
> 如果想要从函数返回一个一维数组，必须声明一个返回指针的函数`int * func(){}`           



### 字符串 

```c++
// C风格
// 字符串实际上是使用null字符终止的一维字符数组
char ge[6] = {'h','e','l','l','o',''} ;
char ge[] = "hello"; 

//C++中的string类
string str1 = "hello";
string str2 = "world";
```

### 指针

**指针是一个变量，其值为另一个变量的地址，即内存位置的直接地址**

> `引用与指针的区别`：
>
> 1. 不存在空引用，引用必须连接到一块合法的内存
> 2. 引用一旦被初始化为一个对象，就不能指向另一个对象
> 3. 引用必须在创建时被初始化；而指针可以在任何时间被初始化

### 结构类型

```c++
struct stract_name{
    stract_变量1;
    stract_变量2;
    ...........;
    stract_变量n;
}; // 可以理解为定义了一个新的包含各种属性的类型
struct stract_name a1; //定义了一个stract变量 a1;
// 结构变量访问结构属性的方式
a1.stract_b变量1；
// 指向结构的指针
struct stract_name *point;
// 结构指针访问结构变量属性
point = &a1;
point -> stract_变量1；
```



####  函数传递参数的方式

1. 传值调用：修改函数内的形式参数的值，对实际参数没有影响
2. 指针调用：将参数的地址赋值给形式参数，则形式参数的变化会影响实际参数
3. 引用调用：该方法把参数的引用复制给形式参数，修改形式参数会影响实际参数



# 类

**默认情况下，类中定义的所有项目都是私有的**

#### 类的构造函数

1. 是类的一种特殊的成员函数，在每次创建类的新对象时执行；与类的名称完全相同，可以用于某些成员变量设置初始值。构造函数中的内容会被先执行。**默认**的构造函数没有参数，如果构造函数有参数，则在创建对象时，需要给对象***赋初始值***。

```c++
#include<iostream>
using namespace std;
class Line
{
    public:
    	void setLength(double len);
    	double getLength(void);
    	Line(double len); // 构造函数(带参数的构造函数)
   		Line(const Line &obj); // 拷贝构造函数
    	~Line(); // 析构函数   	
    private:
    double length;
};
Line::Line(double len)
{
    cout<<"hello"<<len<<endl;
    length = len;
}
// 使用初始化列表来初始化字段
/**
Line::Line( double len): length(len)
{
    cout << "Object is being created, length = " << len << endl;
}
**/
void Line::setLength(double len)
{
    length = len;
}
double Line::getLength(void)
{
    return length;
}
int main()
{
    Line line(9.0); //定义一个类对象;如果构造函数有参数，则需要在创建对象时进行初始化
    line.setLength(6.0);
    cout<<"Length of line:"<<line.getLength()<<endl;
    return 0;
}
```

#### 类的析构函数

1. 在每次删除所创建的对象时执行，不会返回任何值，也不会带任何参数。析构函数在一个对象中最后执行。

#### 拷贝构造函数

1. 复制构造函数总是会存在
2. 拷贝构造函数存在的三种情形：（1）用一个已经初始化的对象去初始化一个新创建的同类对象；（2）如果函数 F 的参数是类 A 的对象，那么当 F 被调用时，类 A 的复制构造函数将被调用。换句话说，作为形参的对象，是用复制构造函数初始化的，而且调用复制构造函数时的参数，就是调用函数时所给的实参；（3）如果函数的返冋值是类 A 的对象，则函数返冋时，类 A 的复制构造函数被调用。

```c++
// 以构造函数部分为例
int main
{
    Line A(9.0);
    Line B = A;
    B.getLength(); //注意这里的对象初始化要调用拷贝构造函数，而非赋值
    return 0;
} // 相同类型的类对象是通过拷贝构造函数来完成整个复制过程的
// 先执行构造函数，再执行拷贝构造函数
```

### 类的友元函数

1. 定义在类外部，但有权访问类的所有成员
2. 友元函数并不是成员函数
3. 友元函数可以是一个函数，称为友元函数；也可以是一个友元类，称为友元类（整个类及其所有成员都是友元）

### 内联函数（inline）

1. 对内联函数进行任何修改，都需要重新编译函数的所有客户端
2. 在类定义中定义的函数都是内敛函数，即使没有使用 **inline** 说明符



## 继承

```c++
#include<iostream>
using namespace std;
// 基类
class Shape
{
    public:
    	void setWith(int w)
        {
            width = w;
        }
    	void setHeight(int h)
        {
            height = h;
        }
    protected:
    	int width;
    	int height;
};
// 派生类：（基类可以被继承为public、private、protected；通常使用public继承）
class Area: public Shape
{
    public:
    	int getArea()
        {
            return (width*height);
        }
};
int main()
{
    Area a1;
    a1.setWidth(5);
    a1.setHeight(7);
    cout<<"area:"<<a1.getArea()<<endl;
    return 0;
}
```

- ***一个子类可以继承多个父类***
- 派生类可以访问基类的所有非私有成员
- 外部类只能访问其他类的公有成员
- `派生类不会继承基类的构造函数、析构函数和拷贝构造函数、重载运算符、友元函数`
- ***公有继承***：基类的公有与保护成员也是派生类的公有与保护成员；基类的私有成员不能直接派生类访问，但可以通过调用基类的**公有**或**保护**成员来访问
- ***保护继承***：基类的公有与保护成员将变成派生类的**保护成员**
- ***私有继承：***基类的**公有**和**保护**成员将成为派生类的**私有**成员



## 重载运算符和重载函数

​	**重载声明**是指一个与之前**已经**在***该作用域***内**声明过**的**函数或方法**具有***相同名称***的声明，但是它们的***参数列表和定义（实现）不相同***

​	***重载的运算符***是带有***特殊名称的函数***，重载运算符有一个**返回类型和参数列表**；**不可重载**的运算符`::` `.` `?:` `.*`

```c++
#include<iostream>
using namespace std;

class Distance
{
    private:
    	int feet;
    	int inches;
    public:
    	// 定义一个无参的构造函数
    	Distance(){
            feet = 0;
            inches = 0;
        }
    	// 定义一个有参的构造函数
    	Distance(int i,int j){
            feet = i;
            inches = j;
        }
    	// 定义一个成员函数方法
    	void displayDistance()
        {
            cout<<"F:"<<feet<<"I"<<inches<<endl;
        }
    	// 重载负运算符
    	Distance operator-()
        {
            feet = -feet;
            inches = -inches;
            return Distance(feet,inches);
        }
};
int main()
{
    Distance D1(11,10),D2(-5,11);
    -D1;
    D1.displayDistance();
    -D2;
    D2.displayDistance();
    return 0;
}
```



## 多态

- 多个不同的类，带有同一个名称，但具有多个不同实现的函数，函数的参数可以相同（即：在子类继承父类时，可以具有与父类相同名称的成员函数）

>**纯虚函数**：`virtual int area()=0;`



## 数据抽象

- **数据抽象是指只向外界提供关键信息，而隐藏其后台的实现细节**

- **数据抽象**是一种依赖于***接口***和***实现***`分离`的设计
- 使用访问标签来定义类的抽象接口，一个类可以包含零个或多个访问标签

### 数据封装

**数据封装是把数据和操作数据的函数绑定在一起**



## 文件读取与写入：(fstream)

- ofstream: 输出文件流，用于创建文件并向文件***写入信息***
- ifstream: 输入文件流，用于从文件读取信息

```
void open(const char *filename, ios::openmode mode);在这里，open()成员函数的第一参数指定要打开的文件的名称和位置，第二个参数定义文件被打开的模式。
```

- ios::app`追加模式，所有写入都追加到文件末尾`
- ios::ate`文件打开后定位到文件末尾`
- ios::in`读取`
- ios::out`写入`



# 动态内存

c++中的内存分为两部分（1）**栈**：在函数内部声明的所有变量都将占用栈内存；（2）**堆**：这是程序中未使用的内存，在程序运行时可用于动态分配内存

```c++
double* pvalue = NULL; // 声明一个double类型的指针，并初始化为NULL；声明指针时，最好进行初始化
pvalue = new double; // 为指针变量请求内存；new不仅分配了内存，还创建了对象
    
// 当动态分配内存的变量不再需要使用时，可以使用delete操作符释放它所占用的内存
delete pvalue;
```

##### 数组的动态内存分配

```c++
char* pvalue = NULL;
pvalue = new char[20]; // 为变量请求内存
delete [] pvalue; // 删除为数组分配的内存

// 为多维数组分配内存：先分配行，在分配列
int ROW = 2;
int COL = 3;
double **pvalue = new double* [ROW]; // 为行分配内存
for(int i=0;i<COL;i++){
    pvalue[i] = new double[COL];
} // 为列分配内存
// 释放多维数组的内存
for(int i=0;i<COL;i++){
    delete[] pvalue[i];
}
delete [] pvalue;
```

##### 对象的动态内存分配

```c++
class Box
{
    public:
    	Box(){
            cout << "调用构造函数" << endl;
        }
    	~Box(){
            cout << "调用析构函数" << endl;
        }
};
int main()
{
    Box* pvalue = new Box[4];
    delete [] pvalue;
    return 0;
}
```

### 命名空间

- 可以作为附加信息来区分不同库中相同名称的函数、类、变量等

- 本质上，命名空间就是定义了一个**范围**

- ```c++
  namespace first_space{
      void fun(){
          cout<<"hello world"<<endl;
      }
  }
  namespace second_space{
      void fun(){
          cout<<"Ni Hao"<<endl;
      }
  }
  // 使用命名空间中的函数（类、变量）的第一种方法
  int main()
  {
      // 根据命名空间调用函数的规则：namespace::名称
      first_space::fun();
      second_space::fun();
      return 0;
  }
  // 第二种方法
  using namespace first_space;
  int main()
  {
      fun(); // 由于在在int main()之前已经指定了命名空间，所以此处直接调用函数
      return 0;
  }
  ```



### 模板

**模板是建立一个通用函数或类，其类内部的类型和函数的形参类型不具体指定，用一个虚拟的类型来代表**。`凡是函数体相同的函数，都可以用这个模板来代替，不必定义多个函数。在调用函数时，系统会根据实参类型来取代模板中的虚拟类型`

```C++
// 函数模板由以下三部分组成：模板说明+函数定义+函数模板调用
template <typename T>
T compare_max(T a, T b){
    return a > b ? a : b;
} // 定义一个两数比较大小的模板，但没有定义用于比较大小的两个数据的类型，在使用时，编译器会实现参数的自动推导
```

- 当普通函数与模板函数并存时（相同类型），会选择调用普通函数，如果非要用模板函数，可以在调用的时候在函数名后加`<>`符号
- **如果有函数模板和普通函数的时候，普通函数的参数类型不不一致的时候，也会调用普通函数，因为会有隐式的转换，但是如果有函数模板的时候，函数模板会产生更好的匹配，使用函数模板。**

># 函数模板和普通函数在一起，调用规则
>
>1 函数模板可以像普通函数一样被重载
>2 C++编译器优先考虑普通函数
>3 如果函数模板可以产生一个更好的匹配，那么选择模板
>4 可以通过空模板实参列表的语法限定编译器只通过模板匹配
