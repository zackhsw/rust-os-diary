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