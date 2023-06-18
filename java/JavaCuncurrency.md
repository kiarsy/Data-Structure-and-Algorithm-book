- [Basics](#basics)
  - [Race Condition](#race-condition)
  - [Dead Lock](#dead-lock)
  - [Volatile Keyword](#volatile-keyword)
  - [Thread Scheduler](#thread-scheduler)
  - [Thread Priority](#thread-priority)
  - [.yield()](#yield)
  - [.sleep(timeout)](#sleeptimeout)
  - [.wait(\[timeout\]),notify(),notifyAll()](#waittimeoutnotifynotifyall)
  - [.join(\[timeout\])](#jointimeout)
  - [.interrupt()](#interrupt)
- [Thread-Safe](#thread-safe)
  - [Synchronized Keyword (intrinsic lock)](#synchronized-keyword-intrinsic-lock)
  - [Lock Interface](#lock-interface)
    - [ReentrantLock](#reentrantlock)
    - [ReentrantReadWriteLock](#reentrantreadwritelock)
    - [StampedLock](#stampedlock)
    - [Working With Conditions](#working-with-conditions)
  - [Semaphore](#semaphore)
  - [Mutex](#mutex)

# Basics

![](https://www.uml-diagrams.org/examples/state-machine-example-java-6-thread-states.png)

![](./images/ThreadStates.png)

## Race Condition
- Race condition in Java is a type of concurrency bug or issue that is introduced in your program because of parallel execution of your program by multiple threads at the same time, Since Java is a multi-threaded programming language hence the risk of Race condition is higher in Java which demands a clear understanding

For example, if thread A is reading data from the linked list and another thread B is trying to delete the same data. This process leads to a race condition that may result in run time error.

- when two threads simultaneously update the same value, as a consequence, leave value in undesirable or inconsistent sate
  
## Dead Lock

It is a situation when a thread that hold a lock and is waiting on a lock that another thread holds, but the other thread in waiting for the lock that first thread holds.

## Volatile Keyword
![](https://jenkov.com/images/java-concurrency/java-volatile-1.png)


## Thread Scheduler
Scheduler in JVM implementation usually employ one of two following strategies:
1. Preemptive scheduling: when another thread with higher priority comes, current thread goes to ready state
2. Time-Sliced or Round-Robin scheduling.

**Note** : the implementation of Scheduler is platform dependent.

## Thread Priority
- Thread.MaxPriority : 10
- Thread.MinPriority : 0
- Default : 5
  
- getPriority and setPriority for controlling priority.

## .yield()

It change thread state to `ready` to run in future.

## .sleep(timeout)


goes to run ready state

## .wait([timeout]),notify(),notifyAll()

![](./images/java-thread-waiting.png)

- if we specify timeout on wait, we cannot understand if timed out or woken up by one of notification methods.
- lock will be released in this thread, if the lock is synchronized only, other lock mechanism does not work this way.

## .join([timeout])

- join caller will be blocked till the thread is completed.
  

## .interrupt()

- only works on blocking functions wait, sleep
- not work on synchronize block
# Thread-Safe

## Synchronized Keyword (intrinsic lock)

- it called `synchronized lock` , `Monitor`
- it use `wait` and `notify` under the hood
- can be used on all objects
- when we use synchronized keyword on a method, it is like `synchronize(this)`
- when we use synchronized keyword on a static method, it is like `synchronize(CLASS.class)`
- if thread can not acquire the lock immediately it is `blocked` otherwise it continue running normally

- A synchronized block doesn't support the fairness. Any thread can acquire the lock once released, and no preference can be specified. We can achieve fairness within the Lock APIs by specifying the fairness property. It makes sure that the longest waiting thread is given access to the lock.
- A thread that is in “waiting” state to acquire the access to synchronized block can't be interrupted. The Lock API provides a method lockInterruptibly() that can be used to interrupt the thread when it's waiting for the lock.


## Lock Interface
[Article A](https://www.baeldung.com/java-concurrent-locks)


- More flexible 
- support multiple associated Condition objects
- fairness possible
- possible to make a thread responsive to interruption while waiting .LockInterruptibly()
- possible to try to acquire lock, but return immediately or after a timeout.
- possible to acquire and release locks different scopes
- releasing synchronization must happen in same order that acquire happened in the same scope
- lock, we can release in any order or any scope cause it is an variable

### ReentrantLock

- Construction(bool fairness)
- 
### ReentrantReadWriteLock
### StampedLock

### Working With Conditions
- Conditions have same use case as wait,notify,notifyAll
- await(), signal(),signalAll

## Semaphore
- let multiple threads use
- does not have condition

## Mutex
- Every lock mechanism is mutex