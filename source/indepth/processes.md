---
title: Process management
section: indepth
---
## About processes

<p class="lead">Phusion Passenger manages multiple processes in order to maximize stability and performance. Learn what processes are and how they behave.</p>

### What are processes?

An instance of an application is called a **process**. Passenger takes care of starting and stopping your application for you. Every time Passenger starts an instance of your application, it is said that an application process is spawned. Every time Passenger stops an instance of your application, it is said that an application process is shut down.

You may also have heard of the term **"thread"**, but threads should not be confused with processes. Threads run *inside* a process, so a process always contains one or more threads. Threads and processes have distinct characteristics.

## Characteristics and caveats

### Memory isolation

A process is *isolated* from other processes. "Isolated" means that processes don't share memory with each other. Suppose that your application has a variable `A` with initial value `A = 1`. If you run two instances of your application -- two processes -- and you tell one process to set `A = 2`, then the value `2` is only visible to that process. The other process still thinks `A == 1`!

### Sharing data between processes

You can't change variables in your program and expect all processes to see the changes. They won't. So how do you communicate changes to all your processes? The answer is by using a shared data store, such as:

 * The database.
 * Redis.
 * Memcached.

### Crash protection

If a process crashes, other processes do not crash along with it. An application crash won't take down Passenger because Passenger runs in its own process. Even Passenger itself is implemented as multiple processes, so that Passenger can restart itself when Passenger crashes.

### Accountabilty

Because processes are isolated from each other memory-wise, it's very easy to find out how much memory a process is using. You can't do that with threads because they all share memory. A very good analogy is a house shared by multiple tenants. If you visit that house, you can't tell what stuff belongs to who. Some stuff may even be owned by multiple people.

Being able to hold processes accountable means that you can restart a process if it starts to become problematic, e.g. when it's using too much memory.

## Further reading

 * [Unix Process Management -- Tutorialspoint](http://www.tutorialspoint.com/unix/unix-processes.htm)
 * [UNIX Process Overview -- The Geek Stuff](http://www.thegeekstuff.com/2012/02/unix-process-overview/)
