---
layout: post
title:  "React-Redux04 - Redux Form"
date:   2018-12-29
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux
---
<p class="intro"><span class="dropcap">R</span>edux Form can be helpful for us to store form data inside of our Redux store. Here is how it handels form data and how we can implement it into our app. The displayed code below is from [the stream video app][app-doc], you can check the project's document and repo in the link.</p>

#### Command to install Redux Form
npm install --save redux-form

#### How Redux Form works?
<img src="{{ '/assets/img/2018-12-29-redux-form.png' }}" alt="structure" style="display: block; width: 600px;">
* Form data exists in a redux store and will be maintained by a reducer.
* mapStateToProps takes form data from a redux store and get it into components as props.
* Prop objects and all the values inside will be passed into input elements as values.
* When a user make changes input elements, a callback handler in our component will be invoked.
* It goes to an action creator that can update form data in a redux store.

#### Adding Redux Form into our app
{% highlight javascript  %}
// /src/reducers/index.js
import { combineReducers} from 'redux';
import { reducer as formReducer } from 'redux-form'; // Add this
import authReducer from './authReducer';

export default combineReducers({
    auth: authReducer,
    form: formReducer
});
{% endhighlight %}

{% highlight javascript  %}
// /src/components/streams/StreamCreate.js -> One of our components!
import React from 'react';
import { Field, reduxForm } from 'redux-form';

class StreamForm extends React.Component {

    // We can set error message if input form touched
    renderError({error, touched}) {
        if (touched && error) {
            return (
                <div className="ui error message">
                    <div className="header">{error}</div>
                </div>
            );
        }
    }

    // We can customize what form element we want to show
    renderInput = ({ input, label, meta }) => {
        const className = `field ${meta.error && meta.touched ? 'error' : ''}`;

        return (
            <div className={className}>
                <label>{label}</label>
                <input {...input} // It takes take all the properties out there and add them as props to the input element.
                    autoComplete="off"    
                />
                {this.renderError(meta)}
            </div>
        );
    }

    onSubmit = (formValues) => {
        this.props.onSubmit(formValues);
    }

    render() {
        return (
            <form 
                onSubmit={ this.props.handleSubmit(this.onSubmit) }
                className="ui form error">
                <Field 
                    name="title" 
                    component={this.renderInput} // we have to assign this component prop
                    label="Title"/>
                <Field 
                    name="description" 
                    component={this.renderInput} 
                    label="Description"/>
                <button className="ui button primary">Submit</button>
            </form>
        );
    }
}

// Check validation
const validate = (formValues) => {
    const errors = {};
    if(!formValues.title) {
        errors.title = 'You must enter a title';
    }
    if(!formValues.description) {
        errors.description = 'You must enter a description';
    }
    return errors;
}

export default reduxForm({
    form: 'streamForm',
    validate
})(StreamForm);
{% endhighlight %}

#### Project Doc & Repo
[Doc][app-doc] / [Repo][app-repo]

The source of this post and code is from [Modern React with Redux][udemy-react], also from [React Doc][react-doc].

[app-doc]: https://nh0627.github.io/blog/stream-app/
[app-repo]: https://github.com/nh0627/udemy-react-redux/tree/master/16.streams
[debugging]: https://github.com/zalmoxisus/redux-devtools-extension
[udemy-react]: https://www.udemy.com/react-redux/
[react-doc]: https://reactjs.org/docs/getting-started.html