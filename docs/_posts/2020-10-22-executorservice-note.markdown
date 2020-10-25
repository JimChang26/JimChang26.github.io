---
layout: post
title:  "ExecutorService note"
date:   2020-10-22 14:46:18 +0800
categories: Java
---

{% include mermaid.html %}

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

ExcutorService has two methods for shutdown all threads.
{% highlight java %}
//shutdown() method will wait all tasks are executed before terminating
executorService.shutdown();
//shutdownNow() method will terminat
executorService.shutdownNow()
{% endhighlight %}



# How to termination of threads

ExecutorService provides two termination methods. Once the termination method is called, ExecutorService will not accept a new task.

* shutdown()
  * terminate when task are done.
* shutdownNow()
