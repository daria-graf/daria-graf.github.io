---
layout: post
title: 'Copy objects in JavaScript'
date: 2023-04-02 22:22:19 +0200
categories: coding javascript
author: 'Daria Graf'
---

In this post I'm going to compare different ways of coping an object in JavaScript.

Here is an example of a code snippets:

{% highlight js %}
const first = {
id: '1',
name: 'first'
}
const second = {...first};
second.id = 2;
second.name = 'second';
{% endhighlight %}

Learn more about desctructuring assignment [MDN Web Docs][mdn-destructuring].

[mdn-destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment?retiredLocale=de
