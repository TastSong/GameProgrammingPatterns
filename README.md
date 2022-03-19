# Game Programmer Study Notes 游戏编程学习笔记 

# Game Programming Patterns 游戏编程模式

![](./Pictures/GameProgrammingPatterns.png)

[代码示例](./GameProgrammingPatterns)	

- 重访设计模式
  - [命令模式](./GameProgrammingPatterns/Command.md)：*将“请求〞封装成对象，以便使用不同的清求，队列或者日志来参数化其他对象，同时支持可撤消的操作*
  - [享元模式](./GameProgrammingPatterns/Flyweight.md)：*以共享的方式高效地支持大量的细粒度的对象。通过复用内存中已存在的对象，降低系络创建对象实例的性能消耗*
  - [观察者模式](./GameProgrammingPatterns/Observer.md)：*定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被白动更新*
  - [原型模式](./GameProgrammingPatterns/Prototype.md)：*用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象*
  - [单例模式](./GameProgrammingPatterns/Singleton.md)：*保证一个类只有一个实例，并且提供了访问该实例的全局访问点*
  - [状态模式](./GameProgrammingPatterns/State.md)：*允许对象在当内部状态改交时改交其行为，就好像此对象改变了自己的类一样*
- 序列模式
  - [双缓冲模式](./GameProgrammingPatterns/DoubleBuffer.md)：*使用序列操作来模拟瞬间或者同时发生的事情*
  - 游戏循环：*实现游戏运行过程中对用户输入处理和时间处理的解耦*
  - [更新方法](./GameProgrammingPatterns/UpdateMethod.md)：*通过每次处理一帧的行为来模拟一系列独立对象*
- 行为模式
  - [字节码](./GameProgrammingPatterns/Bytecode.md)：*将行为编码为虚拟机器上的指令，来赋予其数据的灵活性。从而让数据易于修改，易手加载，并与其他可执行部分相隔离*
  - [子类沙箱](./GameProgrammingPatterns/SubclassSandbox.md)：*用一系列由基类提供的操作定义子类中的行为*
  - [类型对象](./GameProgrammingPatterns/TypeObject.md)：*创造一个类A来允许灵活的创造新的类，而类A的每个实例都代表了不同类型的对象*
- 解耦模式
  - [组件模式](./GameProgrammingPatterns/Component.md)：*允许单一的实体跨越多个领域，无需这些领域彼此耦合*
  - [事件队列](./GameProgrammingPatterns/EventQueue.md)：*事件队列模式，对消息或事件的发送与处理进行时间上的解耦*
  - [服务定位器](./GameProgrammingPatterns/ServiceLocator.md)：*提供服务的全局接入点，而不心让用户和实现它的具体类解耦*
- 优化模式
  - [数据局部性](./GameProgrammingPatterns/DataLocality.md)：*合理组织数据，充分使用CPU的级存来加速内行读取*
  - [脏标识模式](./GameProgrammingPatterns/DirtyFlag.md)：*将工作延期至需要其结果时才去执行，以避免不心要的工作*
  - [对象池模式](./GameProgrammingPatterns/ObjectPool.md)：*放弃单独地分配和释放对象，从固定的池中重用对象，以提高性能和内存使用率*
  - [空间分区](./GameProgrammingPatterns/SpatialPartition.md)：*将对条存储在基于位置组织的数据结构中，来有效的定位对象*

# QFormwork Unity框架

![](./Pictures/QFormwork.png)

[文档说明](./QFormwork/README.md)

- 架构目的
- 设计原则
- 总体架构
- 实例
- 实现细节

# Unity 3D高级编程

![](./Pictures/ProfessionalNotes.png)

