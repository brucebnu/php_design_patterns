# PHP设计模式
- 学习理解设计模式，记录PHP关于23种设计模式的使用,欢迎Star
-  git@github.com:brucebnu/php_design_patterns.git  

- 设计模式分为：创建型模式， 结构型模式，行为型模式等23种设计模式。 

## 五种创建型模式如下：
工厂方法模式  factory_method   
抽象工厂模式  abstract_factory  
单例模式    singleton  
建造者模式   builder   
原型模式    prototype   

## 结构型模式如下：
适配器模式   adapter    
桥接模式    bridge     
合成模式    composite    
装饰器模式   decorator    
门面模式    facade    
代理模式    proxy    
享元模式    flyweight   

## 行为型模式如下：
策略模式    strategy     
模板方法模式  template_method

### 观察者模式(Observer Pattern) observer
- 定义：定义对象间的一种一对多依赖关系，使得每当一个对象状态发生改变时，其相关依赖对象皆得到通知并被自动更新。
    - 观察者模式又叫做发布-订阅（Publish/Subscribe）模式、模型-视图（Model/View）模式、源-监听器（Source/Listener）模式或从属者（Dependents）模式。
- 场景：比如在设置用户(主题)的状态后要分别发送当前的状态描述信息给用户的邮箱和手机，我们可以使用两个观察者订阅用户的状态，一旦设置状态后主题就会通知的订阅了状态改变的观察者，在两个观察者里面我们可以分别来实现发送邮件信息和短信信息的功能。
     
迭代器模式   decorator    
责任链模式   responsibility_chain    
命令模式    command   
备忘录模式   memento    
状态模式    state     
访问者模式   visitor    
中介者模式   mediator   
解释器模式   interpreter  

# 设计模式六大原则
## 单一职责原则
- [定义](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-1.html)：不要存在多于一个导致类变更的原因。通俗的说，即一个类只负责一项职责。
- 问题由来：类T负责两个不同的职责：职责P1，职责P2。当由于职责P1需求发生改变而需要修改类T时，有可能会导致原本运行正常的职责P2功能发生故障。
- 解决方案：遵循单一职责原则。分别建立两个类T1、T2，使T1完成职责P1功能，T2完成职责P2功能。这样，当修改类T1时，不会使职责P2发生故障风险；同理，当修改T2时，也不会使职责P1发生故障风险。
- 备注：职责扩散，就是因为某种原因，职责P被分化为粒度更细的职责P1和P2。所以记住，在职责扩散到我们无法控制的程度之前，立刻对代码进行重构。

## 里氏替换原则 1988
- [定义 1](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-2.html)：如果对每一个类型为 T1的对象 o1，都有类型为 T2 的对象o2，使得以 T1定义的所有程序 P 在所有的对象 o1 都代换成 o2 时，程序 P 的行为没有发生变化，那么类型 T2 是类型 T1 的子类型。
- 定义 2：所有引用基类的地方必须能透明地使用其子类的对象。
- 问题由来：有一功能P1，由类A完成。现需要将功能P1进行扩展，扩展后的功能为P，其中P由原有功能P1与新功能P2组成。新功能P由类A的子类B来完成，则子类B在完成新功能P2的同时，有可能会导致原有功能P1发生故障。
- 解决方案：当使用继承时，遵循里氏替换原则。类B继承类A时，除添加新的方法完成新增功能P2外，尽量不要重写父类A的方法，也尽量不要重载父类A的方法。继承包含这样一层含义：父类中凡是已经实现好的方法（相对于抽象方法而言），实际上是在设定一系列的规范和契约，虽然它不强制要求所有的子类必须遵从这些契约，但是如果子类对这些非抽象方法任意修改，就会对整个继承体系造成破坏。而里氏替换原则就是表达了这一层含义。 
- 备注： 继承带来便利的同时，也存在需要注意的弊端：侵入性、可移植性、增加对象之间耦合性

## 依赖倒置原则
- [定义](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-3.html)：高层模块不应该依赖低层模块，二者都应该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象。
- 问题由来：类A直接依赖类B，假如要将类A改为依赖类C，则必须通过修改类A的代码来达成。这种场景下，类A一般是高层模块，负责复杂的业务逻辑；类B和类C是低层模块，负责基本的原子操作；假如修改类A，会给程序带来不必要的风险。
- 解决方案：将类A修改为依赖接口I，类B和类C各自实现接口I，类A通过接口I间接与类B或者类C发生联系，则会大大降低修改类A的几率。
依赖倒置原则基于这样一个事实：相对于细节的多变性，抽象的东西要稳定的多。以抽象为基础搭建起来的架构比以细节为基础搭建起来的架构要稳定的多。在Java中，抽象指的是接口或者抽象类，细节就是具体的实现类，使用接口或者抽象类的目的是制定好规范和契约，而不去涉及任何具体的操作，把展现细节的任务交给他们的实现类去完成。
        
        依赖倒置原则的核心思想是面向接口编程

## 接口隔离原则
- [定义](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-4.html)：客户端不应该依赖它不需要的接口；一个类对另一个类的依赖应该建立在最小的接口上。 
- 问题由来：类A通过接口I依赖类B，类C通过接口I依赖类D，如果接口I对于类A和类B来说不是最小接口，则类B和类D必须去实现他们不需要的方法。
- 解决方案：将臃肿的接口I拆分为独立的几个接口，类A和类C分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则。


## 迪米特法则(最少知道法则) 1987
- [定义](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-5.html)：一个对象应该对其他对象保持最少的了解。 
- 问题由来：类与类之间的关系越密切，耦合度越大，当一个类发生改变时，对另一个类的影响也越大。
- 解决方案：尽量降低类与类之间的耦合。自从我们接触编程开始，就知道了软件编程的总的原则：低耦合，高内聚。无论是面向过程编程还是面向对象编程，只有使各个模块之间的耦合尽量的低，才能提高代码的复用率。低耦合的优点不言而喻，但是怎么样编程才能做到低耦合呢？那正是迪米特法则要去完成的。
- 备注：迪米特法则又叫最少知道原则。通俗的来讲，就是一个类对自己依赖的类知道的越少越好。也就是说，对于被依赖的类来说，无论逻辑多么复杂，都尽量地的将逻辑封装在类的内部，对外除了提供的public方法，不对外泄漏任何信息。迪米特法则还有一个更简单的定义：<b>只与直接的朋友通信</b>。首先来解释一下什么是直接的朋友：每个对象都会与其他对象有耦合关系，只要两个对象之间有耦合关系，我们就说这两个对象之间是朋友关系。耦合的方式很多，依赖、关联、组合、聚合等。其中，我们称出现成员变量、方法参数、方法返回值中的类为直接的朋友，而出现在局部变量中的类则不是直接的朋友。也就是说，陌生的类最好不要作为局部变量的形式出现在类的内部。

## 开放封闭原则
- [定义](http://wiki.jikexueyuan.com/project/java-design-pattern-principle/principle-6.html)：一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。 
- 问题由来：在软件的生命周期内，因为变化、升级和维护等原因需要对软件原有代码进行修改时，可能会给旧代码中引入错误，也可能会使我们不得不对整个功能进行重构，并且需要原有代码经过重新测试。
- 解决方案：
    - 当软件需要变化时，尽量通过扩展软件实体的行为来实现变化，而不是通过修改已有的代码来实现变化。 
    - 开闭原则是面向对象设计中最基础的设计原则，它指导我们如何建立稳定灵活的系统。开闭原则可能是设计模式六项原则中定义最模糊的一个了，它只告诉我们对扩展开放，对修改关闭，可是到底如何才能做到对扩展开放，对修改关闭，并没有明确的告诉我们。以前，如果有人告诉我"你进行设计的时候一定要遵守开闭原则"，我会觉的他什么都没说，但貌似又什么都说了。因为开闭原则真的太虚了。
    - 开闭原则无非就是想表达这样一层意思：用抽象构建框架，用实现扩展细节。因为抽象灵活性好，适应性广，只要抽象的合理，可以基本保持软件架构的稳定。而软件中易变的细节，我们用从抽象派生的实现类来进行扩展，当软件需要发生变化时，我们只需要根据需求重新派生一个实现类来扩展就可以了。当然前提是我们的抽象要合理，要对需求的变更有前瞻性和预见性才行。
    
## 总结
- 在仔细思考以及仔细阅读很多设计模式的文章后，终于对开闭原则有了一点认识。其实，我们遵循设计模式前面5大原则，以及使用23种设计模式的目的就是遵循开闭原则。也就是说，只要我们对前面5项原则遵守的好了，设计出的软件自然是符合开闭原则的，这个开闭原则更像是前面五项原则遵守程度的"平均得分"，前面5项原则遵守的好，平均分自然就高，说明软件设计开闭原则遵守的好；如果前面5项原则遵守的不好，则说明开闭原则遵守的不好。
- 再回想一下前面说的5项原则，恰恰是告诉我们用抽象构建框架，用实现扩展细节的注意事项而已；
- 单一职责原则，告诉我们实现类要职责单一；
- 里氏替换原则，告诉我们不要破坏继承体系；
- 依赖倒置原则，告诉我们要面向接口编程；
- 接口隔离原则，告诉我们在设计接口的时候要精简单一；
- 迪米特法则，告诉我们要降低耦合。
- 而开闭原则是总纲，他告诉我们要对扩展开放，对修改关闭。