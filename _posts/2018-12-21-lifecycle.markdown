---
layout: post
title:  "React05 - Component Lifecycle"
date:   2018-12-21
author: Nahyeon Lee
categories: udemy-react
tags: react
---
<p class="intro"><span class="dropcap">C</span>omponent lifecycle method is a function that can be optionally defined and used inside of class-based components if we want to use it at a distinct time during the component lifecycle. </p>

### Component lifecycle methods
* componentDidMount(): when a component rendered to DOM for the first time; it is recommended to initialize data than constructor 
* componentDidUpdate(): anytime a component gets updated 
* componentWillUnmount() when a component removed from DOM. 

#### Application with class-component, state and lifecycle detecting a user's geolocation and determining if the user's season is summer or winter [Repo][app-repo]
{% highlight javascript  %}
// index.js
/* It will handle initializing state on user's geolocation, 
component life cycle, and render a error/season/loader message upon condition below. */

import React from 'react';
import ReactDOM from 'react-dom';
import SeasonDisplay from './SeasonDisplay';
import Loader from './loader'

class App extends React.Component {

    // Any constructor is not required!

    state = { lat: null, errorMessage: '' }; // Babel will put this line into Constructor anyways

    // Lifecycle method
    componentDidMount() {
        console.log('My component was rendered to the screen');
        
        // Initialize data here(users physical location)
        window.navigator.geolocation.getCurrentPosition(
            (position) => this.setState({ lat: position.coords.latitude }), 
            (err) => this.setState({errorMessage: err.message})
        );
    }

    // Lifecycle method
    componentDidUpdate() {
        console.log('My component was just updated - it re-rendered!')
    }
    
    render() {
        if ( this.state.errorMessage && !this.state.lat ) {
            return <div> Error : { this.state.errorMessage } </div>
        }
        if ( !this.state.errorMessage && this.state.lat ) {
            return <SeasonDisplay let={this.state.lat} /> // Pass state as props
        }
        return <Loader message="Please accept location request!" />
    }
}

ReactDOM.render(
    <App />,
    document.querySelector('#root')
);
{% endhighlight %}

{% highlight javascript  %}
// SeasonDisplay.js
// SeasonDisplay component shows different text/icons based on props

import './SeasonDisplay.css';
import React from 'react';

const seasonConfig = {
    summer: {
        text: 'Lets hit the beach!',
        iconName: 'sun'
    },
    winter: {
        text: 'Burr, it is chilly',
        iconName: 'snowflake'
    }

};

// Determine season responding to user's latitude
const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
       return lat > 0 ? 'summer' : 'winter'; 
    } else {
       return lat < 0 ? 'summer' : 'winter'; 
    }
}

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    const {text, iconName} = seasonConfig[season];

    return (
        <div className={`season-display ${season}`}>
            <i className={`${iconName} icon-left icon massive`} />
            <h1>{ text }</h1>
            <i className={`${iconName} icon-right icon massive`} />
        </div>
    );
};

export default SeasonDisplay;
{% endhighlight %}

{% highlight javascript  %}
SeasonDisplay.css
.icon-left {
    position: absolute;
    top: 10px;
    left: 10px;
}

.icon-right {
    position: absolute;
    bottom: 10px;
    right: 10px;
}

.season-display {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.season-display.winter i {
    color: blue;
}

.season-display.summer i {
    color: red;
}

.winter {
    background-color: aliceblue;
}

.summer {
    background-color: orange;
}
{% endhighlight %}


{% highlight javascript  %}
// loader.js 
import React from 'react';

const Loader = (props) => {
    return (
        <div className="ui active dimmer">
            <div className="ui big text loader">{props.message}</div>
        </div>
    );
};

// Set default value for props
Loader.defaultProps = {
    message: 'Loading...'
};

export default Loader;
{% endhighlight %}


Output:
<img src="{{ '/assets/img/2018-12-21-season-1.png' }}" alt="season">
<img src="{{ '/assets/img/2018-12-21-season-2.png' }}" alt="season"> 

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/04.seasons
[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html