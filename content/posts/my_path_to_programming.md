+++
title = "Remake Our Self: My Path to Programming"
date = 2020-08-30
slug = "my-path-to-programming"
draft = false
in_search_index = true
[taxonomies]
tags = ["programming", "career"]
+++

This is a long, detailed, and brutally honest post about how I became a software engineer.

<!-- more -->

In this post, I recount the failures that challenged me and the right choices I made that I am grateful for. It is written in self-reflection as well as self-meditation for a small circle of friends and acquaintances. Should you, a dear stranger, find any inspiration or consolation in my writing, I would feel a great sense of joy and achievement.

> I am writing this not for the eyes of the many, but for yours alone: for each of us is audience enough for the other.
>
> -- Epicurus

## TL;DR

It is challenging to start a career in software engineering without a background in a related university degree. It is certainly a rewarding path but, like my story suggests, we must have the conviction to work extremely hard, learn every day, set the right expectations, and continue re-making ourselves so that we could capture an opportunity when luck befalls on us. No matter what kind of career pivots we want to make, the key to success is to find the sweet spot between our passion and market demands through continuous learning and a lot of trials and errors.

---

Thanks to Silicon Valley, software engineering is one of the most (excessively) glorified lines of work in the 21st century. More and more people every day are curious about entering software from other fields.

I started programming in April, 2016. I began my software internship in April 2020. In July, 2020, I officially became a junior software engineer and joined the ranks of life-long learners who play and toil in one of the most dynamic, ever-changing fields.

This blog post is written mostly for myself. With feedback from my closest friends, I hope it represents a sincere, candid account of all the failures I faced, the right actions I took, as well as the personality I display in my pursuit to find career fulfillment.

If there were any external motivations for this post, then it would be to share my conviction that, regardless of what career you are interested in, learning how to **remake our _self_** by acquiring knowledge in unfamiliar territory and picking up new skills on the fly is one of the most essential skills we should learn today.

In another word, embrace knowledge that you are curious about, whether you studied it for your degree or not.

## Back to the Origin

My story began in the fall of 2006 when I entered one of the most prestigious high schools in Fujian, China with flying marks. In my city's annual high school entrance exam, I ranked as the top student in my middle school and among the top 30 best students. My blood was pumped with confidence and I felt I was a smart cookie destined for greatness.

{{ figure(src="/images/my_path_to_programming/hackers_and_painters.jpg", caption="Hackers & Painters", width="50%") }}

Around this time, I developed an admiration for **hackers** after reading the Chinese translation of Eric S. Raymond's blog post, [How to Become a Hacker](http://www.catb.org/esr/faqs/hacker-howto.html) and a few poorly translated chapters of Paul Graham's [Hackers and Painters](http://www.paulgraham.com/hp.html). A hacker's personality and character, as revealed by Raymond and Graham's writings, as well as the meritocratic nature of hacker communities deeply resonated with the yet-to-be-developed values I had. (_Note: Steven Levy's Hackers: Heroes of the Computer Revolution is a great book that I only encountered over a decade later._).

With encouragement from my high school best friend who knew programming already, I signed up for a weekend Pascal crash course offered by my high school. As I entered a room full of blue DOS screens on a fateful, humid Saturday morning, I was frightened.

Having grown up in a family that did not allow much time to play on a computer, I could not even type properly with five fingers at that time, not to mention using a DOS and writing `if-else` statements or `for-loops` in a dreadful language called **Turbo Pascal**! What's worse was that _everyone except me_ seemed to be able to follow the pace of the crash course!

{{ figure(src="/images/my_path_to_programming/turbo_pascal.png", caption="Turbo Pascal DOS Interface", width="60%") }}

For some reason, staring at that blue screen, I could not understand how a computer _thinks_. Nor could I write down any line of code to perform more than a standard:

```pascal
program Hello;
begin
  writeln ('Hello, world.');
end
```

I felt nervous, my head sweating. The teacher asked us to solve some more basic problems, but my brain felt like a overcooked pot of porridge. I sat there, stupified and petrified, while all the other students coded away, sharing their excitement with each other.

By lunch break, I sneaked out of the classroom and went home. I felt awfully stupid among some of the best students in my city.

In the subsequent weeks, I tried `Java`, `C`, and `C++`, languages my cousin was learning for his CS program at a university. Yet each time I did not know even how to install the software for these languages on my father's Windows PC. I tried writing code on paper, but even the simplest `#include <stdio.h>` seemed way too complicated for me, not to mention the verbose `Java`.

And then, sometime sooner or later, I gave up and concluded that I was not made for programming. From that moment on, programming became a painful reminder of that awkward, humiliating morning and my fragile ego could not allow the acknowledgement that I was not as smart as I thought.

## How I Started Learning Python

Fast forward to a decade later in 2016, I had already completed a BA in history from Texas A&M, with the prestigious _magna cum laude_ and the key to _Phi Beta Kappa_ honor society under my belt. Having no idea what to do with my life and with an aversion of preparing for the Law School Admission Test (LSAT), I was pursuing bachelor's studies in a prestigious business school in St. Gallen, Switzerland.

There, in that beautiful little Swiss town, I entered the most trying two years of my life. While my classmates were scoring interviews with the likes of UBS, Goldman Sachs, and McKinsey, I could not get a business internship either in Switzerland or Germany. In fact, from the numerous applications I sent out, I got only one interview and the company took the other candidate.

Nowhere. Stuck. I knew I missed something, but I could not tell what it was. Having been a star at Texas A&M, I felt like a complete loser in Switzerland.

Out of sheer luck, I got in touch with a Frankfurt-based value investor, an alumnus who was kind enough to offer me some time to _chat_. We had a pleasant conversation over coffee in St. Gallen's Altstadt, during which, however, he quickly determined that I lacked all the necessary financial and accounting knowledge to work as an intern for his fund.

Sensing his acute yet accurate judgement, I asked out of desperation: "_What kind of skills should I learn that would be valuable to your fund?_"

He replied: "_You could consider learning_ **Python** _and_ **programming** _for machine learning. Technology is coming into value investing as well now._"

I felt a knot in my stomach tying up instantly. Words could not describe my frustration and disappointment as I walked home. I called my girlfriend at the time with tears in my eyes, whining to her that the last thing in the world I would want to do is learning how to program again and this investor literally just told me I should learn _Python_ for programming. Beaten and defeated, I went to bed early that day but could not fall asleep.

{{ figure(src="/images/my_path_to_programming/roggwiller.jpg", caption="In Cafe Roggwiller, I sat with a kind investor in the middle lounge in the back of this photo when he told me to learn programming. I remember vividly how fear arose in me as I heard his advice.", width="60%") }}

The next morning, still with cloud in my mind, I bit my teeth and searched for online courses that would teach me `Python`. I found a few free resources, managed to install `Python` on my Windows laptop, and started programming.

Immediately, I realized that something was different: I did not feel dumbfounded like I felt with `Pascal`, `C` or `C++`. There was no mysterious, magical, scret code flying around the text editor. It was simple. My hello world program (in `Python2` syntax) was 1 line:

```python
print "Hello, world."
```

With still a lot of uncertainty and fear in me, I told myself that this time, I might actually get somewhere with `Python`. And that was the true story to how I started programming.

## Coding More and Encountering Deep Learning

I would like to sincerely thank Guido van Rossum and all the core `Python` developers because they created a beautiful language that is inviting to those of us who are frightened by `C++`.

After learning basic Python syntax and some programming concepts with the online book [Learn Python the Hard Way](https://learnpythonthehardway.org/python3/) and Coursera's [Python for Everybody](https://www.coursera.org/specializations/python), I gained some confidence in programming. I switched my operating system from Windows to [Ubuntu](https://ubuntu.com/), a popular distro of Linux, as a gesture of committing to coding as a lifestyle.

I didn't fall in love with programming yet. Sometimes, when I encountered a new concept that I could not understand, my fear of computer from 2006 would arise again and I had to give myself time to calm down and get back at the computer screen.

But for a student who felt stuck in his self-pity and stagnated career path, programming was weirdly liberating. And so, even making a useless, buggy text-based game in the terminal was a lovely distraction for me from the boring Economics exams that I had to memorize for.

Without any deliberate purpose, I learned more and more, such as how to dual boot Ubuntu and Windows, how to use the terminal and commandline, and how to write a small script to [scrap search results from YouTube and download YouTube videos](https://github.com/nahuakang/python-mini-projects/blob/master/youtube-downloader.py). The more I wrote, the more fun programming became. I knew no one would use any of the programs I wrote, but I was proud of them anyways.

By the fall of 2016, I made a calculated move of not completing my studies in St. Gallen but instead began my master's studies in Stockholm School of Economics. On the one hand, I wanted to close a long-distance relationship, on the other, I hoped that Scandinavia might offer opportunities to my stagnated career development.

Being the only student in my program who could _script_ in a general-purpose programming language, I went deeper and deeper into it. While my classmates were studying consulting cases, I hacked in my text editor and terminal to render a Hangman Game while learning how to modularize my code. While my classmates were partying and socializing in the evenings, I sat in a basement and continued learning with online math and programming courses. It brought me pride to be the only person who knew something about the magic in a computer among a bunch of business students.

{{ figure(src="/images/my_path_to_programming/malan.jpg", caption="David Malan teaches the world's best made online course, CS50, an introduction to computer science. (Photo credit: New Yorker).", width="50%") }}

Around this time, I completed [MIT's 6.00.1x and 6.00.2x](https://courses.edx.org/courses/course-v1:MITx+6.00.1x+2T2017_2/course/) and started doing [Harvard's CS50 course](https://cs50.harvard.edu/web/2020/), of which I eventually completed 70% of the homework. I love CS50 and its people. To this day, it is still the single best online course of any kind and I recommended it to all my close friends who wished to learn programming.

Soon after, I also discovered Udacity's new program on **Deep Learning**. Having no clue what deep learning is, I signed up for the course because it sounded cool (nowadays you can learn with free resources like [fast.ai](https://www.fast.ai/)). I learned about back propagation, convolutional neural networks, image classification, Long Short-Term Memory (LSTM), and Generative Adversarial Networks (GAN). None of that was easy and I definitely did not manage to do everything on my own. And wow! I could train a "neural network" to recognize digits in images!

Quite similar to my earliest experience with programming, I felt often dumbfounded with deep learning but I persisted because the subject was fascinating and because I thought I had no other competitive advantages.

## Failures After Failures, Until Luck Struck

To digest my learnings better, I started to write blogs. I was honored that the two pieces I wrote on the basics of deep learning ([post #1](https://towardsdatascience.com/introducing-deep-learning-and-neural-networks-deep-learning-for-rookies-1-bd68f9cf5883) and [post #2](https://towardsdatascience.com/multi-layer-neural-networks-with-sigmoid-function-deep-learning-for-rookies-2-bf464f09eb7f)) invited over **240K views** in total. (_Note: I never found the time nor energy to complete the third blog on backpropagation. Here's an amazing [post on backpropagation](https://colah.github.io/posts/2015-08-Backprop/) from Christoph Olah_).

These little successes boosted my confidence and I decided to look for interesting AI startups to apply for a **product, marketing, or bizdev** internship in Berlin. I thought about applying for engineering positions after reading [Lynn Root's story of her transition into engineering](https://www.roguelynn.com/words/my-path-into-engineering/), but I chickened out. Anyways, I reached out to all the startups I could find at the time.

The cycle repeated itself. I was either rejected or ignored.

I remember one startup that I applied to wrote back saying that they did not have a position suitable for me, yet I found out a month later that they hired another person from St. Gallen for a role that I was interested in. That hurt my pride in that moment but, in hindsight, never take these decisions personally. Startups tend to lack a large HR team to digest all the applications and sometimes, not being hired by the wrong employer is a good thing.

In my moments of frustration, Lady Fortuna befell on me. I reached out to Moritz, a complete stranger who at the time was the product owner of a deep learning startup, [TwentyBN](https://20bn.com/). By then, I had almost given up on finding an internship in Berlin and reached out only because Moritz's profile resembled mine and I thought I could seek some advice to my career path. I clicked the button on his LinkedIn profile and sent a short message.

{{ figure(src="/images/my_path_to_programming/linkedin_message.png", caption="A simple LinkedIn message changed my life", width="50%") }}

Little did I know that this message landed me an internship and a full-time job that eventually allowed and encouraged me to transit into software development. (_Note: In October 2017, before my internship with TwentyBN started, I briefly contributed to an open source project [OpenMined](https://www.openmined.org/) in an attempt to gain more experience in software. That experience also scared me because I did not understand Git, Github, unit testing, and CI/CD. I paused it in the excuse of work until April, 2020 when I became a software intern at TwentyBN._)

## Dissatisfaction with Career Path

I worked for 2 years as a product marketer and not for even a day did I feel it was my mission call. I took the job because I fully believed in TwentyBN's people and our technology, but I _dislike_ social media. I wanted to contribute to my company's success but never managed to change my mind about social media marketing. I did not grow much in this position and never felt fulfilled.

During this period of time, I went through an amicable breakup that nevertheless broke my heart. Moreover, I secretly felt my position was being marginalized in the company. My salary rose but deep in my mind, I was frustrated that I could not play a more meaningful role. That depressing feeling I experienced in Switzerland seemed to be rising again.

While a part of me continued to indulge myself in some ocassional evening coding sessions and nerdy programming languages activities, I did not consider software a possibility for me. And I felt I was already too old to go back to a junior position and start over again.

{{ figure(src="/images/my_path_to_programming/embodiedai.png", caption="I tried to change my career by being proactive with marketing ideas. This is a screenshot of the newsletter I led.", width="50%") }}

At work, I started writing and editing our company newsletter [Embodied AI](http://www.embodiedai.co/). In private, I started turning my reading list into book reviews and analysis on leadership in a newsletter called [Plutarch](https://plutarch.substack.com/).

With a desire to build a reputation of my writing, I started experimenting and trying to attract people to sign up for both newsletters. I tried all kinds of marketing channels, got banned by multiple Reddit subreddits, and eventually managed around **500** subscribers for Embodied AI and **100** subscribers for my personal newsletter.

With myself, I took a friend Chris's suggestion, overcame my gym-fear and started trying to weightlift and doing calisthenics, which was completely outside my comfort zone.

Fitness gave me dopamine and testosterone. But my newsletter attempts brought me no gratification. I continued and performed a variety of mini-experiments throughout a span of almost a year. Yet my career dissatisfaction continued.

## Never Too Old to Change Career

Towards the end of 2019, my long dissatisfaction with work manifested into an existential crisis (the coronavirus in 2020 intensified this crisis).

I came to one grim conclusion: **If I were to continue doing product marketing for another 10 years, I would end up hating myself for not taking any action.**

Again, this voice in my mind suggested software.

Already in 2018, I had wanted to ask TwentyBN for an internship as a deep learning engineering intern but I lacked the confidence to make the cut. And by the end of 2019, I heard enough success stories from acquaintances who landed software jobs after bootcamps that my desire to explore software engineering as a career re-kindled.

During my Christmas vacation back in China, I spent all the 3 weeks learning web development with [Harvard's CS50W](https://cs50.harvard.edu/web/2020/), coding from 8AM in the morning until 1 or 2AM in the night. I wanted to test myself with this intensive experience to see if I had it in me to be a programmer or if it were just a phase. The learning curve was steep and the great firewall prevented me from easy access to Google and StackOverflow. But I managed 2 buggy projects and learned some `Flask`, `Django`, `Javascript` and `WebSocket`.

{{ figure(src="/images/my_path_to_programming/programming_age.png", caption="This story persuaded me that I am not too old to make the career switch into software.", width="70%") }}

What was most transformational during these 3 weeks was that, for the first time in almost 14 years, I felt again I was **in the zone**. I was absorbed in programming. Throughout the day I was contemplating on solving the projects and problems. I even had 2-3 dreams during which I was finding solutions to my code.

And programming suited me way more than product marketing. By nature, marketing is a highly difficult line of work. Viral marketing and growth marketing are well-studied topics, but no one could say with 100% confidence if any single strategy or action was responsible for a product or a company's success.

Programming, however, is deadly logical. I was hooked into it because I enjoyed the instant gratification because, sometimes, even a single line of code change could result in a big visual difference. Bug-hunting, while sometimes tedious and frustrating, also gave me huge feelings of reward when I eventually debugged my code and consolidated my learning. This is way better than what I did in the past 2 years!

In the end, I worked so hard during those weeks that I did not hear about the COVID19 until I returned from China to Berlin.

Back at work, I decided that I was not too old to give software engineering a try. I managed to convince my boss Moritz, my Python teamleads, as well as my CTO Ingo to give me a three-month internship with pay reduction. Again, there were sleepless nights and numerous moments of head-banging. The paycut was manageable, but my nervousness of not making the cut and my **imposter syndrome** added a lot of pressure on my mind.

By now, however, my programming experience has taught me **what my learning patterns are** and I have become more patient with myself. I learned steadily, solved tickets, asked for help, and eventually, the internship turned into a new, full-time position.

## Remake Our "Self"

Having a family and good friends that unconditionally supported me helped. Having parents who value education and generously supported me in my worst moments helped. Having received a stranger's advice helped. Having learned programming and deep learning helped. Having been a history major with good writing skills helped. And having been on the same wavelength with my company's management and colleagues helped. All of that help was necessary.

But equally important, I also must thank Lady Fortuna for making me into **a person who has the drive to learn new, seemingly daunting skills to re-make oneself with discipline and tenacity**. Without this habit of continuous learning, I could not have achieved what I want.

As you might tell, my learning journey as a software Padawan has only just begun. Software engineering is a dynamic and energetic field with many talented people and brilliant ideas. I am still learning how to write good software and how to work across multiple teams.

{{ figure(src="/images/my_path_to_programming/twentybn.jpg", caption="TwentyBN and its amazing people", width="60%") }}

In April, I have reconnected with the founder of the open source project [OpenMined](https://www.openmined.org/). I began contributing in my limited capacity again so that to give myself more exposure to other programming languages to hone my overall skillset as a developer. It has not been easy but the OpenMined community is an amazing bunch.

Additionally, there are knowledge gaps that I have to make up for, such as architecture design, pattern design, as well as well-known algorithms and data structures. I am well aware of these gaps and will continue working on them. After all, I signed up for a career that only works if I continue to learn.

## La Fin

Most of us will not have a straightforward career that soars like the rocket. Most of us are destined to encounter career deadlocks at one or another point in our lives. And most of us have the power to do something about it.

For me, that included almost a decade of switching majors and wondering what line of work I would be passionate about.

It involved facing setbacks and rejections every stop of my journey across United States and Europe. It involved failing a major in business administrations and flunked two exams for the first time in my life. It involved being unhappy about my career path for 2 years.

But like Dickens wrote, **it was the worst of times, but it was also the best of times**. Thanks to all the people who are or had been in my life, I survived. Failures challenged my understanding of my strengths and weaknesses, but none of them destroyed me.

Each time I was struck down, I cried a bit, rose up, and found consolation in learning new knowledge and acquiring new skills. There was no giving up.

Here I am today. A new journey just began and I am excited about all the exciting things I will learn along the journey. I am very confident that failures and rejections of all kinds will continue coming my way. I am sure I will have moments of weaknesses and feel defeated. But I have gone through plenty to know that I am strong enough to withstand all of them and continue remaking myself and my life.

I hid most of these failures from others in the past years. A part of me is still ashamed of them. But I decided to write them down as a form of self-reflection. Moreover, I know someone out there is going through similar experiences. Perhaps these words will help.

So here you go. This story is for you and I hope, despite its length, my history resonate with or inspire you so that you can eventually also remake your life. Good luck and never give up.
