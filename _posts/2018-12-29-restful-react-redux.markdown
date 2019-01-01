---
layout: post
title:  "React-Redux05 - RESTful with React-Redux"
date:   2018-12-29
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux restful
---
RESTful convention refers to a standard system of routes and request methods used to commit or operate actions. It is highly recommended to make a network request to our API server and also cooperate with other engineers. I made a simple example of how to implement the RESTful convention into our React-redux app as below action creators and reducers. The displayed code below is from [the stream video app][app-doc], you can check the project's document and repo in the link.

### Restful Convention
<img src="{{ '/assets/img/2018-12-29-restful.png' }}" alt="structure">

### Example codes in RESTful Convention

#### Action Creators to send AJAX request 
{% highlight javascript  %}
// /src/actions/index.js
import streams from '../apis/axios/streams';

export const createStream = formValues => async dispatch => {
    const response = await streams.post('/streams', formValues);
    dispatch({type: 'CREATE_STREAM', payload: response.data });
};

export const fetchStreams = () => async dispatch => {
    const response = await streams.get('/streams');
    dispatch({type: 'FETCH_STREAMS', payload: response.data });
};

export const fetchStream = id => async dispatch => {
    const response = await streams.get(`/streams/${id}`);
    dispatch({type: 'FETCH_STREAM', payload: response.data });
};

export const editStream = (id, formValues) => async dispatch => {
    // put(): Update all properties of record 
    // const response = await streams.put(`streams/${id}`, formValues) 
    // patch(): Update some properties of record that needs to be updated
    const response = await streams.patch(`streams/${id}`, formValues);
    dispatch({type: 'EDIT_STREAM', payload: response.data });
}

export const deleteStream = id => async dispatch => {
    await streams.delete(`streams/${id}`);
    dispatch({type: 'DELETE_STREAM', payload: id });
}
{% endhighlight %}

#### Reducers to take the actions
{% highlight javascript  %}
// /src/reducers/streamReducer.js
import _ from 'lodash';

// Key interpolation syntax
export default (state={}, action) => {
    switch(action.type) {
        // Map keys is a function that's going to take an array and then return an object that keys of
        // this new object are going to be taken from each individual record(as its id) inside of the array.
        case FETCH_STREAMS:
            return { ...state, ..._.mapKeys(action.payload, 'id') };

        // Whenever we get a action with FETCH_STREAM, we are taking our state object and its properties 
        // and add it to the new object with a new key value pair dynamically.
        case FETCH_STREAM:
            return { ...state, [action.payload.id]: action.payload };
        case CREATE_STREAM:
            return { ...state, [action.payload.id]: action.payload };
        case EDIT_STREAM:
            return { ...state, [action.payload.id]: action.payload };

        // omit is not changing the original state object, it rather creates a new object with all the properties from the state
        case DELETE_STREAM:
            return _.omit(state, action.payload);
        default:
            return state;
    }
};
{% endhighlight %}

### Full Project Doc & Repo
[Doc][app-doc] / [Repo][app-repo]

The source of this post and code is from [Modern React with Redux][udemy-react].

[app-doc]: https://nh0627.github.io/blog/stream-app/
[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/16.streams
[udemy-react]: https://www.udemy.com/react-redux/