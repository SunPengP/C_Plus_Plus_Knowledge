# Thread

- 

- ```c++
  
  
  ```
  
- ```c++
  #include <functional> // std::mem_fn
  #include <algorithm> // std::for_each; //相当于是for循环
  struct Foo
  {
    void print_hello(){
        std::cout<<"hello"<<std::endl;
    }
    void print_world(){
        std::cout<<"world"<<std::endl;
    }
    int data = 7;
  };
  int main()
  {
      Foo f; // 创建一个结构体实例
      // std::men_fn相当于定义了访问的成员
      auto p_hello = std::mem_fn(&Foo::print_hello);
      p_hello(&f);
      auto p_world = std::mem_fn(&Foo::print_world);
      p_world(&f);
      auto access_data = std::mem_fn(&Foo::data);
      access_data(&f);
  }
  ```

- 

```c++


```

```c++


```

#### 等待线程结束的两种方式

1. 

## 多线程

- 基于进程：基于进程的多任务处理是程序的并发执行
- 基于线程：基于线程的多任务处理是同一程序的片段的并发执行

每个应用程序至少有一个进程，每个进程至少有一个主线程(以main函数作为入口函数的线程)，除了主线程外，在一个进程中可以创建多个线程。

### std::async 

(异步接口)

- 会自动创建一个线程去调用线程函数，并返回std::future，std::future中保存了线程函数返回的结果

- 可以通过<mark>查询</mark><font color=red>std::future</font>的<mark>状态</mark>来获取异步操作的结果，future有<mark>三种</mark>状态：

  - <mark>deferred</mark>: 异步操作还没开始
  - <mark>ready</mark>: 异步操作已经完成
  - <mark>timeout</mark>: 异步操作超时

- <font color=red>std::promise</font>: 为获取线程函数中某个值提供便利，在线程函数中，给外面传进来的promise赋值，当线程函数执行完成后，可以通过promise获取该值，取值是间接通过promise内部提供的future来获取的

  ```c++
  std::promise<int> pr; // <int>表示promise保存的值的类型
  std::thread t([](std::promise<int>& p){ p.set_value_at_thread_exit(9); },std::ref(pr));
  // get_future返回一个std::future
  std::future<int> f = pr.get_future();
  // future.get() 来获取具体的值
  auto r = f.get();
  ```

- <font color=red>std::packaged_task</font>: 与promise有点类似，不过保存的是函数

  ```c++
  std::packaged_task<int()> task([](){ return 7; });
  std::thread t1(std::ref(task)); 
  std::future<int> f1 = task.get_future(); 
  auto r1 = f1.get();
  ```

- <mark>std::async</mark>:

  - 两种创建方式
    - `std::launch::async`(调用async就开始创建线程)
    - `std::launch::deferred`(延迟加载方式创建线程)

