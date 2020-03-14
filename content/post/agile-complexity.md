+++
title = "Complexity and the Art of Story Pointing"
date = "2020-02-02T18:42:44-07:00"
author = "Erik Goodman"
categories = ["Software"]
tags = ["agile"]
lastmod = "2020-03-13"
+++

# Complexity and the Art of Story Pointing

This blog assumes readers are familiar with Agile methodology. If you are not, 
[agilenutshell.com](http://www.agilenutshell.com/) has a pretty decent, brief overview.

## The Murky Waters of Consensus

Recently several teammates were in a heated argument around story pointing. We were trying to define "What makes
something a one-point story vs. a three-point story?". Afterall, if we can't agree on the simplest of story ratings,
what hope do we have to ensure we can estimate larger stories with any accuracy? These two individuals had fundamentally 
opposed philosophies which I refer to as "Categorical" and "Dynamic".

## Categorical

The Categorical Pointer wants to define parameters to group types of changes into point-categories. This _feels_
like a good idea, because it gives a team some common reference points with which to point user stories and provides a 
solid base to discuss around. It can make planning meeting go quicker as once a task has been identified, categorizing the 
task into bucketed point groups is quick. It can also help developers when writing user stories as it allows
a team to break down a feature into common, relatable tasks.  

Examples:
- A "text-only" change is 1 point
- A change "requiring testing" is automatically 3 points
- A new class is 5 points
- A new API is 8 points

There are a few issues to consider with this approach.   


The first problem with the Categorical approach is that it can influence story writing to drift from _user_ stories
around deliverable features into _technical_ stories where the documentation is about the underlying software details. 
It's easier for many developers to immediately focus on the technical solution of "add option Foo to the widget dropdown"
rather than write the story from a User's perspective as to _why_ we want Foo and what that [accomplishes][1].
I believe this approach is attractive because it can make the story writing meeting go quickly, but it also removes
developers from a key part of software development: compassion and understanding for the users of your software.
It allows a development team to say "we are building this feature because we were told to, simple enough."  


A second issue is that this approach misses the intention of User Stories. Story points are not inteded to be firmly grounded,
as what a team is capable of delivering should improve over time. By focusing points on specific implementation details, teams
run the risk of going down the road to saying things like "well I can do X in half a day, since that's a one point story then 
I can handle `<insert magic formula here>` 16 points this sprint. Since we have 5 engineers, that means we should take in 80 
story points." I have seen many, many teams try to estimate pointing stories _while_ arguing that story points don't relate to 
develolpment time. This road only leads to sadness. 


Finally, basing story points on implementation categories usually focuses on only one part of the
full scope of creative work: Complexity. Complexity alone can certainly affect the duration it takes to complete a task,
but it's only one component that feeds into the overall amount of work to be done. The Dynamic model considers
complexity but stirs in a few other considerations to the pot.

## Dynamic

An alternate approach is to remove the technical implementation entirely from the intention of a user story. 
Start by breaking down the request into its constituent parts and consider the [various spheres of work][2] 
needed to accomplish the task:
- Volume: How much is there? 
- Complexity: How hard is it? 
- Knowledge: What’s known?
- Uncertainty: What’s unknown?

This establishes a fuller picture, but comes at the cost of slowing down the planning process.
That said, I'm of the opinion that slowing down the refinement meetings is not always a bad thing. It can
balance the developer's desire to avoid meetings as much as humanly possible and get back to the fun stuff
with the need of making sure everyone really knows what the actual work is. I also think most engineering managers don't
truly want to micro-manage devs and would like to trust them to just do their work within a reasonable timeframe. The
only way to do that though is by understanding what is reasonable for a particular task, team, and individual.
"What is reasonable" is extremely contextual and will change frequently, and essentially boils down to determining
what we mean to say something is "complex".

# Complexity

When discussing the Categorical approach, I know said that it only focuses on the complexity aspect of a user story.
The truth of the Dynamic approach is that these four functional areas _are themselves just different aspects of complexity_! 
The impetus for this article was overhearing one developer state "If I have to make a simple text change like adding an 's' 
to a word and I have to do that 100 times, it's still a 1-point story because it's _a simple text change_; not something 
complex. It's just a lot of repetition" and my ears perked up immediately. I can hear you screaming that tools like sed 
or find/replace in an editor would make this trivial in many cases, but work with me here! By virtue of being human, 
we quickly lose interest and focus on repetitive tasks and this blows the door wide open for mistakes to be made. Or if you're 
like me, you start down the rabbithole of "hm, this is boring, how can I script this?" and well then we're 
right back to sqaure one...

![xkcd: Automation](https://imgs.xkcd.com/comics/automation.png)  
[xkcd: Automation][3]

(yes, yes, tools like sed or find/replace in an editor would make this trivial in many cases, but work with me here)


## Sounds right, but show me the math

Ok, I think we're ready to put some numbers to this problem. Given the problem of "adding 100 `s`s" to a document, 
how complicated is that in reality? To calculate this, we can start by creating a string containing all the entries 
we intend to make. Our target string looks like this:
`ssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss`

How concisely could I express this string in a message so that you understand the full contents? Using English I could say "100 s characters".
16 characters. That's not too bad, it's way less than the 100 we started with, but we can do better. I could use a hypothetical 
compression algorithm to express it as "100*s", so long as you knew in advance how to decompress my message to interpret its 
contents. Down to 5 characters, much better! If one half of this string were replaced by the letter `j`, our target string is now
more complicated. "50 j characters then 50 s characters", or "50\*j+50\*s", 36 and 9 respectively. And what if instead of two
different characters, the string was split using three? And what if instead or being ordered, the letters were randomly 
distributed throughout the string? Oh dear we are starting to get in trouble. We quickly lose the ability to compress the data
meaningfully, it contains a lot of information! This is the general idea behind [Claude Shannon's source coding theorem][4], it's 
really interesting and worth a read if you've stuck with me through to this paragraph!

We can analyze this scenario in Information Science by identifying the information quantity present in the message. This is referred to as 
the Entropy of the message, A.K.A randomness or surprise of an event. Looking back on our target string, how much surprise is there?
None! If you selected any character at random from the target string, the probability that it will be `s` is 100%. 
No single character tells you anything different from any other character.

The calculation for [Shannon entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)#Definition) is thus:
![Shannon Entropy.png](https://miro.medium.com/max/933/0*a50ZrZrpo_Ny7MGG.png)

The Wikipedia page for [Entropy (information theory)](https://en.wikipedia.org/wiki/Entropy_(information_theory))
provides a lot more context for what this equation is doing and why. To give a feel for what it's on about, let's find the entropy
at the event of a fair coin toss. We know the probability is equally split 50% between Heads and Tails, and we can only have 1 of 2
possible outcomes. Plugging this into our equation above gives us `H(x)=-(1/2 log_2(1/2) + 1/2 log_2(1/2)) = log_2(2) = 1 bit`. 
Repeating this for a fair dice roll ( 6 options, each 1/6 probability) is simplified to `log_2(6)` or ~2.6 bits. The uncertainty
of any particular result increases as our potential results increase.

So in this ideal, [spherical-cows](https://www.wired.com/2011/02/what-is-up-with-the-spherical-cow/) sort of world, my first colleague was correct! Any randomly-selected character
in our target string has a 100% probability to be `s`, regardless of how long the string itself is. This gives it a entropy
value of 0: no information, no randomness, no complexity. Unfortunately cows in our world have legs and horns and agency to move around.
Studies have shown that when typing or entering characters, humans have an error rate of [0.01][5] indicating that one
of these 100 values (if entered one at a time) is likely to _not_ be `s`. And it's not like the fair coin example above, where
we only have two potential outcomes. There are myriad ways to mistype beyond accidentaly selecting a key's neighbor. One could enter the
right key in the wrong place, double-press the key, not press hard enough and mis an entry altogether, or hit the correct key and its neighbor.
Each of these require different action to remedy and I have no idea about the likelihood of each specific type of error.
To make things a teensy-bit simpler I'm going to assume that we only have two outcomes, an expected outcome (letter `s`) and
a suprise out come (anything else). Calculating entropy this way gives us `-(99/100 log_2(99/100) + 1/100 log_2(1/100))` or 
*0.08*. Ok, well that number feels pretty anticlimactic given how far we've come. Regardless, _Entropy is not zero!_ Mistakes
happen and it's naive to presume just because something sounds simple, that's all there is to it.

 
# Conclusions
Many thousands of words have been written on Agile methodology in software development and many thousands more are being
written at this moment. There's no way any single blog post could cover the full spectrum of topics, and I must stop somewhere. 
If you take one thing away from this essay I hope it is to challenge that story points are not a measure of _complexity_ of a task,
there are many additional factors to consider. The points are relative only to themselves and will change between teams
and over time within a team. And that's ok! Story points are just an estimation, and an estimation should not be
considered a contract or a guarantee about what can be delivered in a given timeframe. Before a team can
provide reasonable estimations on a task, they must first speak the same language around task estimation. Only then can
discussions around predicatability and accuracy begin.


# Fun Things
Well, since I'm already aboard the XKCD train, it's hard to have a conversation about complexity in tech circles
without referencing the seminal XKCD comic on password strength as it nicely sums up what it is I'm trying to
communicate:

![xkcd: Password Strength](https://imgs.xkcd.com/comics/password_strength.png)  
[xkcd: Password Strength][6]


The second password is better cryptographically because it is more complex from an information science perspective and
simpler for people to remember. "Easy to remember" doesn't make it less prone to mistakes on entry. I would bet any
typist would be more likely to make a type in the four-word example rather than in "Tr0ub4dor&3" if for no other reason
then they would need to _focus_ on the latter and would fly through the former, another common source of human error.


Alternatively if you are more of the gamer-type nerd than the programmer-type nerd, Ceave Gaming released this
incredible video on creating a combination lock in Mario Maker 2 that discusses some of the same principles. This
is more relevant for the discussion on "complexity" rather than human error and Jira tickets, I still highly
recommend watching the whole vid, it's great!

{{< youtube aSlstPpIW-E >}}


# Further Information

- Explain xkcd 936: Password Strength https://www.explainxkcd.com/wiki/index.php/936:_Password_Strength  
- Entropy (information theory): https://en.wikipedia.org/wiki/Entropy_(information_theory)  
- The Information by James Gleick: https://www.goodreads.com/book/show/8701960-the-information  

[1]: https://www.mountaingoatsoftware.com/agile/user-stories "User Stories"
[2]: https://www.scaledagileframework.com/story/ "Story - Scaled Agile Framework"
[3]: https://xkcd.com/1319/
[4]: https://en.wikipedia.org/wiki/Shannon%27s_source_coding_theorem
[5]: https://www.lifetime-reliability.com/cms/tutorials/reliability-engineering/human_error_rate_table_insights/
[6]: https://xkcd.com/936/
