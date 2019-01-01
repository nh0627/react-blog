---
layout: post
title:  "React08 - Navigating with React Router"
date:   2018-12-26
author: Nahyeon Lee
categories: udemy-react
tags: react react-router
---
Ract Router can let a user navigate to another page with different URLs in our app. However, unlike the traditional way of handling this, we should not use the traditional anchor tag to link somewhere. Because it will return a new HTML document so we will lose all data in memory and access to any API. We'd better use Link tag in this case as below code to keep a browser from dumping all our react and JavaScript data.

### Command to install navigation for dom-based apps
npm install --save react-router-dom

### Code Example
{% highlight javascript  %}
import React from 'react';
import { BrowserRouter, Route, Link } from 'react-router-dom';

const PageOne = () => {
    return (
        <div>
            PageOne
            <Link to="/pagetwo">Navigate to Page Two</Link>
        </div>
    );
}

const PageTwo = () => {
    return (
        <div>
            PageTwo
            <Link to="/">Navigate to Page One</Link>
        </div>
    );
}

const App = () => {
    return (
        <div>
            <BrowserRouter>
                <div>
                    <Route path="/" exact component={PageOne} />
                    <Route path="/pagetwo" exact component={PageTwo} />
                </div>
            </BrowserRouter>
        </div>
    );
}

export default App;
{% endhighlight %}

However, When we do programming, it would be required to forcibly change or navigate a user to a different page responding to some event. However, when we use a browser router from react-router, the browser router creates a history object which not only watches and keeps track of the address bar, but also is able to change the address bar. To manipulate the history object by ourselves to navigate a user forcibly, we can create a customized history object to control it by ourselves rather than allowing react-router to do so.

### Creating a broswer history object
{% highlight javascript %}
import createHistory from 'history/createBrowserHistory';

export default createHistory();

// This is it!
{% endhighlight %}

{% highlight javascript %}
// App.js
import React from 'react';
import { Router, Route, Switch } from 'react-router-dom';
import StreamCreate from '../components/streams/StreamCreate';
import StreamList from '../components/streams/StreamList';
import Header from './Header';
import history from '../history';

const App = () => {
    return (
        <div className="ui container">
            // Use Router than BrowserRouter!
            <Router history={history}>
                <div>
                <Header />
                // This switch is to show only one of these given routes
                <Switch>
                    <Route path="/" exact component={StreamList} />
                    <Route path="/streams/new" exact component={StreamCreate} />
                </Switch>
                </div>
            </Router>
        </div>
    );
}
export default App;
{% endhighlight %}

Then, now we can use this syntax to navigate a user programmatically!
{% highlight javascript %}
history.push('/');
{% endhighlight %}

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html