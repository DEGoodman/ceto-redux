+++
title = "Complexity and the Art of Story Pointing"
date = "2020-02-02T18:42:44-07:00"
author = "Erik Goodman"
+++

# The Murky Waters of Consensus

Recently several teammates were in a heated argument around story pointing. We were trying to define "What makes
something a one-point story vs. a three-point story?". Afterall, if we can't agree on the simplest of story ratings,
what hope do we have to ensure we can estimate larger stories correctly? These two individuals fell solidy into
different camps, which I will label "Categorical" and "Dynamic".

## Categorical

The Categorical Pointer wants to define parameters to group types of changes into point-categories. This initially seems
like a good idea, because it gives a team some common language around user stories and a frame of reference to start
discussions and ease conversations around discussion. It can also help developers when writing user stories as it allows
a team to break down a feature into common, relatable tasks.  

Examples:
- A "text-only" change is 1 point
- A change "requiring testing" is automatically 3 points
- A new class is 5 points
- A new API is 8 points

There are a few problems to consider with this approach.   

The first problem with the Categorical approach is that it can influence story writing to drift from _user_ stories
around deliverable features into _technical_ stories where the documentation is about the underlying software details. I
find this is very common with more junior developers, where it's easier to say "add option Foo to the widget dropdown"
rather than write the story from a User's perspective as to _why_ we want Foo and what that [accomplishes][1].
I believe this approach is attractive because it can make the story writing meeting go quickly, but it also removes
developers from a key part of software development: compassion and understanding for the users of your software.
It allows a development team to say "we are building this feature because we were told to, simple enough."  

The second problem is that pointing stories based on implementation category usually focuses only on one part of the
full scope of a story: Complexity. Complexity alone can certainly affect the duration it takes to complete a task,
but it's only one component that feeds into the overall amount of work to be done. The Dynamic model considers
complexity but stirs in a few other considerations to the pot.

## Dynamic

An alternate approach is to remove the technical implementation entirely from the user story. Start by breaking down the
request into its constituent parts and consider the [various spheres of work][2] needed to accomplish the task:
- Volume: How much is there? 
- Complexity: How hard is it? 
- Knowledge: What’s known?
- Uncertainty: What’s unknown?

This establishes a fuller picture, but can (and will!) slow down the process of taking a story and getting it ready to
be worked. That said, I'm of the opinion that slowing down the refinement meetings is not always a bad thing. It can
balance the developer's desire to avoid meetings as much as humanely possible and get back to the fun stuff,
with the need of making sure everyone really knows what is going on. I also think most engineering managers don't
actually want to micro-manage devs and would like to trust them to just do their work within a reasonable timeframe. The
only way to do that though is by understanding what is "reasonable" for a particular task, team, and individual.
Discussions around storypointing are one way to help set expectations.

# Complexity

In many ways, these four functional areas _are_ just complexity, only in disguise. The impetus for this article was 
overhearing one developer state "If we have to make a simple text change like adding an 's' to a word, and have to do it
100 times, it's still a 1-point story because it's _a simple text change_; not something complex, just a lot of
repetition" and my ears perked up immediately. (side note: I mistyped when writing the example and accidentally entered
a 'd' instead of an 's', it happens!!) By virtue of us being human, we lose interest and focus quickly on repetitive
tasks, and blows the door open for mistakes. Or if you're like me, you start down the rabbithole of "hm, this is boring,
how can I script this...?"

![xkcd: Automation](https://imgs.xkcd.com/comics/automation.png)  
[xkcd: Automation][3]

(yes, yes, SED or find/replace would make this trivial in many cases, but work with me here!)


## Sounds right, but show me the math!
I'll spare you the deeper lecture on entropy (see example 1 in the next section for that), but one quick and directly
relateable way to demonstrate this is via [Claude Shannon's source coding theorem][4]. Given the problem of "adding 100
esses", how complicated can that really be? 
Well, if all of the characters are entered correctly and in the right place, we could (very simplistically) define the
entropy of this change as:
`ssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss`

There's a lot of repetition here, so much so that any individual letter doesn't meaningfully contribute to the
information that 100-character string is trying to relay. A more useful view (from an information science perspective)
would be to compress it so that we know the details of a) what letter we have and b) how many times it's repeated. A
simple way to calculate the entropy of this data is to calculate `a^b` where a is the number of symbols and b is it's
length (see example 1 in the following section for a more complicated and real-life example). 
In this example, we arrive at `1^100`, giving us an entropy value of 1, no real complexity. 

Studies have shown that when typing or entering characters, humans have an error rate of [0.01][5] making a single error
here highly likely to occur once at some point during this task. I'm presuming the likliest error is a straight 1-1
substitution of keys entered, but there are myriad ways to mistype beyond selecting a key's neighbor like entering the
right key in the wrong place, having a modifier key pressed, entering a space, double-pressing the key, not pressing
hard enough, etc. If the task became even slightly higher in volume or included a slightly larger set of characters to
enter or a slightly more complicated scenario in which to place characters, the complexity of the change becomes
massively larger. If even just one of those letters are mistyped, then the system is already twice as complex!  
`1^99 + 1^1 = 2`

Now, this is purely to demonstrate a point. There is a whole fractal world of math and theory you can dive into,
maybe som will make it to a blog post on another day. I will include some references at the end. If you are at all
interested in Information Theory I encourage you to check it out, it's interesting stuff!

## Examples
Well, since I'm already aboard the XKCD train, it's hard to have a conversation about complexity in tech circles
without referencing the seminal XKCD comic on password strength as it nicely sums up what it is I'm trying to
communicate:

![xkcd: Password Strength](https://imgs.xkcd.com/comics/password_strength.png)  
[xkcd: Password Strength][6]


The second password is better cryptographically because it is more complex from an information science perspective and
simpler for people to remember. "Easy to remember" doesn't make it less prone to mistakes on entry. I would bet any
typist would be more likely to make a type in the four-world example rather than in "Tr0ub4dor&3" if for no other reason
then they would need to _focus_ on the latter and would fly through the former, another common source of human error.


Alternatively if you are more of the gamer-type nerd than the programmer-type nerd, Ceave Gaming released this
incredible video on creating a combination lock in Mario Maker 2 that discusses some of the same principles. This
is more relevant for the discussion on "complexity" rather than human error and Jira tickets, I still highly
recommend watching the whole vid, it's great!

{{< youtube aSlstPpIW-E >}}


# Conclusions
Many thousands of words have been written on Agile methodology in software development and I'm sure many thousands more
will come.  There's no way any single blog post could cover the full spectrum of topics, and I must stop somewhere. If
you take one thing away from this essay, it should be that Story points are not a measure of _complexity_ of a task,
there are many additional factors to consider. The points are relative only to themselves and will change between teams
and over time within a team. And that's ok! Story points are just an estimation, and an estimation should not be
considered a contract or a guarantee about what can be delivered in a given timeframe. Before a team can
provide reasonable estimations on a task, they must first speak the same language around task estimation. Only then can
discussions around predicatability and accuracy begin.


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
