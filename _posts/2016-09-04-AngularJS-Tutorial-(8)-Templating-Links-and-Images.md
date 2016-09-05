---
layout: post
title:  "AngularJS Tutorial (8) - Templating Links & Images"
categories: AngularJS
---
{{ page.title }}
===

In this step, we will add thumbnail images for the phones in the phone list, and links that, for now, will go nowhere. In subsequent steps, we will use the links to display additional information about the phones in the catalog.

There are now links and images of the phones in the list.

Reset the workspace to step 8.
{% highlight JavaScript%}
git checkout -f step-8
{% endhighlight %}
Refresh your browser or check out this step online: Step 8 Live Demo.

***

Data
---
Note that the phones.json file contains unique IDs and image URLs for each of the phones. The URLs point to the app/img/phones/ directory.

<br>
`app/phones/phones.json` (sample snippet):
{% highlight JavaScript%}
[
  {
    ...
    "id": "motorola-defy-with-motoblur",
    "imageUrl": "img/phones/motorola-defy-with-motoblur.0.jpg",
    "name": "Motorola DEFY\u2122 with MOTOBLUR\u2122",
    ...
  },
  ...
]
{% endhighlight %}

***

Component Template
---

<br>
`app/phone-list/phone-list.template.html`:
{% highlight html%}
...
<ul class="phones">
  <li ng-repeat="phone in $ctrl.phones | filter:$ctrl.query | orderBy:$ctrl.orderProp" class="thumbnail">
    <a href="#/phones/{{phone.id}}" class="thumb">
      <img ng-src="{{phone.imageUrl}}" alt="{{phone.name}}" />
    </a>
    <a href="#/phones/{{phone.id}}">{{phone.name}}</a>
    <p>{{phone.snippet}}</p>
  </li>
</ul>
...
{% endhighlight %}

To dynamically generate links that will in the future lead to phone detail pages, we used the now-familiar double-curly brace binding in the `href` attribute values. In step 2, we added the `{{phone.name}}` binding as the element content. In this step the `{{phone.id}}` binding is used in the element attribute.

We also added phone images next to each record using an image tag with the ngSrc directive. That directive prevents the browser from treating the Angular `{{ expression }}` markup literally, and initiating a request to an invalid URL (`http://localhost:8000/{{phone.imageUrl}}`), which it would have done if we had only specified an attribute binding in a regular `src` attribute (`<img src="{{phone.imageUrl}}">`). Using the `ngSrc` directive, prevents the browser from making an HTTP request to an invalid location.

Testing
----

<br>
`e2e-tests/scenarios.js`:
{% highlight JavaScript%}
...

it('should render phone specific links', function() {
  var query = element(by.model('$ctrl.query'));
  query.sendKeys('nexus');

  element.all(by.css('.phones li a')).first().click();
  expect(browser.getLocationAbsUrl()).toBe('/phones/nexus-s');
});

...
{% endhighlight %}

We added a new E2E test to verify that the application is generating correct links to the phone views, that we will implement in the upcoming steps.

You can now rerun `npm run protractor` to see the tests run.

Experiments
---

* Replace the `ngSrc` directive with a plain old `src` attribute. Using tools such as your browser's developer tools or inspecting the web server access logs, confirm that the application is indeed making an extraneous request to `%7B%7Bphone.imageUrl%7D%7D` (or `{{phone.imageUrl}}`).<br><br>
The issue here is that the browser will fire a request for that invalid image address as soon as it hits the `<img>` tag, which is before Angular has a chance to evaluate the expression and inject the valid address.

Summary
---
Now that you have added phone images and links, go to step 9 to learn about Angular layout templates and how Angular makes it easy to create applications that have multiple views.
