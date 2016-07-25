# Second Weekly Report

***By Zhang Qi***



#### Working Situation For This Week

The main task of this week is to get started with ZooKeeper. ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these kinds of services are used in some form or another by distributed applications. Each time they are implemented there is a lot of work that goes into fixing the bugs and race conditions that are inevitable. Because of the difficulty of implementing these kinds of services, applications initially usually skimp on them ,which make them brittle in the presence of change and difficult to manage. Even when done correctly, different implementations of these services lead to management complexity when the applications are deployed.

I have a general idea of the concept of ZooKeeper. ZooKeeper is a distributed, open-source coordination service for distributed applications. It exposes a simple set of primitives that distributed applications can build upon to implement higher level services for synchronization, configuration maintenance, and groups and naming. It is designed to be easy to program to, and uses a data model styled after the familiar directory tree structure of file systems. It runs in Java and has bindings for both Java and C. ZooKeeper is simple. ZooKeeper is replicated. ZooKeeper is ordered. ZooKeeper is fast.

Besides, I've learnt some other properties of ZooKeeper.

* Data model and the hierarchical namespace
* Nodes and ephemeral nodes
* Conditional updates and watches
* Guarantees
* Simple API
* Implementation
* Uses
* Performance
* Reliability
* The ZooKeeper Project

After that, I tried the three methods of setting up the environment of ZooKeeper.

* Stand alone
* Clustering pattern
* Pseudo-clustering pattern

#### Problems Encountered

* When installing ZooKeeper in the three virtual machines on the same server, and setting up the NAT network for the three ZooKeeper servers to allow other clients on the Internet to connect with them, I failed to use ZooKeeper API for Java to connect to those ZooKeeper servers.
* At first, I was really confused by the three different methods to set up the environment of ZooKeeper. What is Stand alone pattern? What is Clustering pattern? And what is Pseudo-clustering pattern? How can I implement these methods on my computer?
* There are few infomation of introduction of developing ZooKeeper application using python. However, the teacher assistant recommended us to use python as the developing language.

#### Working Plan For Next Week

* Get into further study of ZooKeeper
* Be familiar with the API under command line
* Be familiar with the API under Java and Python environment
* Study the cross-platform libraray of ZooKeeper of different language
* Work systematically on Python grammar
* Start up the project of this training program



