# 面向对象

面向对象是一种编程范式，用“对象”组织代码和数据，把数据和操作数据的方式封装在一起，目的是方便重用、维护和扩展（实际上大多数情况下反而相反）。

- 对象（Object）：一个实体，有状态（属性）和行为（方法）。
- 类（Class）：对象的抽象。
- 封装（Encapsulation）：将对象和状态和行为隐藏在类的内部，用公共的接口交互，保护内部状态不被外部直接修改。
- 继承（Inheritance）：闯进一个新的类（子类），扩展现有类（父类）的功能。自然继承了父类的属性和方法。
- 多态（Polymorphism）：通过方法重载和重写，允许不同的对象响应相同的方法调用。


## 模拟类

这个很简单能想到用 `Struct` 模拟属性，用函数指针模拟方法。


```c
struct _Point {
    int x;
    int y;
    void (*move)(struct _Point*, int, int);
    void (*report)(struct _Point*);
};
```

## 封装

把定义和声明分开，用 `static` 限制访问。还有编译为动态库，只给出头文件声明，这种实现细节封装方式。

## 继承

用新的结构体组合原先的，模拟出继承的样子。

```c
typedef struct {
    Point base;
    int width;
    int height;
    void (*resize)(struct Rectangle*, int, int);
} Rectangle;
```

## 多态

可以用函数指针重定向方法来模拟编译时的静态绑定。