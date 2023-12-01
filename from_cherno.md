## 结构化绑定

```c++
std::tuple<std::string, int> CreatePerson("Dav", 10);
// c++17引入的新特性
auto [name, age] = CreatePerson;
std::cout << "name->" << name << ";age->" << age << std::endl;
```

### std::variant

```c++
// 与联合体（union）功能类似，但更安全
std::variant<int, double, std::string> v; // v能存放int、double、string中，任意一种类型的数据
v.index(); // 获取实际存放的数据类型的索引
bool has_int = holid_alternative<int>(v); // 返回一个bool值，判断std::variant中是否存放了int类型的数据
```

### std::any

- 是一种值类型，可以安全的更改对象的类型、

  ```c++
  std::any a; // a is empty
  std::any b = 4.3; // b has value 4.3 of type double
   
  a = 42; // a has value 42 of type int
  b = std::string{"hi"}; // b has value "hi" of type std::string
  // a.type()获取a当前存放的数据的类型
  if (a.type() == typeid(std::string)) 
  {
      std::string s = std::any_cast<std::string>(a);
      useString(s);
  }
  else if (a.type() == typeid(int)) 
  {
      useInt(std::any_cast<int>(a));
  }
  ```

  