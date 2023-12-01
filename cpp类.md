# 类

## 一、类的基本知识



- 创建一个类，编译器会默认提供默认构造函数，析构函数，拷贝构造函数
- 如果自己设置了有参构造函数，则编译器不再提供默认构造函数
- <mark>浅拷贝的问题</mark>：堆区的内存被重复释放
- <mark>深拷贝</mark>：重新在堆区申请存储空间
- <mark><font color=red>this指针的本质：</font></mark>是指针常量，指针的指向是不可以修改的；在成员函数后加const修饰的是this指针`const class * const this;`
- 在常函数中可以修改<mark>mutable</mark>修饰的成员
- <mark><font color=red size=5>常对象只能调用常函数</font></mark>

#### 1、假设一个类有一下成员函数

```c++
string isbn() const { return bookNo; }
// 当该类的一个对象调用成员函数 isbn()时， isbn()会有一个隐式的this形参指向调用该函数的对象； 并且该this是一个常量指针。
```

#### 2、构造函数

**每个类都分别定义了它的对象被初始化的方式**，通过``一个或几个``特殊的成员函数来控制其对象的初始化过程。

***构造函数的任务是初始化类对象的数据成员***

- 构造函数的名字和类名相同，***无返回类型***

- 构造函数**不能**被声明成const

- ```c++
  struct Sales_data {
  	Sales_data() = default; //因为该构造函数不接受任何参数，所以他是一个默认构造函数
  	Sales_data(const string &s): bookNo(s){ } // 花括号定义了函数体
  	// 小括号里的内容为构造函数初始值列表
  	Sales_data(const string& s, unsigned n, double p) :
  		bookNo(s), units_sold(n), revenue(p* n) { }
  	Sales_data(istream&);
  	string bookNo;
  	unsigned units_sold = 0;
  	double revenue = 0.0;
  	string isbn() const { return bookNo; } // 常量成员函数
  	Sales_data& combine(const Sales_data&); // 返回类型是类对象类型
  	double avg_price() const;
  
  };
  ```
  
  - <mark>拷贝构造函数</mark>
  
    ```c++
    Person(const Person &p)
    {
        
    }
    Person(10); // 匿名对象调用完成后会被立即释放
    ```
  
    
  
  *** 在类外部定义成员函数： 返回值类型  类名::函数名.....***
  
  - 删除默认构造函数
  
    ```c++
    Log() = delete;
    ```
  
  
  - 类成员初始化
  
    ```c++
    class Student{
        public:
        	Student(int a, std::string b):age(a),name(b){
                
            }
        private:
        	int age;
        	std::string name;
    };
    ```
  
  - 类对象作为类成员
  
    - 先调用类成员的构造函数，再调用该类的构造函数；析构函数的顺序则相反
  
  - 静态成员变量
  
    - 所有的对象共享同一份数据
  
    - 编译阶段就分配内存
  
    - 类内声明，类外初始化(则静态成员变量不可以是私有属性或protected)
  
    - 可以通过类名的方式访问`Student::age;`
  
      ```c++
      class Student{
          public:
          	static int age;
      };
      int Student::age = 10;
      ```
  
  - 静态成员函数
  
    - 只能访问静态的成员变量
  
  - 成员变量和成员函数分开存储
  
  - 每个空对象也应该有一个独一无二的内存地址

#### <mark>this 指针</mark>

- this指针指向被调用成员函数所属的对象

- 解决名称冲突

  ```c++
  class Student
  {
  public:
  	Student(int age) {
  		this->age = age;
  	}
  	int age;
  	Student& addAge(const Student &s)
  	{
  		this->age += s.age;
  		return *this;
  	}
  };
  void func()
  {
  	Student s1(18); // 此时this指向s1;
  	Student s2(20);
      // 此时this指向 s2;
  	s2.addAge(s1).addAge(s1);
  	std::cout << s2.age << std::endl;
  }
  int main()
  {
  	func();
  	return 0;
  }
  ```

  

- 返回对象本身用 <mark>*this</mark>

- 空指针不能访问带有成员属性的成员函数

#### 3、访问控制与封装

可以使用struct和class中的任何一个定义类。**区别**是，struct中定义在第一个访问说明符之前的成员是public的，而class中是private的。

通过***mutable***关键字可以将类的数据成员变***可变数据成员***



#### 4、<mark>const</mark>修饰成员函数

```c++
class Student
{
public:
    // 在成员函数后加const，修饰的是this 指针；让指针指向的值也不可以修改
	void setValue() const 
	{
		m_age = 10; // 当有const时，该行代码报错
        m_name = "张三"; // 正确，因为m_name是mutable修饰的成员
	}
	int m_age;
    mutable std::string m_name;
};
```





## static与extern

### 一、类外的static

###### 在同一个cpp项目中，如果一个cpp文件中有static全局变量，那么在另外一个cpp文件中使用相同的变量名赋值时不会出错



```c++
// 文件 01
static int a = 10;
// 文件 02
int a = 15; // 当输出a时，不会出错

//文件 01
int a = 10;
// 文件 02
extern int a; // 输出a时，会在外部文件01中查找对应的值

//文件 01
static int a = 10;
//文件 02
extern int a; // 报错:因为文件01中的a是static的，外部文件无法看到a，所以使用extern无效
extern int a = 5; //打印a时输出5
```

### 二、类内&结构体内的static

- 静态变量在整个对象实例中共享

- 静态方法不能访问非静态变量

- 非静态方法可以使用静态成员

  ```c++
  #include<iostream>
  struct Enity
  {
  	static int x, y;
  	static void print() {
  		std::cout << x << "," << y << std::endl;
  	}
  		
  };
  int Enity::x;// 使用静态变量的正确方法
  int Enity::y;// 使用静态变量的正确方法
  int main()
  {
  	Enity e; // 使用静态变量的正确方法
  	Enity::x = 6;
  	Enity::y = 10;
  	Enity e2;
  	Enity::x = 10;
  	Enity::y = 20;
  	Enity::print();
  	std::cin.get();
  	
  }
  ```



#### 枚举类型(enum)

```c++
enum Example : char // 指定枚举的类型
{
    A,B,C
};
// Example为枚举类型的名字
```



- public在子类和类外都可以访问
- protected子类可以访问，类外不可以访问
- private子类和类外都不可以访问
- 数组名指向数组第一个元素的地址



### 显示转换与隐式转换

> - 显示转换关键字：<font color=red size=4>explicit</font>
>
> - 当构造函数中不存在显示转换关键字时，允许隐式转换
>
> - ```c++
>   class Enity
>   {
>   private:
>   	std::string m_Name;
>   	int m_Age;
>   public:
>   	Enity(const std::string& name):
>   		m_Name(name),m_Age(-1){}
>   	Enity(int age):
>   		m_Name("Unknow"),m_Age(age){}
>   };
>   void printEnity(const Enity& enity)
>   {
>           
>   }
>           
>   int main()
>   {
>       // printEnity("Tmoas"); //隐式转换失败，因为隐式转换只能转换一次，而此处“Tmoas”默认是const char类型，而非string类型
>       printEnity(std::string("Tmoas"));// 正确
>       printEnity(22); // 可以正常调用函数，因为构造函数的隐式转换
>   	Enity a("Tomas"); // 等同于隐式转换Enity a = "Tomas";
>   	Enity b(22); // 等同于隐式转换 Enity b = 22;
>           
>   	return 0;
>   }
>   ```
>
> - 当构造函数前出现<font color=red size=5>explicit</font>关键字，则禁止使用隐式转换



### **<mark><font color=red size=5>new关键字创建类对象</font></mark>**

- 使用new关键字创建类对象时，实际上做了三件事

  - <mark>获得一块内存空间</mark>
  - <mark>调用构造函数</mark>
  - <mark>返回正确的指针</mark>

- **<mark><font color=green face="楷体">假设有Scop和Entity两个类</font></mark>**

  - ```c++
    Scop entity = new Entity();
    // new Entity();会申请一个Entity实例所需的内存空间，调用Entity类的构造函数，返回指向该地址的指针
    // Scop entity = new Entity();则用了new Entity()返回的指针初始化了Scop类对象，在初始化Scop类对象时，同时调用了Scop类对应的构造函数
    ```

  - 

