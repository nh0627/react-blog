---
layout: post
title:  "React-Redux00 - Intro to Redux"
date:   2018-12-25
author: Nahyeon Lee
categories: udemy-react
tags: redux
---
Redux is a state management library. The goal of React is rendering content and handling user interaction rather than handling data. For handling data, we can make Redux keep/handle states of our app in/from a single store. By doing so, we can create an advanced application easier with Redux than using React alone.

### Redux Cycle
Action Creator 🡒 Action 🡒 dispatch 🡒 Reducers 🡒 State

#### Action Creator
The action creator is a function that creates or returns a plain JavaScript object. We call it to change state of our app.

#### Action
The action is the plain JavaScript object produced by action creator and has a type(of change we want to make) and payload(context around the change) property. The purpose of an action is to describe some changes that we want to make to the data inside of our app.

#### dispatch
The dispatch function is going to take in action; making copies of the object and forward them to places inside of our app.

#### Reducer
The reducer is a function taking in an action. It is going to process an action and then make some changes to data(state) and return it, so that it can be centralized in other location.

#### State
A state property is a central repository of all information that has been created by reducers. It waits until we need to update it again.

### Example code
[https://codepen.io/nh0627/pen/VqboVy?editors=0010][redux-code]

The source of this post and code is from [Modern React with Redux][udemy-react].

[redux-code]: https://codepen.io/nh0627/pen/VqboVy?editors=0010
[udemy-react]: https://www.udemy.com/react-redux/