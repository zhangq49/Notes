# Second Weekly Report

***By Zhang Qi***



#### Working Situation For This Week

The main tasks of this week are writing the requirement document of the Cloud Platform Monitor System and setting up the fundamental framework and elements.

We wrote our requirement document from the following points.

* General description of the Cloud Platform Monitor System
* The function structrue of the system
* The use case diagram of the system
* The use case specification of each use case
* The non-functional requirements of the system
* The glossary of this requirement document

Having some discussion about the system structure of the Cloud Platform Monitor System, we decided to divide the system into five parts, the Front-end part, the Web-server part, the ZooKeeper-server part, the OpenStack virtual machine part and the OpenStack Cloud part. According to the structure, we have done the following subtasks.

* Set up the environment of OpenStack on the physical server and create three virtual machine on the physical server.
* Install ZooKeeper server on the physical server and ZooKeeper client on both the physical server and the virtual machines.
* Install python library psutil on the physical server and the virtual machines.
* Collect the cpu info, the memory info, the disk info and the network info of the physical server and the virtual machines.
* Store the data of  a period time related to the current time and provide the APIs to the Web-server.
* The Web-server returns the data to the front-end.

#### Problems Encountered

* We've been stucked in monitoring the network flow of one single virtual machine, and we didn't know what exactly we should do to achive the task. Finally, we decided to simplify the data we collect and only calculate the total flow.
* What is Daemon and how to find the daemons on a virtual machine? I've looked up a lot of information on the Internet for the specific definition of Daemon. I got the following definition from wikipedia. In multitasking computer operating systems, a daemon is a computer program that runs as a background process, rather than being under the direct control of an interactive user. Traditionally, the process names of a daemon end with the letter *d*, for clarification that the process is, in fact, a daemon, and for differentiation between a daemon and a normal computer program. However, when I searched on the Internet how to find the daemons on a Linux machine, there were quit a few answers, but none was appropriate. Some said a daemon must has a ppid with the value of 1, others said this is not necessary. I was definitely confused by the appropriate answers from the Internet.

#### Working Plan For Next Week

* Finish the APIs of getting the resource information of the server and the virtual machine.
* Set up the Web server and get the resource information from the ZooKeeper server.
* Finish the coding of the front-end pages and the coding of dealing with the resource requests from the front-end to the Web server.
* Optimize the structure and the function encapsulation of the system.
* Add to some other useful functions to the system.



