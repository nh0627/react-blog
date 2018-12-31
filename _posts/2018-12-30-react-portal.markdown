---
layout: post
title:  "React09 - React Portal"
date:   2018-12-30
author: Nahyeon Lee
categories: udemy-react
tags: react
---
It would be hard to create a modal window in a React app. This is because it is difficult to load a modal component into other components due to a complicated component hierarchy(a component is a child of another component that is also a child of other components...) in React. Instead, we need to break the component hierarchy with a portal which allows us to render an element not as a direct child of a component, but as some child of other elements inside HTML structure.

### Create a modal window with a portal

#### Basic syntax
{% highlight javascript  %}
// "child" is a React child that we want to render
// "container" is a location at HTML DOM that we want to put the child
ReactDOM.createPortal(child, container) 
{% endhighlight %}

#### Example modal code
`// Modal.js`
{% highlight javascript  %}
import React from 'react';
import ReactDOM from 'react-dom';

// This modal will be rendered at <div id="modal"></div> in index.html
const Modal = props => {
    return ReactDOM.createPortal(
        <div onClick={props.onDismiss} 
            className="ui dimmer modals visible active">
            <div onClick={(e)=>e.stopPropagation()}
                className="ui standard modal visible active">
                <div className="header">{props.title}</div>
                <div className="content">
                    {props.content}
                </div>
                <div className="actions">
                    {props.actions}
                </div>
            </div>
        </div>,
        document.querySelector('#modal')
    );
};

export default Modal;
{% endhighlight %}

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/portals.html