---
layout: post
title: 손수민든 데이터 시각화
subtitle: 나중에 채우기. 
gh-repo: daattali/beautiful-jekyll
tags: [시각화]
comments: true
---

헬로 여러분들 ~ 요즈음 미세먼지가 심각해졌죠?
  빨래 널어야하는데 빨래에 미세먼지가 철-썩- 달라붙을까봐 걱정 또 걱정이네요~
  여름에는 장마여서 못널어~ 겨울에는 얼어서 못널어~ 봄과 가을에는 미세먼지 때문에 못 널어~
  더 넓은 집으로 이사가서 건조기를 얼른 장만해야겠어요!

아무튼 잡담은 그만하고 
오늘은 미세먼지 데이터를 활용하여 시각화를 손수민들어 볼거에요~
파이썬과 데이터만 있으면 어디든 갈 수 있죠.

우리가 만들건 ----이러한 결과를 만들어 볼 것이고요~
먼저 데이터 출처는 -----입니다.



This is a demo post to show you how to write blog posts with markdown.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](https://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

**Here is some bold text**

## Here is a secondary heading

Here's a useless table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


How about a yummy crepe?

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
