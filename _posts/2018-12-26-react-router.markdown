---
layout: post
title:  "React08 - Navigating with React Router"
date:   2018-12-26
author: Nahyeon Lee
categories: udemy-react
tags: react react-router
---
<p class="intro"><span class="dropcap">R</span>act Router can let a user navigate to another page with different URLs in our app. However, unlike the traditional way of handling this, we should not use the traditional anchor tag to link somewhere. Because it will return a new HTML document so we will loose all data in memory and access to any API. We'd better use Link tag in this case as below code to keep a browser from dumping all our react and JavaScript data.
</p>

#### Command to install navigation for dom-based apps
npm install --save react-router-dom

#### Code Example
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

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html