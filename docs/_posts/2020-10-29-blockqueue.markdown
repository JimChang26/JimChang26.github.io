---
layout: post
title:  "BlockQueue note"
date:   2020-10-29 16:19:18 +0800
categories: Java
---

{% include mermaid.html %}

**Table of contents**
- [What is BlockQueue](#what-is-blockqueue)

# What is BlockQueue

A Queue that additionally supports operations that wait for the queue to become non-empty when retrieving an element, and wait for space to become available in the queue when storing an element.

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