+++
title = "Operating Systems - Coordination Problems"
author = ["eo shiru"]
date = 2019-06-05T10:00:00+02:00
lastmod = 2019-07-03T10:07:43+02:00
tags = ["uni", "os"]
draft = false
+++

Coordination mechanisms and techniques can solve a lot of problems like guaranteeing data consistency when cooperating (guarding critical sections), managing exclusive ressource access etc. However new problems may occur when employing coordination mechanisms:

-   priority inversion
-   starving (verhungern)
-   deadlock (verklemmen)


## Priority Inversion {#priority-inversion}

In the case of priority based scheduling a process with higher priority may be blocked by a process with lower priority, for example:

-   low-prio process \\(P\_L\\) enters a critical section
-   high-prio process \\(P\_H\\) gets ready to execute and tries the same
-   \\(P\_H\\) is blocked

Now if a process with medium priority \\(P\_M\\) suspenses the low-prio process \\(P\_L\\) the blocking/stopping of \\(P\_H\\) may continue.

-   multiple medium-prio processes may take over each other (abloesen)

This is known as unlimited priority inversion and leads to performance problems.


## Deadlock vs Starvation {#deadlock-vs-starvation}

**Deadlock**

-   no process participates in the scheduling process
-   static situation
-   no forward resolution (Vorwaertsaufloesung)
-   no (inner) progress: processes don't move forward

**Starvation**

-   processes continue to participate in the scheduling process
-   dynamic situation
-   forward resolution is possible
-   no (outer) progress: process doesn't move beyond a certain point

The problem of starvation can be solved by breaking the dynamic symmetry by eg randomization. We focus on (dead)locks for now.


## Deadlock {#deadlock}

A **deadlock** is a situation in which none of the involved processes can continue to execute, e.g:<br />
![](/knowledge-database/images/deadlock-example.png)

An illustrative example of this is that of the dining philosophers (Dijkstra): 5 philosophers sit in an italian restaurant, eat spaghetti and think. They have 5 forks and to eat one needs 2 forks. If everyone takes one fork all 5 forks are in one hand each and nobody can eat and they will wait forever &rarr; deadlock.

In context of operating systems resources the following criteria (_Coffman Conditions_) are needed for a deadlock:

-   resource(s) is/are used exclusively
-   processes already hold/occupy some resource while waiting for another resource
-   suspension doesn't happen

Now if in this situation the following happens, the last coffman condition for a deadlock is met:

-   there are cyclic (waiting) dependencies

Note: Condition 1-3 are system design dependant, while condition 4 is something that may arise during run time.


### Deadlock Countermeasures {#deadlock-countermeasures}

-   prevention (Vorbeugung)
-   detection (Entdeckung)
-   avoidance (Vermeidung, Verhinderung)
-   resolution, recovery (Aufloesung)


#### Deadlock Prevention {#deadlock-prevention}

-   prevention = preventive procedure where the resource distribution is realized in a way where deadlocks cannot occur
-   **preclaiming** (Summenbelegung): all ever needed ressources are requested upfront

{{< figure src="/knowledge-database/images/preclaiming.png" >}}

Preclaiming implicates total release of all resources (Totalfreigabe) at/before every (re-)occupation (Neubelegung) or resource request. This perforates the Coffman condition "hold & wait". This is how things would go in case of the dining philosophers:<br />
![](/knowledge-database/images/total-release.png)<br />
&rarr; Deadlock won't occur, but cycles without progress may occur &rarr; starvation (livelock)

Another countermeasures to prevent deadlocks is ordered allocation of resources which means access to resources is sorted and resources may only be requested in this order. This breaks the cyclicality from Coffman Condition 4<br />
![](/knowledge-database/images/ordered-allocation.png)<br />

All in all preventing measures only work in certain conditions and are rather impractical in real life scenarios, that's why they are used rarely.


#### Deadlock Detection {#deadlock-detection}

If a deadlock cannot be prevented per se, it is advantageous to detect the occurance of a deadlock. We'll look at deadlock detection algorithms.<br />
Informally: There's an order in which all process can come to an end &rarr; no deadlock

A detection algorithm has to account for _all_ processes and cann be called..

-   at each occupation / resource request / allocation
-   periodically
-   in the system idle process (Leerlaufprozess)
-   when suspicious (manually)

**Formal Deadlock Definition**<br />
The next slides, slide 19 to slide 33, provide a formal description of deadlocks. These are very hard to convert into this blog format so check them out in the [slides](https://osg.informatik.tu-chemnitz.de/lehre/os/bs-10-Deadlock-handout%5Fde.pdf).


#### Deadlock Avoidance {#deadlock-avoidance}

-   a deadlock regards the _current_ allocation/occupation situation
-   _before_ carrying out an allocation request a check is done and the request might get denied
-   most unfavorable situation: running process requests all outstanding resources (laufender  Prozess stellt komplette Restforderungen)
    -   if all of these demands can be met, the situation is still safe/secure, else the situation is unsafe/unsecure
        -   an unsafe/unsecure resource situation is characterized by the circumstance that there's a subset of processes whose outstanding (resource) request cannot be fullfilled (sooner or later)
        -   current requests might be fullfillable, however a deadlock may occur if the ordering of requests and releases is not optimal

Example of two processes and two resources:<br />
![](/knowledge-database/images/trajectory-1.png)

-   occupation trajectory of two processes \\(P\_1\\) and \\(P\_2\\) which both require the resources A and B
-   when both resources are differently assigned/allocated the situation is unsafe
    -   no deadlock if lucky
    -   guaranteed deadlock if unlucky
-   secure trajectories avoid a deadlock

{{< figure src="/knowledge-database/images/trajectory-1.png" >}}

Formal Definition of safe situations:<br />
![](/knowledge-database/images/safe-situations.png)

Definition safe set of processes: A set of processes \\(P = {P\_1, P2, ..., P\_m}\\) is _safe_ when \\(\exists\\) permutation \\(P\_{k1}, P\_{k2}, ..., P\_{km} \text{with} \overrightarrow{g}\_{k1} - \overrightarrow{b}\_{k1} \text{and} \forall j \in {2, ..., m}, \overrightarrow{g}\_{kj} - \overrightarrow{b}\_{kj} \leq \overrightarrow{f} + \sum\_{i=1}^{j-1}\overrightarrow{b}\_{ki}\\)

The states "safe/secure" and "deadlock free" are really similar.

-   in case of a "deadlock free" situation a permutation is searched, which can be executed under all current occupations/allocation requests
-   in case of a "safe/secure" situation the same is done for the **outstanding requests** (Restforderungen) \\(R= G - B\\)
-   algorithms to detect deadlocks can also be used to avoid deadlocks
-   the matrix alogrithm by Dijkstra which is also known as Banker's algorithm is used to prevent deadlocks
    -   slides: es muessen lediglich die aktuellen Anforderungen durch die Restforderungen ersetzt werden; Problem: Restanforderungen sind i.d.R. nicht genau bekannt
    -   the Banker's algorithm is executed at each allocation and the situation that _would arise when granting_ the request is evaluated
        -   if the resulting situation is safe, the allocation request is allowed else it is put back

{{< figure src="/knowledge-database/images/bankers-algorithm.png" >}}


### Deadlock Resolution/Recovery {#deadlock-resolution-recovery}

-   every resolution of a deadlock consists of breaking the waiting cycle
-   if an ordered resource withdrawal (BM-Entzug) is not possible, the **abortion** (Abbruch) of a process is the only option
    -   question: which process should be cancelled?
    -   criteria:
        -   requested size
        -   urgency/priority
        -   user vs system process
        -   etc....
