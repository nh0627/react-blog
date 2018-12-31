---
layout: post
title:  "React02 - Communicating with Props between Components"
date:   2018-12-18
author: Nahyeon Lee
categories: udemy-react
tags: react
---

<p class="intro"><span class="dropcap">R</span>eact component can split the whole UI of an application into separated and independent pieces, and these pieces can communicate with props(properties).</p>

### React Component
* Component Nesting: components can be nested in a parent component
* Component Reusability: components can be re-used over application
* Component Configuration: components should be able to be configured

### Props
* "Props" handles data from a parent component to a child component to customize/configure it.

Let's create components(funcitonal) to display comments:
{% highlight javascript  %}
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
// To insert a random image
import faker from 'faker';
import CommentDetail from './CommentDetail';

const App = () => {
	return (
		<div className="ui container comments">
			<CommentDetail 
				author="Sam" 
				timeAgo="Today at 4:30 PM" 
				content="Nice to know!" 
				avatar={faker.image.avatar()}/>
			<CommentDetail 
				author="Alex" 
				timeAgo="Today at 5:30 PM" 
				content="I like what you wrote there."
				avatar={faker.image.avatar()}/>
			<CommentDetail 
				author="Jane" 
				timeAgo="Today at 6:30 PM" 
				content="Nice blog post!"
				avatar={faker.image.avatar()}/>
		</div>
	);
};

ReactDOM.render(<App />, document.querySelector('#root'))

{% endhighlight %}

{% highlight javascript  %}
// CommentDetail.js
import React from 'react';
import faker from 'faker';

const CommentDetail = (props) => {
	return (
		<div className="comment">
			<a href="/" className="avatar">
				<img alt="avatar" src={ props.avatar }
				/>
			</a>
		<div className="content">
			<a href="/" className="author">
				{ props.author }
			</a>
			<div className="metadata">
				<span className="date">{ props.timeAgo }</span>
			</div>
			<div className="text">{ props.content }</div>
			</div>
		</div>
	);
};

// CommentDetail component has to be exported to be used in other components!
export default CommentDetail;
{% endhighlight %}

Output:
<img src="{{ '/assets/img/2018-12-18-comments.png' }}" alt="comments" style="display: block;"> 

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html

