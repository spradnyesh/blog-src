{:title "ml-101: Introduction to Machine Learning"
 :layout :post
 :tags  []
 :toc true}

Facts:

* As some of my friends on twitter and facebook know, I recently completed the "Machine Learning" course on [coursera](https://www.coursera.org/), taught by "Andrew Ng" from Stanford university. I managed to get a 100% score on the programming assignments and the review tests (mean attempt of 2.22 on the tests), but did not get a completion certificate because I missed the "completion survey" before the deadline
* While we teach, we learn.  -- Roman philosopher Seneca (see [this](http://en.wikipedia.org/wiki/Learning_by_teaching) [this](http://ideas.time.com/2011/11/30/the-protege-effect/), [this](http://ezinearticles.com/?The-Best-Way-to-Learn-is-to-Teach&amp;amp;id=560127), and lots more)

Combining these 2 facts I thought that it would be great to try and explain what I have learned during the last few weeks to all of you. This has the advantages of:

* My understanding of the subject will improve
* I've been having the "writers block" for the last 2-3 days, and was not able to think of what to write here on [Golbin](http://www.golb.in/). Problem solved ;)
* Maybe someone will benefit from this and will get inspired to try it out. Maybe I will get someone to collaborate on a project with, who knows?
So lets start! Wait! Before starting, let me put down a few notes:
* I have signed the "code of honor" on coursera, so do NOT expect to find assignment questions and answers to them here
* I will try to use different examples (than in the course) to explain. This is mostly so that by applying the concepts to different things, I believe I will be able to improve my understanding better

Ok, lets start now. Really start! First some definitions:

> [Machine Learning is a] field of study that gives computers the ability to learn without being explicitly programmed. &amp;ndash;Arthur Samuel (1959)

> A computer program is said to learn from experience E with respect to some task T and some performance measure P, if it's performance on T, as measured by P, improves with experience E. &amp;ndash; Tom Mitchell (1998)

The 2nd definition is a mathematically more well-posed learning problem, but maybe a bit more difficult to understand. The best way to understand the concept is through the following example: In 1959 Arthur Samuel created a checkers program even though he himself was not a good checkers player. What he did was for the program to play tens of thousands of games against itself, and learn from the various board positions that it encountered during the games. That is, when a program is not told the rules of the game, but learns them itself by observation, we can call it a machine learning program.

Machine learning is not a new field, but has been gaining a lot of interest and popularity in the last few years. It has grown out of "Artificial Intelligence" stream of computer science, but heavily uses other subjects like statistics for example.

In fact, today, machine learning algorithms are very pervasive, especially on the web. You are surrounded by them, although you might not notice them. Take the following for example:

* Every time you use [google](http://www.google.com/) search, you are using a algorithm that has been automatically learned by machine(s) to show relevant results to you
* When you use email, there is a spam classifier algorithm working in the background to automatically send spam messages to the junk folder
* Even the various ads that you see on web pages; some machine has learnt which ads it should show to you so as to increase the probability of you clicking on them
So what other kinds of programs can we write using ML?
* ML is very good for programs that we cannot write by hand; either because we don't understand the concept totally ourselves, or because it is too difficult to map the problem into the computer domain. For example, autonomous helicopter navigation, handwriting recognition, NLP (natural language processing), computer vision, etc
* Self customizing programs: When [amazon](http://www.amazon.com/) (or [netflix](https://www.netflix.com/), etc) shows you recommendations of what to buy next, this program should be different for every user. Obviously it is not possible to make a million different copies (with different behavior and hence algorithm) of the recommender program. ML shines beautifully when solving such problems
* Database mining: These days companies and organizations collect a huge amount of data (in terabytes), and in most cases we don't know what gems are hidden inside. This is where ML clustering algorithms can be used
* and the list goes on and on

So that's it for today. We will slowly dig deeper into the subject in the upcoming posts. So keep watching this space :)
