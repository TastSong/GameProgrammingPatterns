## 服务定位器

### 定义

提供服务的全局接入点，避免使用者和实现服务的具体类耦合。

### 场景

* 全局只有一个；建议和单例一样少用

### 案例

[全局声音管理](./Assets/DecouplingPatterns/ServiceLocator)

### 实现方式

* **服务** 类定义了一堆操作的抽象接口。

* 具体的**服务提供者**实现这个接口。 

* 分离的**服务定位器**提供了通过查询获取服务的方法，同时隐藏了服务提供者的具体细节和定位它的过程。

### 优缺点

**优点**

-  你可以保证一个类只有一个实例。
-  你获得了一个指向该实例的全局访问节点。
-  仅在首次请求对象时对其进行初始化。

**缺点**

-  违反了_单一职责原则_。 该模式同时解决了两个问题*(在一个方法中进行了创建类和提供类对象的操作)*。
-  单例模式可能掩盖不良设计， 比如程序各组件之间相互了解过多等。
-  该模式在多线程环境下需要进行特殊处理， 避免多个线程多次创建单例对象。
-  客户端代码单元测试可能会比较困难， 因为许多测试框架以基于继承的方式创建模拟对象。 由于构造函数是私有的， 而且绝大部分语言无法重写静态方法， 所以你需要想出仔细考虑模拟单例的方法。 要么干脆不编写测试代码， 或者不使用此模式。

### 与其他设计模式的关系

- **服务定位模式**在很多方面是**单例模式**的兄弟，在应用前值得看看哪个更适合你的需求。