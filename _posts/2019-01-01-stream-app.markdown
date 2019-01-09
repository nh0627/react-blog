---
layout: post
title:  "React App Practice02 - Video Streaming App"
date:   2019-01-01
author: Nahyeon Lee
categories: udemy-react
tags: react redux react-redux app-practice
---
This post is about a video stream app that I made through [Modern React with Redux][udemy-react].

### Screen Shot
<img src="{{ '/assets/img/posts/2019-01-08-streamy.png' }}" alt="streamy">

### Features with the course
* Navigator with routing
* Login/Logout with Google OAuth to manage a stream/channel and comments
* List of all the streams with a simple description underneath it
* Detail pages to show a streamed video
* Every user can create/retrieve/delete/edit unlimited streams/channels 

### Fetures that I updated
* Every user can make/retrieve/delete a comment to/from each stream/channels
* Add categories to filter streams

### Skills
* Client: React, Redux
* API Server: JSON Server
* RTMP Server: [Node-Media-Server][NMS]

### Libraries
* react
* redux
* react-redux
* axios
* redux-thunk
* redux-form
* react-router-dom
* lodash
* dateformat
* json-server
* [node-media-server][NMS]
* [OBS Studio][OBS]

### Repository
[Here][app-repo]

The source of this post and code is from [Modern React with Redux][udemy-react].

[OBS]: https://obsproject.com/
[NMS]: https://github.com/illuspas/Node-Media-Server
[app-repo]: https://github.com/nh0627/react-video-stream
[udemy-react]: https://www.udemy.com/react-redux/