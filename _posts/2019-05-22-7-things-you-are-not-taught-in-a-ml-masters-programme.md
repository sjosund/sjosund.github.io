---
layout: post
title: 7 Things You Are Not Taught in a Machine Learning Master's Programme
---
I started working at a ML start-up right after graduation and quickly realized that I was not prepared for it.
While I had graduated with a bachelor’s degree in engineering physics, a master’s in ML,
and had  a fair amount of knowledge about algorithms, the skills needed at a company were quite different from what I had learned at university.
At the workplace, there was limited value in being able to do complex integrals or prove convergence bounds,
while the ability to get things up and running with whatever means possible was crucial.

<br>
<a href="https://imgflip.com/i/2zursc"><img src="https://i.imgflip.com/2zursc.jpg" title="made at imgflip.com"/></a>
<br>

In hindsight, I don’t find it surprising that there’s a gap between what’s taught in universities and what’s needed in industry.
There’s very little exchange between universities and industry (in Sweden at least), and few lecturers have solid industry experience.
Thus, academia tends to focus on educating more researchers, rather than fulfilling the needs of businesses.

Luckily, our team acquired more senior developers, who helped me fill in many of the pieces that were missing.
Since then, I’ve had the fortune of supervising many recent graduates, thesis students, and junior machine learning engineers,
and I often recognize their challenges as the same challenges I once experienced myself.
So I decided to write this post, where I will share seven work practices that I believe are crucial when working with machine learning in industry,
but which tend to be overlooked at university. I believe that these things are beneficial to learn even if you’re still in academia.


## 1. Sharing code & version control
Use Git and Github (or equivalent) for all coding projects, no matter whether you’re working alone or in a group.
People break their code all the time (myself included), and it can be very tricky to backtrack to see why it happened.
If you periodically commit your code, it’s easy to go back to a working version. A very dramatic way of “breaking” your code is if you lose it.
I had one colleague who accidentally did `rm -rf` in the wrong folder, and a few who got their laptops stolen.
Neither of these was a catastrophe in terms of the work lost, as they had their work backed up on Github.

Using Github as code repository is also a [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) way of code sharing --
you always have _one_ master version of the code, which you constantly update your local code against.
Using git for this enables you to easily find and resolve clashes when you and your friend have changed the same parts of the code.

Finally, using Github makes it very easy to conduct code reviews, which I will discuss further below.
To learn more about version control, you can check out [this tutorial](https://www.atlassian.com/git/tutorials/what-is-version-control) from Atlassian.


## 2. Using virtualenv / conda
Once you have a few different projects going on at the same time on your laptop,
you will most certainly encounter the problem of clashing package requirements -- project A requires version x.y.z of a package,
and project B requires version u.v.w. This problem is especially prevalent as we’re still in the somewhat early days of deep learning,
and packages are not always stable. One solution could be to reinstall the package every time you switch projects, but who has time for that?
A better solution is to use [virtualenv](https://virtualenv.pypa.io/en/latest/) + [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/)
(or [conda](https://conda.io/en/latest/)) where you create virtual environments (VMs) for each of your projects,
where each VM can have different versions of the required packages.
A nice side effect of using a VM is that your project’s package requirement will be minimal,
making it easier and faster for others to get your awesome project up and running on their own machine.


## 3. Project planning, task tracking, and structuring your work
A good strategy for reaching any kind of goal is to first clearly specify what your goal is, break it down into smaller subtasks,
and solve them one by one. Doing this makes it easier to split up work between people, and makes large tasks seem less overwhelming.

A crucial point here is for you to clearly define what it means to complete a certain task, and to write that down explicitly.
Say that your task is to build an inference service for your new, shiny deep learning model.
Your definition of “done” might be “This task is done when it’s possible to send this specific image URL to the service,
the DL model process it, and returns the correct answer.” This is related to [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development),
which is another useful concept to learn.

When working with other people, you also want to have a DRY way of sharing the subtasks progress and splitting up the workload.
I usually use [Trello](https://trello.com/) for this -- it’s lightweight and very easy to set up. I’ve used this for everything,
from organizing my personal and professional machine learning projects to planning my wedding.

<br>
[ ![](/images/things-they-did-not-teach-you-at-uni/trello.png) ](/images/things-they-did-not-teach-you-at-uni/trello.png)
<br>

An alternative to Trello is [Github Projects](https://help.github.com/en/articles/about-project-boards),
which has the advantage of being seamlessly connected with Github issues.

I usually work with 3-5 columns in my Trello boards,
optional in parenthesis - TODO, In Progress, (Blocked), (Review), and Done.
- **TODO**: All tasks that no one has started.
- **In Progress**: The tasks someone is currently working on. I think it’s good to try to limit these to a maximum of 2 or 3 per person.
- **Blocked**: The tasks that are being held up for some external reason, like waiting for your bank to process some documents.
- **Review**: When working with others, this column contains finished tasks that are awaiting review.
- **Done**: The tasks that are completely finished.

Head over to [this interactive Trello tutorial](https://trello.com/b/I7TjiplA/trello-tutorial) to try it out for yourself.


## 4. Code Reviews
The basic concept behind code reviews is that once you’re done building some functionality, someone else looks through your code. This practice has several benefits:
- You’ll catch more bugs.
- You learn a ton. By looking through someone else’s code, you’ll discover new functionalities, new algorithms, and new ways of thinking around problem solving.
- It spreads knowledge about the codebase across the team. If someone is sick one day or quits, there will still be others who know and understand the code that person has written.
- It erodes your ego. To constantly have others point out how you can improve your code forces you to become humble and reminds you that there’s always more to learn.
- Related to the previous two, it prevents siloing. When a single person works on something for an extended period of time,
this person can easily grow very protective about the code and ideas that have gone into it.
This prevents others from correctly assessing a project’s progress and quickly catching when the person is stuck.

Code reviews are most conveniently handled through Github pull requests, or PRs for short.
A detailed walkthrough on how to get it started can be found [here](https://www.digitalocean.com/community/tutorials/how-to-create-a-pull-request-on-github).


## 5. Ensuring Code Quality

Having high quality code reduces the risk of bugs, makes the code easier to extend, and makes it easier for others to understand. A few ways of improving code quality include:
- Writing proper documentation for your functions.
- Making sure that you follow the code standard for the language that you’re using. (PEP8 for python.)
This doesn’t have to be cumbersome, as you can often use automatic tools such as the [⌥⌘L command in PyCharm](https://www.jetbrains.com/help/pycharm/reformatting-source-code.html).
- Using a [standard project structure](https://docs.python-guide.org/writing/structure/).
- Avoiding being too creative and witty with the naming of projects, classes, and variables.
A class named after someone’s favourite Pokémon might be entertaining for the person that wrote it, but it just makes the code base a lot more difficult to understand.
- Reading the excellent books [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) and
[The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-Journeyman-Master/dp/020161622X), which go into great depth about this topic.


## 6. Recognizing the differences between academia and industry

There are a couple of things that I find that surprise many people when first entering a company:

* Companies can spend money if it pays off. For example, your company can afford to buy you a shiny new GPU if that means you can work more efficiently.
Let’s say the cost of buying an [Nvidia RTX 2070](https://www.amazon.com/EVGA-RTX-2070-Black-08G-P4-1071-KR/dp/B07J9L4HC2) for US$500
corresponds to about 5-10% of your monthly salary. If that purchase makes you work 5-10% more efficiently,
the company will see a return on that $500 payment in no time.
* Data collection is often more important than algorithm innovation. As Kai-Fu Lee says in his book
[AI Superpowers](https://www.amazon.com/AI-Superpowers-China-Silicon-Valley-ebook/dp/B0795DNWCF):

  > “Given much more data, an algorithm designed by a handful of mid-level engineers usually outperforms one designed by a world-class deep-learning researcher”.

  ML in academia tends to focus on coming up with better algorithms. Standard datasets,
  such as [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) or [ImageNet](http://www.image-net.org/),
  are commonly used so that researchers can spend their time efficiently and enable comparison with other people’s research.
  Industry, on the other hand, focuses mainly on building products without any constraints on using standard datasets.
  As collecting more data is often the easiest way to increase your model performance, you'll put a lot of effort doing exactly this.


## 7. Using good tools, and using them efficiently
One of the easiest ways to boost your coding productivity is to start using a proper IDE.
I personally use [PyCharm](https://www.jetbrains.com/pycharm/) for python development and think that it’s great.
There’s a free version available that has most of the necessary features. A few of the basic features that you’ll soon wonder how you could live without include:
- Code completion
- Proper debugging tools. Print-line debugging no more!
- Refactoring: Easy and safe changing of variable names, files, and methods.
- Quick navigation, by jumping to or showing function and variable definitions. This is a huge one.

I’m also using the ideaVim plugin, giving Vim-like navigation and shortcuts. It takes a bit of time to get used to, but I highly recommend it.

I’m also hearing a lot of good things about [VS Code](https://code.visualstudio.com/docs/languages/python), but haven’t tried it myself yet.

Use the terminal as much as possible, rather than relying on the visual interface of your OS. While the terminal has a slightly higher threshold,
it’s usually a lot faster, more precise, and opens up the possibility of scripting frequent or tedious tasks. Also, take the time to learn the basics of Bash.

Finally, I really like the [Spectacle](https://www.spectacleapp.com/) app on Mac, which gives you keyboard shortcuts for resizing windows.
Overall for efficiency, I think it’s good to challenge yourself to use the mouse as little as possible.


## What's next?

To get the most out this blog post, here are some steps you could take to put things into practice. Pick a project that you’re working on, and then:
1. Create a [Trello board](https://trello.com) for free, and put all of your project TODOs there. (including the points below)
2. Clean up your project structure.
3. Create a repo on [GitHub](https://github.com) (public or private) and push your code there.
4. Install virtualenv locally and make sure you can get your code up and running from scratch in there. Document this process into a README file, which you also push to your repo.
5. If you’re working together with other people, start doing code reviews.
6. Write basic documentation on how to use your code and how your functions work.


## Conclusion
In this post I’ve talked about a few industry-essential work habits that are rarely taught in universities. To recap, these include:
- Implementing good practices for sharing and versioning your code.
- Isolating your dependencies using virtual environments.
- Planning your projects, breaking them down into smaller pieces, and tracking their progress.
- Doing code reviews.
- Improving your code quality.
- Understanding that the basic operating premises are different between university and industry.
- Making sure to use good tools, and learning how to use them efficiently.

If you start doing all of these things, you will find your efficiency increasing substantially, and your transition into industry will become a lot smoother.

Is there something I missed, or do you have something that you disagree with?
Let me know at [@sjosund](https://twitter.com/sjosund) or at &lt;Given name>.&lt;Surname without the dots above the o>@gmail.com.


If you found this blog post helpful, please share it with friends, classmates or colleagues!
