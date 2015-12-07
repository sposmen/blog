---
layout : post
title : "Continuous Integration: Start ensuring from repo pushes"
subtitle : Initial bug insert prevention inside main repository.
category : tech
tags :
  - continuous integration
  - tdd
  - bdd
  - git
  - pre push
---

Last decade have been an increasingly change in software development process. One of them is the good known Agile. 
And, complementing its principles, TDD and BDD increases its force combined with a good automation process with
Continuous Integration. Here is where there are always helping tips to the process in the develop side.

The first step, where a developer combine its own code with others, is through pushes to the unified repository.

Main purpose of this post is to give readers an initial bug insert prevention inside main repository.

On this case it will be used GIT for its hooks structure.

### Initial step: Good TDD/BDD scripts

As good practice in the Agile process, TDD and BDD could be good players. This is the initial step on this process where a developer
generates the code to validate its created code. Usually it is ran through a command line. The important thing here is that it must
return to command line with the correspondent status, where _0_ is satisfactory and _1_ or others are being as un-success executions.

To validate how it goes, the developer could run `echo $?` immediate after the test was run in bash terminal. This command
shows the test script result.


### Second step: GIT pre-push hook

GIT have scripts hooks that help developers, or development process, to automate certain requirements. `pre-push` is the
above mentioned because it is the tangent point between the developer and the repository, and there is where could be
prevented (as initial point) some bugs being integrated within an application.
 
The location of the script is `PROJECT_GIT_ROOT\.git\hooks\pre-push` and each time a developer start a GIT repository
there is created an example script called `pre-push.sample`.

Here is an example of this script helping to avoid bug insertions

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

- Check the script with `git push` command. It could be easy to check emulating _0_ and _1_ from the pre-push script.

- Finally, the developer must play accordingly to his particular case.