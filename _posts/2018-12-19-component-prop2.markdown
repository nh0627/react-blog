---
layout: post
title:  "React03 - Add More Components inside a Component"
date:   2018-12-19
author: Nahyeon Lee
categories: udemy-react
tags: react
---
A React app usually has one App component as the root/top one. Then it can contain children components that we can reuse as many as we want into a parent component and configure/customize them with props as below.

### Add components over components
{% highlight javascript  %}
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import faker from 'faker';
import CommentDetail from './CommentDetail';
import ApprovalCard from './ApprovalCard';

const App = () => {
	return (
		<div className="ui container comments">
			<ApprovalCard>
				{/* A component can be reused without any child component */}
				<div>
				<h4>Warning!</h4>
				Are you sure you want to do this?
				</div>
			</ApprovalCard>
			<ApprovalCard>
				<CommentDetail 
				author="Sam" 
				timeAgo="Today at 4:30 PM" 
				content="Nice to know!" 
				avatar={faker.image.avatar()}/>
			</ApprovalCard>
			<ApprovalCard>
				<CommentDetail 
				author="Alex" 
				timeAgo="Today at 5:30 PM" 
				content="I like what you wrote there."
				avatar={faker.image.avatar()}/>
			</ApprovalCard>
			<ApprovalCard>
			     <CommentDetail 
			     author="Jane" 
			     timeAgo="Today at 6:30 PM" 
			     content="Nice blog post!"
				avatar={faker.image.avatar()}/>
			</ApprovalCard>
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

export default CommentDetail;
{% endhighlight %}

{% highlight javascript  %}
// ApprovalCard.js
import React from 'react';
const ApprovalCard = (props) => {
	return (
		<div className="ui card">
			{/* Load the child component, CommentDetail like below! */}
			<div className="content">{props.children}</div>
			<div className="extra content">
				<div className="ui two buttons">
					<div className="ui basic green button">Approve</div>
					<div className="ui basic red button">Reject</div>
				</div>
			</div>
		</div>
	);
};
export default ApprovalCard;
{% endhighlight %}

Output:
<img src="{{ '/assets/img/2018-12-19-comments.png' }}" alt="comments"> 

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html

