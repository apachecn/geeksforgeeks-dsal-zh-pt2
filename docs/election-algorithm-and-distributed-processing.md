# 选举算法和分布式处理

> 原文:[https://www . geesforgeks . org/election-algorithm-and-distributed-processing/](https://www.geeksforgeeks.org/election-algorithm-and-distributed-processing/)

**分布式算法**是在分布式系统上运行的算法。分布式系统是不共享内存的独立计算机的集合。每个处理器都有自己的内存，它们通过通信网络进行通信。网络中的通信是在一台机器上的进程与另一台机器上的进程通信时实现的。分布式系统中使用的许多算法需要一个协调器来执行系统中其他进程所需的功能。**选举算法**旨在选择协调者。

**选举算法:**
选举算法从一组处理器中选择一个进程作为协调器。如果协调器进程由于某些原因崩溃，则在其他处理器上选举一个新的协调器。选举算法基本上决定了协调器的新副本应该在哪里重新启动。

选举算法假设系统中的每个活动进程都有一个唯一的优先级号。优先级最高的流程将被选为新的协调员。因此，当协调器出现故障时，该算法会选择优先级最高的活动进程。然后这个数字被发送到分布式系统中的每个活动进程。

对于分布式系统的两种不同配置，我们有两种选举算法。

**1。欺负算法–**
该算法适用于每个进程都可以向系统中的其他进程发送消息的系统。

**算法–**假设进程 P 向协调器发送消息。

1.  如果协调器在时间间隔 T 内没有响应，则认为协调器已经失败。
2.  现在进程 P 用高优先级数字向每个进程发送选举消息。
3.  它等待响应，如果在时间间隔 T 内没有人响应，那么进程 P 选择自己作为协调者。
4.  然后，它向所有优先级较低的进程发送消息，表明它被选为它们的新协调器。
5.  然而，如果在时间 T 内从任何其他进程 Q 接收到答案，
    *   (1)进程 P 再次等待时间间隔 T’从 Q 接收另一个消息，表明它已被选为协调器。
    *   (二)如果 Q 在时间间隔 T '内没有响应，则认为失败，重新启动算法。

**2。环算法–**
该算法适用于组织成环的系统(逻辑上或物理上)。在这个算法中，我们假设进程之间的链接是单向的，每个进程只能向它右边的进程发送消息。该算法使用的数据结构是**活动列表**，该列表具有系统中所有活动进程的优先级。

**算法–**

1.  如果进程 P1 检测到协调器故障，它会创建新的活动列表，该列表最初为空。它向右边的邻居发送选举信息，并将数字 1 添加到其活动列表中。
2.  如果进程 P2 从左边的进程接收到消息 elect，它将以 3 种方式响应:
    *   (I)如果收到的消息在活动列表中不包含 1，则 P1 会将 2 添加到其活动列表中并转发该消息。
    *   (二)如果这是 P1 收到或发送的第一条选举信息，它将创建一个新的活动列表，编号为 1 和 2。然后，它发送选举消息 1，然后是 2。
    *   (三)如果 P1 进程收到自己的选举消息 1，则 P1 的活动列表现在包含系统中所有活动进程的编号。现在，P1 进程从列表中检测出最高优先级的编号，并将其选为新的协调员。