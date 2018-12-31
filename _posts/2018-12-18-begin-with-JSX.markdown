---
layout: post
title:  "React01 - Begin with JSX"
date:   2018-12-18
author: Nahyeon Lee
categories: udemy-react
tags: react
---

ES2015 or 2016 JS is not guaranteed to be fully supported by a user's browser. In order to use it normally, we need use Babel which takes ES2015 or 2016 and converts them into ES5 Javascript code. 
"React seperate concern with loosely coupled units called "components" (not in seperate files) that contain markup and logic(from [React Doc][react-doc-jsx]"). To do so, JSX can be useful to put UI and JavaScript code together. However, like ES2015 or 2016, a browser cannot understand natively JSX, so it needs to be converted to normal javascript code for a browser to render it with Babel.

These two are the same, but different syntax:

{% highlight javascript  %}
// JSX
const App = () => {
	return <div>Hi there!</div>; 
};

// ES5
var App = function App() {
	return React.createElement(
		"div",
		null,
		"Hi there!"
	);
};
{% endhighlight %}

### JSX VS. HTML
Custom styling with JSX:
{% highlight javascript  %}
// HTML 
<div style="background-color: red;"></div>

// JSX
<div style={{backgroundColor: 'red'}}></div>
{% endhighlight %}

Different element attributes:
{% highlight html  %}
// HTML 
<label class="label" for="name">Name:</label>

// JSX
<label className="label" htmlFor="name">Name:</label>
{% endhighlight %}

JSX with JS variables:
{% highlight javascript  %}
const buttonText ={ text: 'Click Me!' };
const style = { backgroundColor: 'blue', color: 'white' };

<button style={ style }>
	{ buttonText.text }
</button>
{% endhighlight %}

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html
[react-doc-jsx]: https://reactjs.org/docs/introducing-jsx.html
