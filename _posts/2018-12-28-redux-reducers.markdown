---
layout: post
title:  "React-Redux03 - Rules of Reducers"
date:   2018-12-28
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux
---

### Rules of Reducers
* Produces 'state' or data to be used inside of your app using only previous state and the action 
* Must return any value besides 'undefine'
{% highlight javascript  %}
export default() => {
    // Error: it should always have return statement!
}
{% endhighlight %}
* Must not return reach 'out of itself' to decide what value to return(reducers are pure)
{% highlight javascript  %}
export default(state, action) => {
    // bad!
    return document.querySelector('input');
    // bad!
    return axios.get('/posts');
    // good
    return state + action;
}
{% endhighlight %}
* Must not mutate its input 'state' argument; We are not going to mutate state ever! However, When we work on a reducer that is returning an array or an object, we might want to change an element/property in the returned array/object. In that case, we can use the syntax below which also makes sure we are not mutating any state argument, because it creates a new array or object:
<img src="{{ '/assets/img/posts/2018-12-28-no-mutate.png' }}" alt="mutate">

The source of this post and code is from [Modern React with Redux][udemy-react].

[udemy-react]: https://www.udemy.com/react-redux/