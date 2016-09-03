---
layout: post
title:  "AngularJS Tutorial (1) - Static Template"
categories: AngularJS
---
{{ page.title }}
===

In order to illustrate how Angular enhances standard HTML, you will create a purely static HTML page and then examine how we can turn this HTML code into a template that Angular will use to dynamically display the same result with any set of data.

In this step you will add some basic information about two cell phones to an HTML page.

* The page now contains a list with information about two phones.

Reset the workspace to step 1.

{% highlight JavaScript %}
git checkout -f step-1
{% endhighlight %}

Refresh your browser or check out this step online: Step 1 Live Demo.
The most important changes are listed below. You can see the full diff on GitHub.

**app/index.html:**
{% highlight JavaScript %}
<ul>
  <li>
    <span>Nexus S</span>
    <p>
      Fast just got faster with Nexus S.    </p>
  </li>
  <li>
    <span>Motorola XOOM™ with Wi-Fi</span>
    <p>
      The Next, Next Generation tablet.    </p>
  </li>
</ul>
{% endhighlight %}

Experiments
---
Try adding more static HTML to `index.html`. For example:
{% highlight JavaScript %}
<p>Total number of phones: 2</p>
{% endhighlight %}

Summary
---
This addition to your app uses static HTML to display the list. Now, let's go to step 2 to learn how to use Angular to dynamically generate the same list.
