---
layout : post
title : "Merging Trails and Docker"
subtitle : Two emerging technologies living together.
category : tech
author : sposmen
tags :
  - continuous integration
  - trails
  - docker
  - git
  - emerging technologies
---

Sometimes, when developers try to merge certain technologies, is difficult to find a good way to do it. There is where our team found a chance to
continue learning new things based on emerging technologies. In this particular case Trails combined with Docker is the goal for this article.


## Initial step: Have installed Docker locally and start a new TrailsJS repository

### 1. Trails has its installation instructions here: <a href="https://github.com/trailsjs/trails/blob/master/README.md" target="_blank">TrailsJS</a>.
    
  For Trails the followed configuration are the selected:
  
   - Express 4
   - ORM Waterline (By default it connects to a local disk structure) 
   - Automatic Footprints
 
  
  Additionally, it is created a basic model to give the chance to test how it goes in Docker.
  
  1. Create a model executing `yo trails:model user` in command line, it creates a basic `User` model.
  2. Define the required schema in `api/models/User.js` based on waterline structure:
      
     ```javascript
     static schema () {
       return {
         username: 'string'
         /* ... */
       }
     }
     ```
  3. It is required to enable the basic `dev` ORM connection located in `config/database.js` removing it as a comment in `dev` attribute inside the `stores` key.
  4. Finally is required to install the sqlite connector according to `dev` requirement by executing `npm install --save waterline-sqlite3`
  
  At this point a functional endpoint to `http://0.0.0.0:3000/api/v1/user` would be working loading the app by `npm start`
      
### 2. Docker has its installation instructions here: <a href="https://docs.docker.com/engine/installation" target="_blank">Docker Installation</a>

