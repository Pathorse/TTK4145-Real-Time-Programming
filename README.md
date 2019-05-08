# TTK4145-Real-time Programming
<meta name ="author" content="Paal A. S. Thorseth">

**Below you find notes regarding important topics in Real-time Programming. The topics are based on relevant exams for TTK4145 at NTNU.**

## List of topics
1. [Topic 1 - *Fault tolerance*](#of1)
2. [Topic 2 - *Acceptance tests*](#of2)
3. [Topic 3 - *Real-Time Programming*](#of3)
4. [Topic 4 - *Synchronization*](#of4)



<a name="of1"></a>
## Topic 1 - Fault tolerance

**Fault tolerance** is the property that enables a system to continue operating properly in the event of the failure of (or one or more faults within) some of its components. If its operating quality decreases at all, the decrease is proportional to the severity of the failure, as compared to a naively designed system, in which even a small failure can cause total breakdown. Fault tolerance is particularly sought after in high-availability or life-critical systems. The ability of maintaining functionality when portions of a system break down is referred to as **graceful degradation**.

A **fault-tolerant design** enables a system to continue its intended operation, possibly at a reduced level, rather than failing completely, when some part of the system fails. The term is most commonly used to describe *computer systems* designed to continue more or less fully operational with, perhaps, a reduction in throughput or an increase in response time in the event of a partial failure. That is, the system as a whole is not stopped due to problems in either *hardware* or *software*. *Software brittleness* is the oppositve of *robustness*. *Resilient Networks* continue to transmit data despite the failure of some links or nodes.

A system with high **failure transparency** will alert users that a component failure has occured, even if it continues to operate with full performance, so that failure can be repaired or imminent complete failure anticipated.

Within the scope of an *individual system*, fault tolerance can be achieved by anticipating exceptional conditions and building the system to cope with them, and, in general, aiming for **self-stabilization** so that the system converges towards an error-free state. However, if the consequences of a system failure are catastrophic, or the cost of making it sufficiently reliable is very high, a better solution may be to use some form of duplication. In any case, if the consequence of a system failure is so catastrophic, the system must be able to use reversion to fall back to a safe mode.


Below you find a number of choices to be examined to determine which components should be fault tolerant:
- **How critical is the component?** In a car, the radio is not critical, so this component has less need for fault tolerance.
- **How likely is the component to fail?** Some components, like the drive shaft in a car, are not likely to fail, so no fault tolerance is needed.
- **How expensive is it to make the component fault tolerant?** Requiring a redundant car engine, for example, would likely be too expensive both economically and in terms of weight and space, to be considered.

### Requirements
The basic characteristics of fault tolerance require:
1. **No single point of failure** - If a system experiences a failure, it must continue to operate without interruption during the repair process.
2. **Fault isolation to the failing component** - When a failure occurs, the system must be able to isolate the failure to the offending component. This requires the addition of dedicated failure detection mechanisms that exist only for the purpose of fault isolation. Recovery of a fault condition requires classifying the fault or failing component.
3. **Fault containment to precent propagation of the failure** - Some failure mechanisms can cause a system to fail by propagating the failure to the rest of the system.
4. **Availability of reversion modes**



<a name="of2"></a>
## Topic 2 - Acceptance tests

In engineering and its various subdisciplines **acceptance testing** is a test conducted to determine if the requirements of a specification or contract are met. 

In *software testing* the ISTQB(International Software Testing Qualifications Board) defines **acceptance testing** as:

>Formal testing with respect to user needs, requirements, and business processes conducted to determine whether or not a system satisfies the acceptance criteria and to enable the user, customers or other authorized entity to determine whether or not to accept the system.


### Types of acceptance testing
- **User acceptancte testing - UAT**
    - This may include factory acceptance testing (FAT), i.e. the teseting done by a vendor before the product or system is moved to its destination site, after which site acceptance testing (SAT) may be preformed by the users at the site.
- **Operational acceptance testing - OAT**
    - Also known as operational readiness testing, this refers to the chechking done to a system to ensure that processes and procedures are in place to allow the system to be used and maintained. This may include checks done to back-up facilities, procedures for disaster recovery, training for end users, maintenance procedures, and security procedures. 
- **Contract and regulation acceptance testing**
    - In contract acceptance testing, a system is tested against acceptance criteria as documented in a contract, before the system is accepted. In regulation acceptance testing, a system is tested to ensure it meets governmental, legal and safety standards.

### Notes based on answers for exam questions

**Fault tolerance** does not require the system to be fault free. We use **acceptance testing** for detecting whether anything is wrong, not to identify *any fault*.

**Learn-by-heart list from the book - Examples of what one can test for when making acceptance tests**
- Replication checks
- Timing checks
- Reversal checks
- Coding checks
- Reasonableness checks
- Structural checks
- Dynamic Reasonableness checks



<a name="of3"></a>
## Topic 3 - Real-Time Programming

In *computer science*, **real-time computing (RTC)**, or **reactive computing** describes hardware and software systems subject to a "real-time constraint", for example fomr event to system response. **Real-time programs** must guarantee response within specified time constraints, often referred to as "deadlines". The correctness of these types of systems depends on their temporal aspects as well as their functional aspects. **Real-time responses** are often understood to be in the order of milliseconds, and sometimes microseconds. A system not specified as operating in real time cannot usually *guarantee* a response within any timeframe, although *typical* or *expected* response times may be given.

**Real-time software** may use one or more of the following:
- *Synchronous programming languages*
- *Real-time operating systems*
- *Real-time networks*
each of which provide essential frameworks on which to build a real-time software application. 

System used for *mission critical* applications must be real-time, such as for control of fly-by-wire aircraft, or anti-lock brakes on a vehicle, which must produce maximum deceleration but intermittently stop braking to prevent skidding.

**Real-time systems**, as well as their deadlines, are classified by the consequence of missing a deadline:
- *Hard* - missing a deadline is a total system failure.
- *Firm* - infrequent deadline misses are tolerable, but may degrade the system's quality of service. The usefulness of a result is zero after its deadline.
- *Soft* - the usefulness of a result degrades after its deadline, thereby degranding the system's quality of service.

### Notes based on answers for exam questions

**Priorities** are very important in real-time programming to be able to reason on timing/execution behaviour of our program and/or to make schedulability proofs, we need predictability. Priorities is what make us able to predict which thread is running in any given situation.

Making a **upper bound of execution time** relates both to design and estimates.
- *Design*
    - No recursion
    - No algorithms with undeterminable execution time
    - No unbounded size data structures nor dynamic datastructures at all
    - No unbounded input data dependencies
- *Estimation* 
    1. Having sequences of predictable time assembly instructions enclosed by looping with known max bounds which means we can multiply and sum.
    2. We can run the system at a worstcase scenario, measure time of execution and add some buffer to ensure a safe *uppder bound*.

The consequences of *not being able to tell the timing* from code is terrible in a maintenance perspective, yielding the need for a re-analysis of the whole system to ensure that executions are within given time frames. An update could in the worst case lead to worse timing behaviour than previously. 



<a name="of4"></a>
## Topic 4 - Synchronization

In *computer science*, **synchronization** refers to one of two distinct but related concepts: **synchronization of processes**, and **synchronization of data**.
> **Process synchronization** refers to the idea that multiple processes are to join up or *handshake* at a certain point, in order to reach an agreement or commit to a certain sequence of action.

> **Data synchronization** refers to the idea of keeping multiple copies of a dataset in coherence with one another, or to maintain data integrety.
**Process synchronization** primitives are commonly used to implement **data synchronization**.

### Thread or process synchronization
**Thread synchronization** is defined as a mechanism which ensures that two or more concurrent processes or threads do not simultaneously execute some particular program segment known as *critical section*(TODO REF CONCURRENT). Processes' access to *critical section* is controlled by using synchronization techniques. When one thread start executing the *critical section* (serialized segment of the program) the other thread should wait until the first thread finishes. If proper synchronization techniques are not applied, it may cause a *race condition*(REF TODO) where the values of variables may be unpredictable and vary depending on the timings of *context switches* of the processes or threads.

For example, suppose that there are three processes, namely 1,2, and 3. All three of them are concurrently executing, and they need to share a common resource(critical section) as shown in Figure 1 ![alt text](https://github.com/Pathorse/TTK4145-Real-Time-Programming/blob/master/Images/Multiple_Processes_Accessing_the_shared_resource.png "Figure 1: Three processes accessing a shared rescource (critical section) simulataneously."). Synchronization should be used here to avoid any conflicts for accessing this shared resource. Hence, when Process 1 and 2 both try to access that resource, it should be assigned to only one process at a time. If it is assigned to Process 1, the other process (Process 2) needs to wait until Process 1 frees that resource, as shown in Figure 2 ![alt text](https://github.com/Pathorse/TTK4145-Real-Time-Programming/blob/master/Images/Shared_Resource_access_in_synchronization_environment.png "Figure 2: A process accessing a shared resource if available, based on some synchronization technique.").

Another **synchronization** requirement which needs to be considered is the order in which particular process or threads should be executed. For example, we cannot board a plane until we buy a ticket. Similarly, we cannot check e-mails without validating our credentials. In the same way, an ATM will not provide any service until the correct PIN has been entered. 

Other than mutual exclusion, synchronization also deals with the following:
- **Deadlocks**, which occurs when many processes are waiting for a shared resource (critical section) which is being held by some other process. In this case, the processes just keep waiting and execute no further.
- **Starvation**, which occurs when a process is waiting to enter the critical section, but other processes monopolize the critical section, and the first process is forced to wait indefinitely.
- **Priority inversion**, which occurs when a high-priority process is in the critical section, and it is interrupted by a medium-priority process. This violation of priority rules can happen under certain circumstances and may lead to serious consequences in **real-time systems**.
- **Busy waiting**, which occurs when a process frequently polls to determine if it has access to a critical section. This frequent polling robs processing time from other processes.


### Semaphores
**Semaphores** are signalling mechanisms which can allow one or more processes/threads to access a section. A **semaphore** has a flag which has a certain fixed value associated with it and each time a thread wishes to access the section, it decrements the flag. Similarly, when the thread leaves the section, the flag is incremented. If the flag is zero, the thread cannot access the section and gets blocked if it chooses to wait.

Some **semaphores** would allow only one thread or process in the code section. Such **semaphores** are called **binary semaphore** and are very similar to **mutex**(todo referanse). I.e. if the value of **semaphore** is 1, the thread is allowed to access and if the value is 0, the access is denied.

### Notes based on answers for exam questions


Written by Paal Arthur Schjelderup Thorseth


### TODO
- concurrency
    - mutual exclusion
    - race conditions
    - critical section