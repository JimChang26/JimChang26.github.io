---
layout: post
title:  "ExecutorService note"
date:   2020-10-22 14:46:18 +0800
categories: Java
---

{% include mermaid.html %}

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

// output
// pool-1-thread-1 is create!
// pool-1-thread-2 is create!
// pool-1-thread-4 is create!
// pool-1-thread-3 is create!
// pool-1-thread-5 is create!
// pool-1-thread-6 is create!
// pool-1-thread-7 is create!
// pool-1-thread-8 is create!
// pool-1-thread-9 is create!
// pool-1-thread-10 is create!
{% endhighlight %}

ExcutorService has two methods for shutdown all threads.
{% highlight java %}
//shutdown() method will wait all tasks are executed before terminating
executorService.shutdown();
//shutdownNow() method will terminat
executorService.shutdownNow()
{% endhighlight %}



`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
