#论文笔记

This repo hopes to record the process of reading the papers. Some of the papers are from the papers that need to be read in class. This part will be more secure and virtualized. There are still some papers that are of interest to you and you want to know. This part may be more virtual and distributed. The paper notes hope to be able to record their thoughts when reading the paper, including but not limited to the general idea of ​​the paper, the way it is implemented, and its own evaluation of the paper. I hope to limit the notes of each paper to less than 1000 words.

** Currently no longer maintained as a Markdown file, go to the [issue page] (https://github.com/gaocegege/papers-notebook/issues) and welcome to [this issue] (https:// Github.com/gaocegege/papers-notebook/issues/1) Share paper** that you think is worth reading

## 目录 (TOC)

* [Distributed System] (#distributed distributed-system)
    * [Scheduler] (#scheduler scheduler)
      * [Mesos](#mesos)
      * [Omega](#omega)
      * [Borg](#borg)
      * [Yarn](#yarn)
      * [Sparrow](#sparrow)
      * [Apollo](#apollo)
      * [Hawk](#hawk)
      * [Mercury](#mercury)
      * [Firmament](#firmament)
      * [ERA](#era)
      * [Efficient Queue Management for Cluster Scheduling] (#efficient-queue-management-for-cluster-scheduling)
      * [Tarcil](#tarcil)
      * [Eagle](#eagle)
      * [Canary](#canary)
      * [Profiling a warehouse-scale computer](#profiling-a-warehouse-scale-computer)
    * [Graph Computation](#graph-computation)
      * [Wukong](#wukong)
    * [Lock Service](#lock-service)
      * [Chubby](#chubby)
    * [Consensus] (#consistency consensus)
      * [Raft](#raft)
      * [Zookeeper](#zookeeper)
      * [Paxos](#paxos)
    * [Storage] (#Storage storage)
      * [BigTable](#bigtable)
      * [Dynamo](#dynamo)
      * [Spanner](#spanner)
      * [Distributed Transaction with RDMA and HTM](#distributed-transaction-with-rdma-and-htm)
      * [Key-Value Store with RDMA](#key-value-store-with-rdma)
      * [RDF Store with RDMA](#rdf-store-with-rdma)
      * [Ambry](#ambry)
* [Virtualization] (#virtualization)
    * [virtual machine manager (hypervisor)] (# virtual machine manager hypervisor)
      * [Xen](#xen)
      * [kvm](#kvm)
    * [Container] (#container container)
      * [mbox](#mbox)
      * [Slacker](#slacker)
* [Sandboxing] (# sandbox sandboxing)
    * [System Call Interposition] (# system call intercept system-call-interposition)
      * [Janus](#janus)
      * [Ostia](#ostia)
    * [Software-based Fault Isolation] (#software-based-fault-isolation)
      * [SFI](#sfi)
      * [Google Native Client](#google-native-client)
      * [Language-Independent Sandboxing](#language-independent-sandboxing)
* [System] (#system system)
    * [File System] (# file system file-system)
      * [RAMCloud](#ramcloud)
      * [Optimistic Crash Consistency](#optimistic-crash-consistency)
      * [F2FS](#f2fs)
      * [PMFS](#pmfs)
    * [Operating System] (# operating system operating-system)
      * [Exokernel](#exokernel)
    * [Memory](#memory)
      * [Transactional Memory](#transactional-memory)
    * [CFI](#cfi)
      * [Control-Flow Integrity](#control-flow-integrity)
    * [Tail Latency](#tail-latency)
      * [The Tail at Scale](#the-tail-at-scale)
    * [Lock](#lock)
      * [Non-scalable locks are dangerous](#non-scalable-locks-are-dangerous)
    * [Bug](#bug)
      * [STACK](#stack)
* [Security] (#security security)
    * [virtulization, security] (#virtual machine security virtulization-security)
      * [CloudVisor](#cloudvisor)
    * [Taint Tracing](#taint-tracing)
      * [TaintDroid](#taintdroid)
    * [ROP](#rop)
      * [Hacking Blind](#hacking-blind)
* [Big Data] (#Big Data)
    * [framework] (#framework)
      * [Hadoop](#hadoop)
      * [Spark](#spark)
    * [Data Processing](#data-processing)
      * [Realtime Data Processing at Facebook](#realtime-data-processing-at-facebook)
* [network] (# network)
    * [Network Function Virtualization(NFV)](#network-function-virtualizationnfv)
      * [Click](#click)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)


## Distributed (Distributed System)

### Scheduler (Scheduler)

* [Comparison of Container Schedulers] (https://medium.com/@ArmandGrillet/comparison-of-container-schedulers-c427f4f7421)
* [The path to the evolution of the cluster scheduling framework] (http://www.infoq.com/cn/articles/scheduler-architectures)

In my opinion, distributed is a way of studying how programs can run better on multiple machines with better performance. If you want to achieve this, scheduling is critical.

The papers I have read about distributed schedulers are Mesos, Omega, Yarn and Borg. Among them, Mesos is the earliest, it comes from the University of Berkeley. The brightest part is the framework of two-tier scheduling, which makes the scheduling loosely coupled with the framework. Many companies are using it today, and there are many startups based on Mesos, such as Mesosphere. The second author of Omega and Mesos is a person. Omega does not know who wrote it. It should be considered as a study by the university and Google. Omega, published on EuroSys'13, is based on Mesos and proposes a fully parallel scheduling solution that delivers better performance in scheduling. However, the paper is a simulation experiment to verify, and I don't know if there is any production use. Borg is published on EuroSys'15 and is a cluster management tool that Google has been using all the time. It can be said that Google can use high-cost machines to achieve high availability, a large part is because of Borg. Borg and Omega are not open source, and Mesos is open source, but Borg has an open source successor, the current famous Kubernetes. Kubernetes is implemented using Docker Conatainer instead of the Linux kernel's features for performance-level isolation at the process level. However, Kubernetes seems to be tearing up with Docker recently, because some of Docker's strengths may not only support Docker Conatiner. Kubernetes is not production ready for a long time. It can only support 100 nodes. It is completely incomparable with Borg's 10K. I don't know what it is.

#### Mesos

* [Mesos: A Platform for Fine-Grained Resource Sharing in the Data Center] (https://people.eecs.berkeley.edu/~alig/papers/mesos.pdf)
* [Apache Mesos] (https://github.com/apache/mesos)

Mesos is a paper that the scheduler can't get around because it is one of the most widely used open source systems in the industry today. Mesos is very similar to the idea of ​​exokernel, separating management and protection. All previous schedulers are determined by themselves to give resources to a task. In mesos, the framework decides whether to accept the resource. On the disaster recovery, mesos is the leader election through the zookeeper, and the state maintained by the master is soft, so the master has no single point of failure, and for the node failure, it will be fed back to the framewo
