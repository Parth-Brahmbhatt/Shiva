#Project Goal
To provide a framework that allows developer to test failure scenarios of distributed systems in a simple, configurable
repeatable way. 

#Problem description
There has been a boom in the development of distributed system since Apache Hadoop to solve a multitude of problems. However,
there is a lack/absence of a test framework that can allow developers to test how these systems react under different failure 
scenarios. Each system has to either reinvent the wheel by writing a framework that is catered to their specific use case or
they live with a non scalable manual testing plan. 

With this project we want to allow the developers to easily run the common failure scenarios on their systems. The initial
version will focus on following failure scenario:

* CPU hogging 
* Memory hogging
* Network hogging and partition
* Complete host failures
* Disk failure
* Brownouts
* Process failures

# Design
We want the users to take the following steps, we will create an API for each of this operation:
* Define a cluster.
* Define/Choose attacks.
* Launch attacks on cluster.
* Get attack status from the cluster.

Given the kind of attacks we want to launch we will need some process running on all the cluster hosts with super user permissions.
These processes can either poll to get the attack information from a central server or we can push the attack information to
these hosts as part of launch-attack operation. 

Following are components that can be configured by the user:
* Host: A host will have an identity (ip, hostname) and additional tags,i.e. Data center, Masters.
* Cluster: A cluster is schema of your system. Primarily it will be made of List of hosts.
* Attack: An attack defines the failure characteristics you want to introduce to your cluster. There are some commonalities 
among all kind of attacks like, what % of fleet should be attacked or what hosts should be attacked, how long the attack should continue to execute. 

##Classes
```scala
class Host(identity: HostIdentity, tags: List[Tag])

class Cluster(name: String, hosts: List[Host])

class Attack(name: String, runForSecs: Long)
```
