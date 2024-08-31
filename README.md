# Container Wrapper

## Introduction

我们实现容器（或者是普通的类）时，常存在难以进行功能性测试的问题。
我曾经写了个[哈希表](https://github.com/1nchy/cpp-stl/blob/master/hash_table.hpp)，尽管经过了较多的手动传参测试，但后来仍然发现实现代码中存在着问题。

至于问题是如何被发现的，我生成了大量的随机操作序列，让类进行上百万次 curd 操作。并在类的结构中定义了 `check` 方法，用来检测其内部数据结构是否被破坏。
详见[代码](https://github.com/1nchy/cpp-stl/blob/master/adebug.hpp)。

这个方法虽然有效，但有诸多缺点：

1. 对随机操作序列的抽象层次较低。
2. 只能对容器的几个固定方法进行测试，如 `clear`，`add` 等在不同容器中参数个数相同的函数。
3. 对容器成员方法的绑定方式不灵活，只能基于上面的特性，把容器成员方法绑定到固定类型的成员变量中。
4. 对新增方法的测试不友好，需要增加操作序列 id、增加容器测试类的成员变量等。
5. 对某些传参较特殊的方法无法测试，例如 `insert` 等。

限于当时的代码及工程能力，没有抽象成更好的测试工具。

而在今天，正如该项目所展示的那样，我把这个测试工具进行了更好的抽象与优化。
包括了随机对象生成，更好的容器及成员方法包装。

关于测试用例的效率，这个确实只能力大砖飞，相比起大模型生成测试用例，这个的优势在于小巧方便，顺便在实现的过程中多学习一下 c++ 的模板知识。

## Details

`container::wrapper` 类还是比较复杂的，具体的设计与构造过程，见[文档](./doc/container_wrapper.md)。