---
layout: post
title:  "React06 - Making a Simple Picture App with React Input Form and Listing data from API(1)"
date:   2018-12-22
author: Nahyeon Lee
categories: udemy-react
tags: react
---
<p class="intro"><span class="dropcap">E</span>vent handlers in React work simliarly to normal HTML DOM. However, there are certain differences that we have to be aware of using React as below. To practice this points, I have implemented an application listing pictures according to user's keyword to deal with how to use Input form and make Ajax call to API in React.</p>

### Returning false
To prevent default behavior, we cannot return 'false' like a normal HTML code. Rather, we have to call preventDefault:
{% highlight javascript  %}
// HTML
<button onclick="onExampleCilck(); return false">Submit</button>

// React
function onExampleCilck(e) {
    e.preventDefault();
}
{% endhighlight %}

### Controlled components
We'd better store data in mutable React state than the DOM rather than letting HTML form keep data as it does natually. If we store data in React state, React component can do both render a form and control the form's data from user input; it is easiler way to control data in React! This is called "controlled component" that data/value of an input form element is controlled by React like this:

{% highlight javascript  %}
import React from 'react';
class SearchBar extends React.Component {
	state = { term: '' };

	onFormSubmit = (event) => {
	event.preventDefault();

	this.props.onSubmit(this.state.term);
	}
	render() {
		return (
			<div className="ui segment">
				<form onSubmit={this.onFormSubmit} className="ui form">
					<div className="field">
						<label>Image search:
							<input 
							type="text" 
							value={this.state.term}
							onChange={ e => this.setState({ term: e.target.value }) } />
							{/* Controlled component: React state will control submitted value */}
						</label>
					</div>
				</form>
			</div>
		);
	}
}
{% endhighlight %}

### axios VS. fetch: the axios is recommended to make Ajax call
* The axios is a standalone third party package that can be installed into a React project
* The fetch function is a singular function that is built into almost all modern browsers, but far more basic to use
* How to install axios: npm install --save axios

### The app features ([repo][app-repo])
1. Get a search term from a user
2. Use the search term to make a request to an outside API and fetch data
3. Take the fetches images and show them on the screen in a list

{% highlight javascript  %}
/* This app contains two components: SearchBar and ImageList */

// App.js
import React from 'react';
import unsplash from '../api/unsplash';
import SearchBar from './SearchBar';
import ImageList from './ImageList';

/* This app contains two components: SearchBar and ImageList */
class App extends React.Component{

    state = { images: [] };

    // In ES2015, aero functions automatically bind the value of "this" for all code inside the function.
    // This request is an asynchronous request, it will take some amount of time to get a result from API.
    onSearchSubmit = async (term) => {
        // When we put async/await keyword, it will wait till getting a response from API and we can freely work with it later.
        const response = await unsplash.get('/search/photos', {
            params: { query: term }
        });

        this.setState({ images: response.data.results });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar onSubmit={this.onSearchSubmit}/>
                <ImageList images={this.state.images} />
            </div>
        );
    }
};

export default App;
{% endhighlight %}

{% highlight javascript  %}
// unsplash.js
import axios from 'axios';
// This create method is going to create a pre-customized instance of the axios.
export default axios.create({
	baseURL: 'https://api.unsplash.com',
	headers: {
		Authorization: 
		'Client-ID ID' // Put API access key
	}
});
{% endhighlight %}

{% highlight javascript  %}
// SearchBar.js
import React from 'react';
class SearchBar extends React.Component {
	state = { term: '' };
	// In ES2015, aero functions automatically bind the value of "this" for all code inside the function. if not, "this" will be undefined
	// keep the browser from trying to submit the form automatically and in the process refreshing the page
	onFormSubmit = (event) => {
	event.preventDefault();
	// Passing submitted data to the parent App component
	this.props.onSubmit(this.state.term);
	}
	render() {
		return (
			<div className="ui segment">
				<form onSubmit={this.onFormSubmit} className="ui form">
					<div className="field">
						<label>Image search:
							<input 
							type="text" 
							value={this.state.term}
							onChange={ e => this.setState({ term: e.target.value }) } />
							{/* Controlled component: React state will control submitted value */}
						</label>
					</div>
				</form>
			</div>
		);
	}
}
export default SearchBar;
{% endhighlight %}

{% highlight javascript  %}
// ImageList.js
const ImageList = props => {
	// Push props.images into an array and display it into div
	const images = props.images.map(({ description, id, urls }) => {
		// Listing images with map() function
		// Let each element has a unique key(id property) in a list also to identify elements.
		return(
			<img key={id} alt={description} src={urls.regular} />
			);
		});
		return <div>{images}</div>
	};
export default ImageList;
{% endhighlight %}

Output:
<img src="{{ '/assets/img/2018-12-22-picture-1.png' }}" alt="picture" style="display: block; width: 700px;"> 

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/07.pics
[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html