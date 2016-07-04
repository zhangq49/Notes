# Chapter 4 Novel Introdution of UML Models

## What is visual modeling?

#### Concepts

* Modeling captures essential parts of the system.
* Visual Modeling is modeling using standard graphical notations.

#### Visual Modeling Captures Business Processes

* Use-case analysis is a technique to capture business processes from a user's perspective.

#### Visual Modeling Is a Communication Tool

* Use visual modeling to capture business objects and logic
* Use visual modeling to analyze and design your application

#### Visual Modeling Manages Complexity

#### Visual Modeling Promotes Reuse

---

## What is the UML?

The UML is the standard language for visualizing, specifying, constructing, and documenting the artifacts of a software-intensive system.

---

## UML diagrams

#### Agenda

* Use case model: 
  * use case diag.
  * activity diag.
* Interaction diagrams:
  * sequence diag.
  * collaboration diag.
* Class model:
  *  class diag.
* UML other diagrams:
  * statechart diag.
  * deployment diag.
  * components diag.
  * package diag.

---

#### Use-Case Model

* What is a Use-Case Model?
  * A model that describes a system's functional requirements in terms of use cases.
  * A model of the system's intended functions(use cases) and its environment(actors).
* Actor
  * anything that interacts with the system.
  * role a user of the system can play.
  * not part of the system.
* Use case
  * describes a sequence of events, performed by the system, that yields an observable results of value to a particular actor.
* 用例图
  * 从系统的外部用户的观点看系统应该具有的功能
  * 用例图主要用于对系统、子系统或类的行为进行建模
  * 它只说明系统实现了什么功能，而不必说明如何实现
* 活动图
  * An activity diagram in the use-case model can be used to capture the activities in a use case.
  * 提供了对工作流进行建模的途径
  * 活动图中的活动
    * 表示执行工作流中的一组动作
    * 一旦结束，控制流将自动转移到下一个活动，或通过转换进入下一个状态

---

#### Interaction diagrams

* 时序图
  * 时序图描述了在时间上对象交互的安排
  * 图形展现了
    * 多个交互对象
    * 信息交流的序列
  * 时序图包含
    * 对象
    * 对象生命线
    * 按顺序对象间的信息交流
    * 控制焦点（optional）


* 协作图
  * 协作图是强调发送和接收消息的对象间的结构组织的交互图。在图形上，协作图是顶点和弧的结合。
  * 协作图包含
    * 对象
    * 链
    * 消息
* 协作图和时序图的不同点

---

#### Class Diagrams

* What is a Class Diagrams?

  Static View of a System

* 关系

  * 聚集
  * 泛化（继承）
  * 关联

#### 对象图

* 类图的一种变形
* 在对象名下面要加下划线
* 所使用的符号与类图基本相同

#### 接口

* 只具有操作的功能，不具有属性、关联和操作的实现
* 和类一样用四角形表示实例，使用《interface》构造型
* 用实现关系（带空心白色三角的虚线）符号来连接实现接口的元素（类，构件等）

---

#### Statechart Diagrams

* 作用

  显示一个对象从创建到消亡的整个生命周期

* 状态图主要显示内容

  对象在生命周期里所经历的状态序列

  诱发对象从一个状态变为另一个状态的事件

  状态改变所导致的动作

#### Deployment Diagram

* 描述执行时的系统结构（硬件、软件）
  * 执行环境中的硬件结构和连接关系
  * 对硬件（节点）部署软件（构件）

#### Component Diagram

* 提供当前模型的物理视图，对系统地静态实现视图进行建模
* 从组织内容看，构件图显示软件构件的组织及构件间的依赖关系
  * 源代码构件
  * 二进制代码构件
  * 可执行构件
* 构件图中，构件间的调用表示为构件间的依赖关系

#### 包

* 包是基于模型元素的含义或作用将模型元素分组的一种机制
* 目的：通过分组，可提高模型的维持性

---

## UML

#### 什么是UML

* 面向对象软件工程使用的统一建模语言
* 一种图形化了的语言，主要用图形方式表示
* 一种开放的标准

#### 特点

* 统一的标准
* 面向对象
* 可视化
* 表达能力强

#### 应用

* 在软件开发中的应用
  * 可视化
  * 说明
  * 建造
  * 建档
* UML是一个通用的标准建模语言
  * 静态结构建模
  * 动态行为建模
  * 体系架构建模
* UML是一种建模语言
  * 不是一种方法，它独立于过程
  * 可遵循任何类型的建模过程

