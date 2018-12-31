---
layout: post
title:  "React-Redux02 - Async with Redux Thunk"
date:   2018-12-27
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux redux-thunk
---
<p class="intro"><span class="dropcap">A</span> middleware makes network requests from the Redux side of app. It is a plain JavaScript function that is called with every single action we dispatch. Especially it is required when we work with an asynchronous Action Creator, because it has the ability to STOP, MODIFY or otherwise mess around with actions. Redux Thunk is one of middelwares in the world of Redux that can work with Action Creators!
</p>

#### General Data Loading with Redux
1. Component gets rendered onto the screen
2. Component's 'componentDidMount' lifecycle method get called
3. We call Action Creator automatically from 'componentDidMount'
4. Action Creator runs code to make an API request
5. API responds with data
6. Action creator returns an 'action' with the fetched data on the 'payload' property; <em>this is where Redux-Thunk comes into play</em>
7. Specially configured reducers sees the action, returns the data of the 'payload'
8. Because we generated some new state object, redux/react-redux cause our React app to be rerendered; we get fetched data into a component by generating new state in our redux store, then getting that into our component through mapStateToProps

In relation to the process above, if we make Action Creator like below, there will be an error as the reason in the comments:
{% highlight javascript  %}
// /src/actions/index.js
import jsonPlaceholder from '../apis/jsonPlaceholder';

// There is an error in this component, because this Action Creator is not returning a plain JavaScript object, because we have the async await syntax.
// However, we cannot just simply skip this async await syntax.
// This is because by the time we finally get a response from the API,
// our action has long since been processed by our reducers that have already ran.
export const fetchPosts = async () => {
    const response = await jsonPlaceholder.get('/posts');
    return {
        type: 'FETCH_POSTS',
        payload: response
    };
};
{% endhighlight %}

#### Rules with Redux Thunk
In the normal rules of Action Creator in Redux, "it must return action objects". However, with Redux Thunk, Action Creator can return action objects or functions. In the case that a function is returned, Redux Thunk is going to automatically call the function with dispatch and getState function. Once we get a response eventually, we can manually dispatch an action with the response at some point in time in the future.

The code above can be fixed like this with React Thunk:
{% highlight javascript  %}
// /src/actions/index.js
import jsonPlaceholder from '../apis/jsonPlaceholder';

export const fetchPosts = () =>
    async dispatch => {
        const response = await jsonPlaceholder.get('/posts');

        dispatch({ type: 'FETCH_POSTS', payload: response })
    };
{% endhighlight %}

#### App Repo
[Here][app-repo]

The source of this post and code is from [Modern React with Redux][udemy-react].

[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/14.blog
[udemy-react]: https://www.udemy.com/react-redux/