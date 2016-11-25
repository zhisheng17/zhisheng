# The volatile keyword in Java



*Topics covered include:*

 ![img](http://www.javamex.com/RightArrowBlue.gif) [Synchronized vs volatile](http://www.javamex.com/tutorials/synchronization_volatile.shtml#synchronized_volatile)

 ![img](http://www.javamex.com/RightArrowBlue.gif) [When to use volatile?](http://www.javamex.com/tutorials/synchronization_volatile_when.shtml)

 ![img](http://www.javamex.com/RightArrowBlue.gif) [Atomic updates of volatile fields](http://www.javamex.com/tutorials/synchronization_concurrency_7_atomic_updaters.shtml)

It's probably fair to say that on the whole, the volatile keyword in Java is poorly documented, poorly understood, and rarely used. To make matters worse, its formal definition actually changed as of Java 5. On this and the following pages, we will cut through this mess and look at what the Java volatile keyword does and when it is used. We will also compare it to other mechanisms available in Java which perform similar functions but under subtly different other circumstances.



### What is the Java volatile keyword?

Essentially, volatile is used to indicate that a **variable's value will be modified by different threads**.

Declaring a volatile Java variable means:

- The value of this variable will **never be cached thread-locally**: all reads and writes will go straight to "main memory";
- Access to the variable **acts as though it is enclosed in a synchronized block**, synchronized on itself.

We say "acts as though" in the second point, because to the programmer at least (and probably in most JVM implementations) there is no actual lock object involved. Here is how synchronized and volatile compare:



## Difference between synchronized and volatile



 ![QQ图片20161114234132](C:\Users\10412\Desktop\QQ图片20161114234132.png)



In other words, the main differences between synchronized and volatile are:

- a primitive variable may be declared volatile (whereas you can't synchronize on a primitive with synchronized);
- an access to a volatile variable **never has the potential to block**: we're only ever doing a simple read or write, so unlike a synchronizedblock we will never hold on to any lock;
- because accessing a volatile variable **never holds a lock**, it is **not suitable** for cases where we want to **read-update-write** as an atomic operation (unless we're prepared to "miss an update");
- a volatile variable that is an object reference may be null (because you're effectively synchronizing on the *reference*, not the actual object).

Attempting to synchronize on a null object will throw a NullPointerException.

### Volatile variables in Java 5

We mentioned that in Java 5, the meaning of volatile has been tightened up. We'll come back to this issue in a moment. First, we'll look at a typical [example of using volatile](http://www.javamex.com/tutorials/synchronization_volatile_typical_use.shtml). Later, we'll look at topics such as:

- the tighter [definition of *volatile* in Java 5](http://www.javamex.com/tutorials/synchronization_volatile_java_5.shtml);
- [atomic updates](http://www.javamex.com/tutorials/synchronization_concurrency_7_atomic_updaters.shtml) to volatile variables, useful in concurrent programming and possible as of Java 5;
- a summary of [when to use volatile](http://www.javamex.com/tutorials/synchronization_volatile_when.shtml), along with some [typical Java bugs](http://www.javamex.com/tutorials/synchronization_volatile_dangers.shtml) involving the volatile keyword.

------

comments powered by Disqus

**NOTE:** The original authentic version of this article is published on the Javamex web site. It has been ripped off on various blogs and sites such as scribd. If you are reading this article on any site other than [javamex.com](http://www.javamex.com/) then you are reading a copyright infringing version which may potentially be out of date.

*Article written by Neil Coffey (@BitterCoffey).*

