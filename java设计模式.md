---
title: java设计模式
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---
### 设计模式总结
[基础的介绍][1]
设计模式是软件开发人员在软件开发过程中面临的一般问题的解决方案，定义就是开发问题解决方案，经验之道，工程代码比较重要的就是规范，大家都遵守一个规范开发就会很舒服。
**关键词**：开发人员的共同平台，最佳的实践
一共23种设计模型
创建型
结构型
行为型
j2EE
#### 六大原则

 1. 开闭原则（Open Close Principle），对扩展开放，对修改关闭，实现热插拔效果，使用接口和抽象类实现
 2. 里氏代换原则（Liskov Substitution Principle）
 3. 依赖倒转原则（Dependence Inversion Principle），依赖于抽象而不依赖于具体
 4. 接口隔离原则（Interface Segregation Principle），使用多个接口，不要使用一个接口实现多个功能，降低耦合度
 5. 迪米特法则，又称最少知道原则（Demeter Principle），功能模块尽量独立。
 6. 合成复用原则（Composite Reuse Principle），尽量使用合成和聚合的方式，而不是使用继承

### UML总结

[类图][2]

**类图**
作用就是理清楚类和类之间的关系，用于设计和分析阶段
类的关系有泛化(Generalization)、实现（Realization）、依赖(Dependency)和关联(Association)。其中关联又分为一般关联关系和聚合关系(Aggregation)，合成关系(Composition)。下面我们结合实例理解这些关系。


  [1]: http://www.runoob.com/design-pattern/design-pattern-intro.html
  [2]: http://www.uml.org.cn/oobject/201104212.asp