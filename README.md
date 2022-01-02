# Game Programming Patterns 游戏编程模式
Unity实现《游戏编程模式》

# 重访设计模式
## 命令模式

### 定义

将一个请求封装为**一个对象**，从而使你可用不同的请求对客户进行参数化； 对请求排队或记录请求日志，以及支持可**撤销**的操作。

### 场景

1. 通过操作来参数化对象
2. 将操作放入队列中、操作的执行或者远程执行操作
3. 实现操作回滚功能

### 案例

1. **[配置输入](./Assets/DesignPatternsRevisited/CommandPattern)**：用户通过键盘、手柄以及界面按钮实现移动等操作，并可以实现撤销操作；
2. GUI中的点击等UI操作，即**交互逻辑**应该可以通过命令模式来实现具体的业务逻辑，从而进行逻辑解耦；数值更新的**表现逻辑**，可以通过**观察者模式**进行逻辑解耦*(事件的方式，进行通知)*；

### 实现方式

1. 声明仅有一个执行方法的[命令接口](./Assets/DesignPatternsRevisited/CommandPattern/Command.cs)。
2. 抽取请求并使之成为实现命令接口的[具体命令类](./Assets/DesignPatternsRevisited/CommandPattern/MoveCommand.cs)。 每个类都必须有一组成员变量来保存请求参数和对于实际接收者对象的引用。 所有这些变量的数值都必须通过命令构造函数进行初始化。
3. 找到担任[*发送者*职责的类](./Assets/DesignPatternsRevisited/CommandPattern/InputHandler.cs)。 在这些类中添加保存命令的成员变量。 发送者只能通过命令接口与其命令进行交互。 发送者自身通常并不创建命令对象， 而是通过客户端代码获取。
4. 修改发送者使其执行命令， 而非直接将请求发送给接收者。
5. 客户端必须按照以下顺序来初始化对象：
   - 创建接收者。
   - 创建命令， 如有需要可将其关联至接收者。
   - 创建发送者并将其与特定命令关联。

### 优缺点

**优点**

-  *单一职责原则*。 你可以解耦[触发](./Assets/DesignPatternsRevisited/CommandPattern/MoveCommand.cs)和[执行](./Assets/DesignPatternsRevisited/CommandPattern/MoveCommandReceiver.cs)操作的类。

-  *开闭原则*。 你可以在不修改已有客户端代码的情况下在程序中创建新的命令。

-  你可以实现撤销和恢复功能。

-  你可以实现操作的延迟执行。

-  你可以将一组简单命令组合成一个复杂命令。

- 运行时切换连接至发送者的命令对象， 以此改变发送者的行为。

  ```c#
  MoveCommand moveCommand = new MoveCommand(moveCommandReciever, direction, moveDistance, objectToMove);
  JumpCommand jumpCommand = new JumpCommand(jumpCommandReciever, direction, jumpDistance, objectToMove);
  Command command;
  if (isMove){
      command = moveCommand；
  } else {
      command = jumpCommand；
  }
  command.Execute();
  ```

**缺点**

* 代码可能会变得更加复杂， 因为你在发送者和接收者之间增加了一个全新的层次。*(全新层次指本来只需要直接调用方法来实现操作就可以，现在需要通过命令类来实现操作)*

### 与其他设计模式的关系

- 责任链模式***(GOF)*、 命令模式、 中介者模式** *(GOF)*和观察者模式用于处理请求发送者和接收者之间的不同连接方式：

  - *责任链*按照顺序将请求动态传递给**一系列**的潜在接收者， 直至其中一名接收者对请求进行处理。
  - *命令*在发送者和请求者之间建立**单向连接**。
  - *中介者*清除了发送者和请求者之间的直接连接， 强制它们通过一个中介对象进行**间接沟通(双向)**。
  - *观察者*允许接收者动态地**订阅或取消**接收请求。

- 责任链的管理者可使用命令模式实现。 在这种情况下， 你可以对由请求代表的同一个上下文对象执行许多不同的操作。

  还有另外一种实现方式， 那就是请求自身就是一个*命令*对象。 在这种情况下， 你可以对由一系列不同上下文连接而成的链执行相同的操作。

- 你可以同时使用**命令**和**备忘录模式** *(GOF)*来实现 “撤销”。 在这种情况下， 命令用于对目标对象执行各种不同的操作， 备忘录用来保存一条命令执行前该对象的状态。

- 命令和策略模式看上去很像， 因为两者都能通过某些行为来参数化对象。 但是， 它们的意图有非常大的不同。

  - 你可以使用*命令*来将任何操作转换为对象。 操作的参数将成为对象的成员变量。 你可以通过转换来延迟操作的执行、 将操作放入队列、 保存历史命令或者向远程服务发送命令等。
  - 另一方面， *策略*通常可用于描述完成某件事的不同方式， 让你能够在同一个上下文类中切换算法。

- 原型模式可用于保存命令的历史记录。

- 你可以将访问者模式视为命令模式的加强版本， 其对象可对不同类的多种对象执行操作。

## 享元模式

### 定义

摒弃了在每个对象中保存所有数据的方式， 通过**共享**多个对象所共有的相同状态， 让你能在有限的内存容量中**载入更多对象**。

### 场景

1. 仅在程序必须支持**大量对象**且没有足够的内存容量时

### 案例

**[字符对象](./Assets/DesignPatternsRevisited/FlyweightPattern)**：A-Z每个字符作为一个对象，所有的A，有着相同的属性(内在属性)，例如：width、height等；也有着不同的属性(外在属性)，例如：pointSize

### 实现方式

1. 将需要改写为享元的类成员变量拆分为两个部分：
   - 内在状态： 包含不变的、 可在许多对象中重复使用的数据的成员变量。
   - 外在状态： 包含每个对象各自不同的情景数据的成员变量
2. 保留类中表示内在状态的成员变量， 并将其属性设置为不可修改。 这些变量仅可在构造函数中获得初始数值。
3. 找到所有使用外在状态成员变量的方法， 为在方法中所用的每个成员变量新建一个参数， 并使用该参数代替成员变量。
4. 你可以有选择地创建工厂类来管理享元缓存池， 它负责在新建享元时检查已有的享元。 如果选择使用工厂， 客户端就只能通过工厂来请求享元， 它们需要将享元的内在状态作为参数传递给工厂。
5. 客户端必须存储和计算外在状态 （情景） 的数值， 因为只有这样才能调用享元对象的方法。 为了使用方便， 外在状态和引用享元的成员变量可以移动到单独的情景类中。

### 优缺点

**优点**

-  如果程序中有很多相似对象， 那么你将可以节省大量内存。


**缺点**

*  你可能需要牺牲执行速度来换取内存， 因为他人每次调用享元方法时都需要重新计算部分情景数据。
*  代码会变得更加复杂。 团队中的新成员总是会问：  “为什么要像这样拆分一个实体的状态？”。

### 与其他设计模式的关系

- 你可以使用**享元模式**实现**组合模式***(GOF)*树的共享叶节点以节省内存。

- 享元展示了如何生成大量的小型对象， **外观模式*****(GOF)*则展示了如何用一个对象来代表整个子系统。
- 如果你能将对象的所有共享状态简化为一个享元对象， 那么**享元**就和**单例模式**类似了。 但这两个模式有两个根本性的不同。
  1. 只会有一个单例实体， 但是*享元*类可以有多个实体， 各实体的内在状态也可以不同。
  2. *单例*对象可以是可变的。 享元对象是不可变的。

## 观察者模式
## 原型模式
## 单例模式
## 状态模式
# 序列模式
## 双缓冲模式
## 游戏循环
## 更新方法
# 行为模式
## 字节码
## 子类沙箱
## 类型对象
# 解耦模式
## 组件模式
## 事件队列
## 服务定位器
# 优化模式
## 数据局部性
## 脏标识模式
## 对象池模式
## 空间分区

