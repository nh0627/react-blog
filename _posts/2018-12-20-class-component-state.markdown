---
layout: post
title:  "React04 - Class-based Components, State and Component Lifecycle"
date:   2018-12-20
author: Nahyeon Lee
categories: udemy-react
tags: react
---
A component can be functional or a class-based. Functional components are good enough to display simple content, but class components can be good for more than a simple feature with any complex logic. There is a concept of "state" in React also; State lets components to update their output data as responding immediately to a user's action(asynchronously).

### Rules of Class Components
* Must be a JavaScript class
* Must extend(subclass) React.Component
* Must define a 'render' method that returns some amount of JSX

### Rules of State
* Only usable with class-components
* 'State' is a JS object that contains data related to a single component
* Updating 'state' on a component causes the component to <em>(almost) instatntly re-rendered</em>
* State must be initialized when a component is first created (a constructor can be helpful)
* State can <em>only</em> be updated using the function 'setState'

### Detecting user's geolocation with React State
{% highlight javascript  %}
// index.js
import React from 'react';
import ReactDOM from 'react-dom';

/*
Timeline of how this app works
	1. JS file loaded by browser
	2. Instance of App component is created
	3. App components 'constructor' function gets called
	4. State object is created and assigned to the 'this.state' property
	5. We call geolocation service
	6. React calls the components render method
	7. App returns JSX, gets rendered to page as HTML
	... after a while
	8. We get result of geolocation!!!
	9. We update our state object with a call to 'this.setState'
	10. React sees that we updated the state of a component
	11. React calls our 'render' method a second time
	12. Render method returns some (updated) JSX
*/

// App component has code to figure out user's location and month
class App extends React.Component {
	constructor(props) {
		super(props); // It must to be called!!!
		// Initialize state object with sensible value, but THIS IS ONLY TIME we do direct assignment to this.state
		this.state = { lat: null, errorMessage: '' }; 
		// Get users physical location
		window.navigator.geolocation.getCurrentPosition(
		// To update state object, setState must be called! *rather than "this.state.lat = value")
		(position) => this.setState({ lat: position.coords.latitude }), 
		(err) => this.setState({errorMessage: err.message})
		);
	}
	// React says we have to define render!!
	render() {
		if ( this.state.errorMessage && !this.state.lat ) {
			return <div> Error : { this.state.errorMessage } </div>
		}
		if ( !this.state.errorMessage && this.state.lat ) {
			return <div>Latitude: { this.state.lat } </div>
		}
		return <div>Loading!</div>
		}
}
ReactDOM.render(
	<App />,
	document.querySelector('#root')
);
{% endhighlight %}

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html