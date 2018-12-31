---
layout: post
title:  "React07 - Making a Simple Picture App with Ref(2)"
date:   2018-12-23
author: Nahyeon Lee
categories: udemy-react
tags: react
---
In the previous post, I made an app listing pictures according to user's keyword input. However, in this post I would like to make each picture as a grid in order to let the app have a better display of images.

#### Before
<img src="{{ '/assets/img/2018-12-22-picture-1.png' }}" alt="picture"> 

#### Now
<img src="{{ '/assets/img/2018-12-23-picture-2.png' }}" alt="picture"> 

To do so, ImageCard component needs to be made to put each picture into grid in the order below:
1. Let the ImageCard render itself and its image.
2. Reach into the DOM and figure out the height of the image. <em>We need React refs here!</em>
3. Set the image height on state to get the component to rerender.
4. When rerendering, assign a 'grid-row-end' to make sure the image takes up the appropriate space.

### React Refs
* Gives direct access to a single DOM element rendered by a component
* We create refs in the constructor, assign them to instance vairables, then pass to a particular JSX element as props

{% highlight javascript  %}
import React from 'react';

class ImageCard extends React.Component {

    constructor(props) {
        super(props);

        this.imageRef = React.createRef(); // Create a React ref
    }

    componentDidMount() {
        console.log(this.imageRef.current.clientHeight); // We can print out each image's height
    }

    render() {
        const { description, urls } = this.props.image;
        return (
            <div>
                <img
                    {/*Pass a new prop ref to wire up the ref (JSX tag)*/}
                    ref={this.imageRef}
                    alt={description}
                    src={urls.regular}
                />
            </div>
        );
    }
}

export default ImageCard;
{% endhighlight %}

By the way, if we execute the code above, we can see the image height is 0 on Chrome console. This is because when we console log out the height of the image, there is no image downloaded yet. It is too early to get the image height value at the time, because there is no image loaded yet. To fix this:

{% highlight javascript  %}
import React from 'react';

class ImageCard extends React.Component {

    constructor(props) {
        super(props);
        this.state = { spans: 0 }; // Initialize a state
        this.imageRef = React.createRef();
    }

    componentDidMount() {
        // It will listen for the event load any time that an image loaded, and then call setSpans() 
        this.imageRef.current.addEventListener('load', this.setSpans);
    }

    setSpans = () => {
        // Get the correct height of each image and set it into the state
        const height = this.imageRef.current.clientHeight;
        const spans = Math.ceil(height / 10) + 1;
        this.setState({ spans });
    }

    render() {
        const { description, urls } = this.props.image;
        return (
            <div style={gridRowEnd:`span ${this.state.spans}`}}>
                <img
                    ref={this.imageRef}
                    alt={description}
                    src={urls.regular}
                />
            </div>
        );
    }
}

export default ImageCard;
{% endhighlight %}

The final code is [here][app-repo].

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/07.pics
[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html