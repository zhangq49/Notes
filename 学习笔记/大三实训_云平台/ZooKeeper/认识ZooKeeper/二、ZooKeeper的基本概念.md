# 二、ZooKeeper的基本概念

## 集群角色

#### Leader、Follower、Observer

* Leader服务器是整个ZooKeeper集群工作机制中的核心
* Follower服务器是ZooKeeper集群状态的跟随者
* Observer服务器充当一个观察者的角色



#### 设计模式

* Leader、Follower设计模式
* Observer观察者设计模式



## 会话

* 客户端与ZooKeeper服务器的连接
* 使用TCP连接维持



## 数据节点

#### 两类数据节点

* 急群中的一台机器称为一个节点
* 数据模型中的数据单元Znode，分为持久节点和临时节点。ZooKeeper的数据模型就是一棵树，树的节点就是Znode，Znode中可以保存信息。



## 版本

#### 版本类型

* version：当前数据节点数据内容的版本号
* cversion：当前数据节点子节点的版本号
* aversion：当前数据节点ACL变更版本号



#### 数据库锁类型

* 悲观锁
* 乐观锁



## wathcer

* 事件监听器

  ZooKeeper允许用户在指定节点上注册一些watcher，当数据节点发生变化时，ZooKeeper服务器会把这个变化的通知发送给感兴趣的客户端



## ACL权限控制

#### ACL是Access Control Lists的简写，ZooKeeper采用ACL策略来进行权限的控制，有以下权限：

* CREATE：创建子节点的权限
* READ：获取节点数据和子节点列表的权限
* WRITE：更新节点数据的权限
* DELETE：删除子节点的权限
* ADMIN：设置节点ACL的权限

