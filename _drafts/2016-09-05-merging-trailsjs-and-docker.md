---
layout : post
title : "Merging TrailsJS and Docker"
subtitle : Two emerging technologies living together.
category : tech
author : sposmen
tags :
  - continuous integration
  - trailsjs
  - docker
  - git
  - emerging technologies
---

Sometimes, when developers try to merge certain technologies, is difficult to find a good way to do it. There is where our team found a chance to
continue learning new things based on emerging technologies. In this particular case TrailJS combined with Docker is the goal for this article.


### Initial step: Have installed Docker locally and start a new TrailsJS repository

1. Docker has its installation instructions here: <a href="https://docs.docker.com/engine/installation" target="_blank">Docker Installation</a>
2. TrailsJs has its installation instructions here: <a href="https://github.com/trailsjs/trails/blob/master/README.md" target="_blank">TrailsJS</a>


### Second step: GIT pre-push hook

GIT have scripts hooks that help developers to automate certain requirements in specific phases of the version control process. `pre-push` is the
hook that it's the tangent point between the developer and the unified repository, and this is where we can prevent 
some bugs from being integrated into the application.
 
The location of the script is `PROJECT_GIT_ROOT\.git\hooks\pre-push` and each time a developer start a GIT repository, an example script called `pre-push.sample` is created as a template.

Here is an example on how to use this script to help  avoid bug insertions on a ruby project:

{% highlight bash %}
#!/bin/sh

# Go to the project root path
cd $(git rev-parse --show-toplevel)

# Here is where the test script must be executed
bundle exec rake test

# Return the final status of the test script
exit $?
{% endhighlight %}

### Final steps

- Check the script with `git push` command. You can do this  easily by emulating _0_ and _1_ from the pre-push script.

- The developer must adjust the script accordingly to his particular case (by running it's language build tools and tests).