# rust  os dialy

## 7/5

---

今天才报名参加2022年关于rust开发操作系统的夏令营活动，期待这新的旅程希望带来不一样的经历。



## 7/6

---

才搞明白夏令营的要做哪些事情，==！ 由于工作原因我只能抽出一小段时间来完成相应任务，这种久违的时间紧迫感，让人感到亲切。今天熟悉了活动流程，开始学习rust，rust的性能非常吸人之外，就是它的cargo包管理，包管理真的太重要了，之前python就遇到各种关于包的问题，如果没有包项目将很难管理。

## 7/7

---

rustlings 真是个不错的练习小工具，今天提交了varialbes的练习，白天工作太忙了，真的是只有在学校学生时期才有充足的时间来专注学习，诸君珍惜

## 7/8

---

rustlings 安装是遇到的错误

Q: `运行rustlings cargo install 时提示please ensure that VS 2013, VS 2015, VS 2017 or VS 2019 was installed with the Visual C++ option`

A: ```c

1. rustup uninstall toolchain stable-x86_64-pc-windows-msvc

2. rustup toolchain install stable-x86_64-pc-windows-gnu

3. rustup default stable-x86_64-pc-windows-gnu

\```

- 语句和表达式

  表达式结尾没有分号，通常要返回结果；语句有分号结束。rust函数中居然不用return 使用表达式直接返回结果，==！神奇。

- 函数

  函数没啥好说的，rust函数无值返回时，隐式返回（），这玩意儿也是个表达式！？

## 7/9

---

- 判断与流程控制

  rust 使用的关键字if、for、while、loop、continue、break。案例中if、loop可以作表达式返回值。

  break居然可以带返回值！~

  | `for item in collection`      | `for item in IntoIterator::into_iter(collection)` | 转移所有权 |
  | ----------------------------- | ------------------------------------------------- | ---------- |
  | `for item in &collection`     | `for item in collection.iter()`                   | 不可变借用 |
  | `for item in &mut collection` | `for item in collection.iter_mut()`               | 可变借用   |

- 所有权、引用与借用

  rust中全新的概念，实现基础依然是靠栈和堆（毕竟是在现有计算架构体系下），

  - 所有权

    - 背景

      栈数据往往可以直接存储在 CPU 高速缓存中，而堆数据只能存储在内存中。访问堆上的数据比访问栈上的数据慢，因为必须先访问栈再通过栈上的指针来访问内存。数据在堆中分配的数据，没有及时释放，导致泄漏无法收回，造成内存不安全。

    - 所有权内容

    1. Rust 中每一个值都被一个变量所拥有，该变量被称为值的所有者

    2. 一个值同时只能被一个变量所拥有，或者说一个值只能拥有一个所有者

    3. 当所有者(变量)离开作用域范围时，这个值将被丢弃(drop)

  - 引用与借用

    - 背景

      总是把一个值传来传去来使用它，如果仅仅支持通过转移所有权的方式获取一个值，那会让程序变得复杂。 

      使用某变量的指针或引用，这获取变量的引用，称之为借用(borrowing)

    - 引用与借用内容

      - 不可变引用

        `&`类型的引用，因此它指向的数据无法进行修改。

      - 可变引用

        mut s ，同一作用域，特定数据只能有一个可变引用。

        > 使 Rust 在编译期就避免数据竞争，数据竞争可由以下行为造成：
        >
        > - 两个或更多的指针同时访问同一数据
        >
        > - 至少有一个指针被用来写入数据
        >
        > - 没有同步数据访问的机制

    - 总结
      - 同一时刻，你只能拥有要么一个可变引用, 要么任意多个不可变引用
      - 引用必须总是有效的

- 复合数据类型

  - 字符串与切片

    ```rust
    //Rust 中的字符是 Unicode 类型，因此每个字符占据 4 个字节内存空间，但是在字符串中不一样，字符串是 UTF-8 编码，也就是字符串中的字符所占的字节数是变化的(1 - 4)当 Rust 用户提到字符串时，往往指的就是 String 类型和 &str 字符串切片类型，这两个类型都是 UTF-8 编码。
    let s = String::from("hello");
    let slice = &s[0..2];
    let slice = &s[..2];
    ```

  - 元组

    ```rust
    //元组是由多种类型组合到一起形成的，因此它是复合类型，元组的长度是固定的，元组中元素的顺序也是固定的。
    let s1 = String::from("hello");
    let (s2, len) = calculate_length(s1);
    ```

  - 结构体

    ```rust
    //结构体
    struct User {
        active: bool,
        username: String,
        email: String,
        sign_in_count: u64,
    }
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };
    //元组结构体
        struct Color(i32, i32, i32);
        let black = Color(0, 0, 0);
    //单元结构体
    struct AlwaysEqual;
    let subject = AlwaysEqual;// 我们不关心 AlwaysEqual 的字段数据，只关心它的行为，因此将它声明为单元结构体，然后再为它实现某个特征
    impl SomeTrait for AlwaysEqual {
    }
    
    //User 结构体从其它对象借用数据，不过这么做，就需要引入生命周期(lifetimes)这个新概念（也是一个复杂的概念），简而言之，生命周期能确保结构体的作用范围要比它所借用的数据的作用范围要小。
    
    ```

  - 枚举

    ```rust
    //枚举类型是一个类型，它会包含所有可能的枚举成员, 而枚举值是该类型中的具体某个成员的实例。
    enum PokerSuit {
      Clubs,  //成员是什么类型？？ 下面解释了类似单元结构体 O.O!
      Spades,
      Diamonds,
      Hearts,
    }
    let heart = PokerSuit::Hearts;
    //任何类型的数据都可以放入枚举成员中: 例如字符串、数值、结构体甚至另一个枚举。
    enum Message {
        Quit,
        Move { x: i32, y: i32 },
        Write(String),
        ChangeColor(i32, i32, i32),
    }
    fn main() {
        let m1 = Message::Quit;
        let m2 = Message::Move{x:1,y:1};
        let m3 = Message::ChangeColor(255,255,0);
    }
    //以上可以用结构体方式定义
    struct QuitMessage; // 单元结构体
    struct MoveMessage {
        x: i32,
        y: i32,
    }
    struct WriteMessage(String); // 元组结构体
    struct ChangeColorMessage(i32, i32, i32); // 元组结构体
    
    //Option处理空值
    //null 代表没有值，不是默认值，null会引发很多问题，rust中弃用，使用Option枚举代替，来限制空值的泛滥。
    enum Option<T> {
        Some(T),
        None,
    }
    ```

  - 数组

    ```rust
    //数组有两种，第一种是速度很快但是长度固定的 array，第二种是可动态增长的但是有性能损耗的 Vector
    let a:[i32;5] = [9, 8, 7, 6, 5];
    let first = a[0]; // 获取a数组第一个元素
    // arrays是一个二维数组，其中每一个元素都是一个数组，元素类型是[u8; 3]
    let arrays: [[u8; 3]; 4]  = [one, two, blank1, blank2];
    //数组切片
    let slice: &[i32] = &a[1..3];
    ```



- 模式匹配
  - match 和if let

    ```rust
    match target {
        模式1 => 表达式1,
        模式2 => {
            语句1;
            语句2;
            表达式2
        },
        _ => 表达式3
    }
    // _ => (),  _ 将会匹配所有遗漏的值。() 表示返回单元类型与所有分支返回值的类型相同
    
    //if let
    //当你只要匹配一个条件，且忽略其他条件时就用 if let ，否则都用 match。
    if let Some(3) = v {
        println!("three");
    }
    
    // 宏：matches!，它可以将一个表达式跟模式进行匹配，然后返回匹配的结果 true or false。
    let foo = 'f';
    assert!(matches!(foo, 'A'..='Z' | 'a'..='z'));   //使用match!就可以匹配枚举成员进行性比较
    ```

    

  - 解构Option

    ```rust
    //一个变量要么有值：Some(T), 要么为空：None
    enum Option<T> {
        Some(T),
        None,
    }
    ```

  - 模式适用场景

    ```rust
    //模式是 Rust 中的特殊语法，它用来匹配类型中的结构和数据，它往往和 match 表达式联用，以实现强大的模式匹配能力。模式一般由以下内容组合而成：
        //字面值
        //解构的数组、枚举、结构体或者元组
        //变量
        //通配符
        //占位符
    //1. match 分支
    match VALUE {
        PATTERN => EXPRESSION,
        PATTERN => EXPRESSION,
        PATTERN => EXPRESSION,
    }
    //2. if let 分支
    if let PATTERN = SOME_VALUE {  //if let 允许匹配一种模式，
    }
    //3. while let 条件循环 
    while let Some(top) = stack.pop() {// stack.pop从数组尾部弹出元素
        println!("{}", top);
    }
    //4. for循环
    let v = vec!['a','b','c'];
    for (index, value) in v.iter().enumerate() {
        println!("{} is at index {}", value, index);
    }
    //5. let语句
    let PATTERN = EXPRESSION;  //这个模式匹配 也是神奇，要求匹配类型上 对位上
    //6. 函数参数
    fn foo(x: i32) {
        // 代码
    }
    ```

- 方法method

  ```rust
  
  struct Circle {
      x: f64,
      y: f64,
      radius: f64,
  }
  
  impl Circle {
      // new是Circle的关联函数，因为它的第一个参数不是self，且new并不是关键字
      // 这种方法往往用于初始化当前结构体的实例
      // 这种定义在 impl 中且没有 self 的函数被称之为关联函数： 因为它没有 self,我们需要用 :: 来调用，例如 let cn = Circle::new(3, 3,3);。这个方法位于结构体的命名空间中：:: 语法用于关联函数和模块创建的命名空间, 如 String::from 一样。
      fn new(x: f64, y: f64, radius: f64) -> Circle {
          Circle {
              x: x,
              y: y,
              radius: radius,
          }
      }
  
      // Circle的方法，&self表示借用当前的Circle结构体
      // self 表示 Rectangle 的所有权转移到该方法中，这种形式用的较少
      // &self 表示该方法对 Rectangle 的不可变借用
      // &mut self 表示可变借用
      fn area(&self) -> f64 {
          std::f64::consts::PI * (self.radius * self.radius)
      }
  }
  
  // 枚举 也可以实现方法 好强大o^o
  #![allow(unused)]
  enum Message {
      Quit,
      Move { x: i32, y: i32 },
      Write(String),
      ChangeColor(i32, i32, i32),
  }
  
  impl Message {
      fn call(&self) {
          // 在这里定义方法体
      }
  }
  
  fn main() {
      let m = Message::Write(String::from("hello"));
      m.call();
  }
  ```




## 7/10

---

继续rustlings...



## 7/11

---

- 泛型

  针对值的泛型（壕无人性...）

  ```rust
  // N 这个泛型参数，它是一个基于值的泛型参数！因为它用来替代的是数组的长度。N 就是 const 泛型，定义的语法是 const N: usize，表示 const 泛型 N ，它基于的值类型是 usize。
  fn display_array<T: std::fmt::Debug, const N: usize>(arr: [T; N]) {
      println!("{:?}", arr);
  }
  fn main() {
      let arr: [i32; 3] = [1, 2, 3];
      display_array(arr);
      let arr: [i32; 2] = [1, 2];
      display_array(arr);
  }
  ```

- 特征

  ```rust
  //特征定义了**一个可以被共享的行为，只要实现了特征，你就能使用该行为**。
  //如果不同的类型具有相同的行为，那么我们就可以定义一个特征，然后为这些类型实现该特征。定义特征是把一些方法组合在一起，目的是定义一个实现某些目标所必需的行为的集合。
  // 真的是类似**接口**
  pub trait Summary {
      fn summarize(&self) -> String;
  }
  pub struct Post {
      pub title: String, // 标题
      pub author: String, // 作者
      pub content: String, // 内容
  }
  
  impl Summary for Post {
      fn summarize(&self) -> String {
          format!("文章{}, 作者是{}", self.title, self.author)
      }
  }
  
  pub struct Weibo {
      pub username: String,
      pub content: String
  }
  
  impl Summary for Weibo {
      fn summarize(&self) -> String {
          format!("{}发表了微博{}", self.username, self.content)
      }
  }
  ```

  ## 7/12

  ---

  休息中...

  
  ## 7/13

  ---

  rust 不愧是拥有陡峭学习难度，直接干蒙了。为了作业任务，也只能有选择的查看学习了。
  
  - 集合类型
    - Vector  
    可理解动态数组
    ```rust
      let mut v = Vec::new();
      v.push(1);
      // 使用宏创建初始化
      let v = vec![1, 2, 3];
    ```
    - KV存储HashMap
    ```rust
      use std::collections::HashMap;

      let mut scores = HashMap::new();

      scores.insert(String::from("Blue"), 10);
      scores.insert(String::from("Yellow"), 50);

      let team_name = String::from("Blue");
      let score: Option<&i32> = scores.get(&team_name);
    ```

  - 返回值和错误处理
    - panic!("crash and burn");
    - 错误处理
    ```rust
    use std::fs::File;

    fn main() {
        let f = File::open("hello.txt");

        let f = match f {
            Ok(file) => file,
            Err(error) => {
                panic!("Problem opening the file: {:?}", error)
            },
        };
    }
    ```
  
  - 包和模块
    - 项目(Packages)：一个 Cargo 提供的 feature，可以用来构建、测试和分享包
    - 包(Crate)：一个由多个模块组成的树形结构，可以作为三方库进行分发，也可以生成可执行文件进行运行
    - 模块(Module)：可以一个文件多个模块，也可以一个文件一个模块，模块可以被认为是真实项目中的代码组织单元

  ## 7/16

  ---

  今天周末终于有时间做这个rustlings小测验，不敢记录太多日记，怕太多都是关于rust变态感叹，:)  ,rust有很多需要学习的地方对于我来说，没怎么接触过这个语言，后面要是直接上手编程确实要费些功夫，rust很多特性给人带来很多新奇（虽然很多早就有了），值得学习。