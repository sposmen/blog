---
layout : post
title : "Continuous Integration: Start from repo pushes"
subtitle : Initial bug insert prevention inside main repository.
category : tech
author : sposmen
tags :
  - continuous integration
  - tdd
  - bdd
  - git
  - hooks
  - pre push
---

In the last decade, there have been an increasingly change in software development processes. One of them is the well known Agile, and it's complementing technical practices, like, TDD and BDD which combined creates a good automation process and supports 
Continuous Integration. Here we can find lots of helping tips to enhance the process from the developer side.

The first contact in the continuous integration process is where a developer combine its own code with the code of others,through pushes to the unified repository.

The main purpose of this post is to give readers an initial tip to prevent bug insertions to  the main repository, by using the available hooks from the control version system. We'll use git in this article as an example.



### Initial step: Good TDD/BDD scripts

As good practice in the Agile process, TDD and BDD could be good players. This is the initial step on this process where a developer
writes it's acceptance and unit tests to validate his created code. This is usually ran through a command line. The important thing here is that it must
return to command line with the correspondent status, where _0_ is satisfactory and _1_ or others are being as unsuccessful execution.
'
To validate how it goes, the developer could run `echo $?` immediate after the test was run in bash terminal. This command shows the test script result.


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