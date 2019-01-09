---
layout: post
title:  "React-Redux01 - React with Redux"
date:   2018-12-26
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux
---
The Redux library is not only designed to work with React. Thus, we have to note that after installing React and Redux, and we need a third party library, React-Redux, which can let us use integrate React with Redux.

### Command to install Redux and Redux-React into React project
npm install --save redux react-redux

### How React-Redux works?
<img src="{{ '/assets/img/posts/2018-12-26-react-redux-structure.png' }}" alt="structure">
* To use react-redux, we need to create two new components: Provider and Connect
* The Provider is rendered at the very top of app and has eternal reference to Redux store. The term Provider essentially means it is providing information to all of the different components inside of our app. 

{% highlight javascript  %}
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore } from 'redux';

import App from './components/App';
import reducers from './reducers';

// Create an instance of provider and wrap our app component with it
// The store prop is going to be a result of calling create store and passed in our reducers.
// So in a typical redux application, we don't have to go directly to the store. The provider will take care of it. 
ReactDOM.render(
    <Provider store={createStore(reducers)}>
        <App />
    </Provider>,
    document.querySelector('#root'));
{% endhighlight %}

* The connect function is special because it can communicate with the Provider at the very top of our hierarchy. It communicates with the Provider not through the props system but through a completely different system of communication(the context system). So the connect function can get data from the Provider and pass it as a prop to components that need to interact with the redux store. The connect function can be used not only to get data out of our store but also to get action creators correctly into our components to change data in the Redux store. 

{% highlight javascript  %}
// SongList.js
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { selectSong } from '../actions';

class SongList extends Component {

    renderList() {
        return this.props.songs.map( (song) => {
            return (
                <div className="item" key={song.title}>
                    <div className="right floated content">
                        <button 
                            className="ui button primary"
                            onClick={() => this.props.selectSong(song)}>
                            Select
                        </button>
                    </div>
                    <div className="content">{ song.title } 
                    </div>
                </div>
            );
        });
    }
    render() {
        return <div className="ui divided list">{this.renderList()}</div>;
    }
}

// Take our state object inside of our redux store, and it will show up as props inside of our component.
const mapStateToProps = state => {
    return { songs: state.songs };
}

// We should not call Action Creator inside of our component.
// This connect function will call automatically the Action Creator that we made,
// and automatically take the action that gets returned as calling the dispatch function of Redux for us.
export default connect(mapStateToProps, { selectSong })(SongList);
{% endhighlight %}

### Repo for the full example codes
[Here][app-repo]

The source of this post and code is from [Modern React with Redux][udemy-react].

[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/13.songs
[udemy-react]: https://www.udemy.com/react-redux/