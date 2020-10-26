---
layout: post
title:  "ExecutorService note"
date:   2020-10-22 14:46:18 +0800
categories: Java
---

{% include mermaid.html %}

# Table of contents
- [Table of contents](#table-of-contents)
- [What is ExcutorService](#what-is-excutorservice)
- [How to termination of ExecutorService](#how-to-termination-of-executorservice)

# What is ExcutorService

ExcutorService is an interface that provides methods to manage termination and methods that can produce a Future for tracking progress of one or more asynchronous tasks.

{% highlight java %}
ExcutorService executorService = Executors.newFixedThreadPool(10);
for (int i = 0; i < 10; i++){
	executorService.execute(new Runnable() {
		@Override
		public void run() {
			System.out.println(Thread.currentThread().getName() + " is here!");
		}
	});
}
executorService.shutdown();

// The "thread order" may be different, because it's asynchronous.
// pool-1-thread-1 is here!
// pool-1-thread-2 is here!
// pool-1-thread-4 is here!
// pool-1-thread-3 is here!
// pool-1-thread-5 is here!
// pool-1-thread-6 is here!
// pool-1-thread-7 is here!
// pool-1-thread-8 is here!
// pool-1-thread-9 is here!
// pool-1-thread-10 is here!
{% endhighlight %}

# How to termination of ExecutorService

ExecutorService provides two termination methods. Once the termination method is called, ExecutorService will not accept any new task.

the detail of this two Method in Java docs

* shutdown()
  * Initiates an orderly shutdown in which previously submitted tasks are executed.
* shutdownNow()
  * Attempts to stop all actively executing tasks, halts the processing of waiting tasks, and returns a list of the tasks that were awaiting execution. <br><br> There are no guarantees beyond best-effort attempts to stop processing actively executing tasks. For example, typical implementations will cancel via Thread.interrupt(), so any task that fails to respond to interrupts may never terminate.

The following method shuts down an ExecutorService in two phases, first by calling shutdown to reject incoming tasks, and then calling shutdownNow, if necessary, to cancel any lingering tasks:

{% highlight java %}
 void shutdownAndAwaitTermination(ExecutorService pool) {
   pool.shutdown(); // Disable new tasks from being submitted
   try {
     // Wait a while for existing tasks to terminate
     if (!pool.awaitTermination(60, TimeUnit.SECONDS)) {
       pool.shutdownNow(); // Cancel currently executing tasks
       // Wait a while for tasks to respond to being cancelled
       if (!pool.awaitTermination(60, TimeUnit.SECONDS))
           System.err.println("Pool did not terminate");
     }
   } catch (InterruptedException ie) {
     // (Re-)Cancel if current thread also interrupted
     pool.shutdownNow();
     // Preserve interrupt status
     Thread.currentThread().interrupt();
   }
 }
{% endhighlight %}

