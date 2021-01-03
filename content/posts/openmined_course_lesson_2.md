+++
title = "OpenMined Course 1: Summary - Society Runs on Information Flows"
date = 2021-01-03
slug = "openmined-course-1-lesson-2-summary"
draft = false
in_search_index = true
[taxonomies]
tags = ["openmined", "privacy", "privacy preserving tech"]
+++

This post is a summary of Course 1, Lesson 2 of OpenMined's new private AI series, [Our Privacy Opportunity](https://courses.openmined.org/courses/our-privacy-opportunity). For a Google Doc version of the summary, [click here](https://docs.google.com/document/d/1A8efR94WzNcgE1XBjWI7zknCJc2oyxF--dGTzQwduQ4/edit?usp=sharing). Feel free to comment in the Gdoc to help improve the summary notes.

<!--more-->

Towards the end of 2020, I was approached by the OpenMined team to help out on writing the new [private AI series courses](https://courses.openmined.org). Unfortunately, given professional and private reasons, I could not contribute to the course development. Therefore, I hope to write and collect notes from the courses and offer them as my minor contribution to this open source community that I love and believe in.

---

Privacy is fundamental to our lives, yet for the past three decades since the rise of the internet, each individual has lost a large chunk of their private information to companies as well as political entities.

For instance, social media platforms collect and analyze large amounts of user data or sell them to other companies. Some governments collect data via mass surveillance programs to monitor their citizens. News networks are increasingly known to offer biased opinions and misinformation to their audience based on information about their target audience’s political beliefs and social values, thus polarizing society to the two extremes on the spectrum.

But despite hearing so much news and debates about privacy, how do we actually define this concept? What does information flow have to do with privacy? How should we respond to social media platforms and other service providers that violate our private data? Should private data be kept absolute private? Or can we utilize some form of technology to safely share data for social good? What are some serious problems caused by bad information flows and violation of privacy? How do some societies and communities solve these challenges?

These are some of the questions that this lesson tries to discuss. Below are the notes.

## Information Flow

**Gist:** Society runs on information flow, which is everywhere. From supranational organizations down to individual groups of humans, we live our lives and make decisions based on information that flows across different channels.

**Definition of Information Flow:** A flow of bits from a sender to receiver with some probability. This probabilistic nature matters because you often don't get to share a piece of information exactly to one recipient. Unintended recipients are involved.

**Example:** Imagine Andrew is gossiping with Emma in a pub, thinking their conversation is private. The pub is loud and Emma only hears bits and pieces of Andrew’s voice. Meanwhile, by coincidence, Nahua sits in the booth next to them and overhears parts of the gossip.

## Privacy

**Gist:** Privacy is about the (_appropriate_) flow of information, not necessarily about the information itself.

**Definition of privacy:** Privacy is not about simply keeping information private, but rather the ability to ensure flows of information that satisfy social norms.

**The Concept of Contextual Integrity:** The best definition of privacy is coined by Helen Nissenbaum as the concept of Contextual Integrity. Contextual integrity's core aim is to provide a description for when people feel that their privacy is violated. If you use a piece of data from someone and they care about how you might use the information from the data, then you’re using private data. It does not matter if this piece of data is labeled “private” by law or not because privacy is about the flow of information in context of social norms.

**Example:** Each human face is a public information because every time you go out into the world, your face is public and can be viewed by anyone who passes you. However, facial recognition software is controversial and troubling. This is because the identification of faces is without consent. The information is not necessarily private, but the information flow is highly inappropriate in the context where people do not expect their faces to be used for identification software or, worse, surveillance purposes.

**Conclusion:** Privacy is not just about private information leaking out, but also about public information that might become even more public. Some information flows in a way that people do not expect or do not like. It’s about expectation of how the data flows.

## The Importance of Data and Privacy

**Gist:** Data is fire. Privacy is about data. Privacy matters even to the people who think _“I have nothing to hide.”_

**Data-is-Fire Analogy:** Data is compared to oil and electricity by many renowned researchers and journalists. We say data is fire because:

1. Data can be shared unlimited number of times
2. Data has its dual use for both good and bad.
3. Data is ubiquitously present throughout the society.

Why care? You may have nothing to hide right now but, at a certain point in your life, you might have **_changes in life_** that you don’t want others to know about, such as medical records.

Also, given the rise of highly powerful machine learning models, AI can infer or predict information about an individual from seemingly non-sensitive or unrelated public information. All this information can be used for **_targeting_**, i.e. advertising, targeted disinformation, or even deliberate physical harm.

**Anonymization does not work:** Anonymization is important because knowing or not knowing the identifying information would protect an individual from certain types of targeting. However, data anonymization does not work anymore. It cannot protect individuals because you don’t even need the ID or the name of a person to target them! As long as you know enough about a person and have a way to reach them, you can target them.

Example: Fitness app Strava has collected anonymized user data and generated a heatmap, which [outlines the exercise routes of military personnels](https://www.bbc.com/news/technology-42853072) in bases around the world. The data is anonymous but it reveals important information that could not only harm individuals but national security interest.

## Privacy & Transparency Dilemmas

**Gist:** Data is fire. So there exists a constant trade-off on whether to reveal sensitive data for social good, such as medical research that would solve certain illnesses, or social hazard, such as leakage of sensitive data or mass surveillance. The trade-off involves privacy and transparency dilemmas, which are two sides of the same coin.

**Privacy-Dilemma:** A lot of data can generate social good but is prone to violation of individual privacy and malicious intentions.

**Transparency Dilemma:** Too little data might protect individual privacy but negatively impact the decision-making process and the accuracy of a decision.

**Privacy-Transparency Trade-Off:** This trade-off underpins many societal challenges as it is historically a [Pareto trade-off](https://en.wikipedia.org/wiki/Pareto_efficiency), i.e. where one gains, the other loses. The important question here is: _Can we get more of both instead of a zero-sum game? How can we remove this Pareto trade-off for industries that could benefit from this hurdle to generate social good?_

**Example:** Too much private data leakage could lead to companies knowing too much about their customers without the customers’ consent. [Target figured out](https://www.forbes.com/sites/kashmirhill/2012/02/16/how-target-figured-out-a-teen-girl-was-pregnant-before-her-father-did/) a teen girl was pregnant before her father did because of too much private data being collected and analyzed. However, maximizing privacy can lead to a lack of transparency. Each person must make a decision based on limited information and social proofs. How do you know if a product you buy on Amazon is good or not if no other user provides any information of their experiences? Or if the product reviews might be fake? The information you need to make a decision exists but you might not have access to this information flow, or the information flow exists but the output isn’t verified.

## Areas Where We Urgently Need Solutions to Privacy-Transparency Trade-Off

### Research:

Research is almost always constrained by information flows.

**Example:** Deep learning researchers rely heavily on data. They often have to build and collect their own datasets. They want to collaborate with each other and ensure that the methods they develop are robust, not biased, and can generalize on data across the population. To make sure the tools work, researchers must foster a transparent environment to ensure data is used for good. Meanwhile, they must also ensure that the data being used will remain private.

To empower researchers to make breakthroughs across disciplines and generate social good, we need the solution to solve the privacy-transparency tradeoff.

### Healthy Market Competition for Information Services

Any services that handle users’ personal data are services that benefit from _locking you in_. These services are anti-competitive by nature because of data privacy. So the privacy-transparency trade-off is a **lose-lose scenario** for the customer and the market is not competitive. These companies often have a strong incentive to centralize user data into silos. As a consumer, you are often locked in for good.

**Question:** _Is locking all data down the solution to privacy?_

The sharing of data has two very subtly different scenarios:

1. A user switching services and brings data with them due to user-specific interests.
2. A company gets user consent to sell data to other companies due to its profit-seeking interests.

The current popular narrative that _“data should not be shared at all”_ is in the interest of some of the most privacy-intrusive companies. Such narrative, if written into law, would enable companies with private data to become monopolies because users can no longer switch services easily.

**Interoperability:** What we need is an improvement in interoperability among service providers. Interoperability means that you can buy your shoes from one company and socks from another. Computers are very interoperable. We can always make computerized systems to be interoperable. But the law surrounding computers prevents interoperability, and can be even a crime. So dominant companies can decide who can interoperate with them, resulting in a _lack of market competitiveness._

**Example 1:** Interoperability is the reason how many startups got hold of their grounds. Facebook was interoperable with Myspace via password and messages. That was adversarial interoperability. Myspace users could send or receive messages with friends from Facebook or vice versa.

**Example 2:** GDPR is an example that empowers consumers and improves interoperability. GDPR gives consumers 7 rights, including _the right of access_ (send you a copy of all your data) and _the right to be forgotten_ (approach companies to delete almost all your data). GDPR makes companies more responsible and accountable for handling user data.

**Conclusion:** The simple narrative that “locking all data down could solve the privacy problem” can backfire on our goal to improve privacy. If we want to protect privacy, we need organizations to be forced to share information in many cases, especially when a user wants to switch services. This allows privacy concerns to drive market competition. In the end, satisfying privacy can also be about forcing companies to share information in the way you want them to. It’s about stopping flows that are harmful and forcing flows that are beneficial.

### Data, Energy & the Environment

Energy is a field where privacy-transparency trade-off affects public good. Coordinating energy demand on a nationwide scale requires serious collaboration efforts.

The ability to analyze data on the energy grid is important. Smart meters can help people become smarter about their energy usage. Greener, low-carbon future depends on our ability to use such data wisely.

But this can be very privacy-invasive as the data could be used to draw out a detail about a household’s activities and behavioral patterns, such as when you are home or not and what you are using (even what TV channels you are watching). It could become a form of mass surveillance. So we need to have systems that ensure the privacy-transparency trade-off for such collaboration.

**Example:** Data coalitions in Taiwan. In Taiwan, citizens have air boxes at home to detect air quality due to air pollution blowing from China. In this space, public environmental polity is low but private environmental polity is high. So private Taiwanese citizens gather together to pull data together to learn from each other and then use that pool of data, which the government does not produce but desires, to bargain for what citizens want: More units of such installation in public parks, military areas, etc.

**Conclusion:** It is possible for millions of people to collaborate on a large scale to solve urgent challenges.

### Feedback Mechanisms & Information Flows

**Feedback Mechanism** is everywhere and is the bedrock of our society because each individual navigates their social settings via signals from feedback mechanisms. We have always relied on each other to make daily decisions, such as which car to buy, which restaurants to go, etc. Individual actions are influenced by social forces.

**Examples:** Amazon product reviews, presidential elections, protests, Facebook likes, imprisonment or punishments, gossips are all feedback mechanisms.

But because of the privacy-transparency trade-off, many feedback mechanisms are broken. Sometimes feedback information is so sensitive or valuable that it can be misused for malign purposes. Lack of feedback mechanism can sometimes lead to alleviation of someone’s accountability for certain actions completely, paving the way for openly malicious actions.

**Example:** How good is your surgeon when you go into surgery? Where could you get feedback about the surgeon? How much feedback could you get? If you cannot get the information easily, the feedback mechanism is probably broken.

### Democracy & Healthy Public Conversation

**Public squares:** In the past, a public square for political debates or discourses could be a pub or a town hall. Today, public squares become more symbolic and virtual: Social media, TV channels, door-to-door activists are all forms of public square.

**Problem:** A trend nowadays is the polarization of political opinions among a nation’s population. This is caused by the privacy-transparency trade-off and the mal-functioning of information flows.

**Example:** [Taiwan used a platform called Polis](https://www.theguardian.com/world/2020/sep/27/taiwan-civic-hackers-polis-consensus-social-media-platform) to optimize for consensus and unity among people, improve public discourse, and cut through noise and trolling on the internet.

**Conclusion:** We can have a community-build, consensus-facilitating platform that informs government on the desire of people and helps the people to update themselves based on what they learned about their community. Social media does not have to divide us. All we have to do is to optimize tech to bring people together. We can build novel information-flow systems that benefit society.

### New Market Incentives

Incentives are heavily intertwined with information flows.

**Example:** Attention is the most dominant incentive on the internet. Netflix, Facebook, and most internet companies seek attention and optimize for attention (even [human sleep is seen as a competition for Netflix](https://www.theguardian.com/technology/2017/apr/18/netflix-competitor-sleep-uber-facebook)).

**Problem:** Companies lack proper heuristics to measure their successes. Measuring attention is the best heuristic for these companies because attention reveals a huge amount of information about each individual. Attention is the most readily available and successful metric on the internet.

**Ideation on Incentives:** We must, however, have better heuristics to measure than attention. After all, customer loyalty is more important than attention for Netflix. But how would Netflix adjust itself? Wellness metrics are such details that Netflix could use but they are not readily available. So Netflix cannot optimize for these wellness metrics. Customers end up being the losers who are addicted to the platform and could become sleep-deprived. Therefore, we must have safer information flows to help companies establish proper incentives that do not generate a negative impact on their customers.

### Safe Data Networks for Business, Governance and R&D

**Example:** Developing EU-wide products and services requires EU-wide data access. Data must be able to flow easily across the EU and be used in a productive and safe manner. Such data flows can be beneficial especially in situations like a global pandemic.

**Question:** What’s the ideal information flow? Why not entirely free-flowing?

First of all, trade secrets must be protected. Secondly, a country’s data is also crucial for that country’s national security and economic prospects. So who controls the data matters. Anonymizing data isn’t enough. Therefore, data cannot be allowed to free-flow across the EU.

**Ideation for Solution:** Ideal information flow of sensitive data should be that the data is only shared in a privacy-preserving manner. But sharing data across space means that we still have a data governance problem. What if the data does not have to move? What if one nation holds the data and another can access it remotely in a privacy-preserving manner? Today, we have technology, such as differential privacy, that enables such privacy-preserving sharing of data without the data leaving its physical storage. This can maintain the trust for safe EU-wide data collaboration.

### Conflict, Political Science, and Information Flows

From your problem with your significant other to the worker’s union against enterprises to wars among nations, conflicts are everywhere in our everyday life.

**Mutual Optimism:** [“Rationalist explanations for war”](https://web.stanford.edu/group/fearon-research/cgi-bin/wordpress/wp-content/uploads/2013/10/Rationalist-Explanations-for-War.pdf) is the most famous work on why nations enter war with each other. It coined the term mutual optimism, which suggests that wars occur when two countries’ leaders have simultaneous, overly optimistic estimations about how they’d fare in a military action.

**Privacy in Political Conflicts:** There’s private information involved about willingness of a nation to go to war. For instance, if nation A knew that it had developed a new weapon that it believed nation B did not possess, this is a piece of private information that could affect the decision-making process.

**Ideation:** But what if two nations could be able to determine the result of the war somehow before they launched their missiles and instead negotiate to settle? No blood is drawn and conflict could be resolved.

**Problem:** Since neither side has all the information to make a proper estimation of the outcome of a potential war, each side might think that they have the upper hand. So we need an approach to reveal such secret information without each party actually leaking the sensitive information to the other party while being able to estimate an outcome of a conflict.

**Example:** 3rd party negotiation for Indo-Pakistan conflict (_Note: the video clip was not available in the lecture_).

### Disinformation & Information Flows

**Disinformation:** Often in life, we are reliant on what we are told. Is what we are told actually true? These days, we rely on entire strangers on the internet to tell us information. Additionally, centralized global news networks have a tremendous influence in disseminating information to people. Society’s most important feedback mechanisms rely on such information. So whether the news is true or not is one of the most important questions out there.

**Freedom of Speech** is fundamental to democracies. Historically, freedom of speech centered around the analog form of communication. Communication at scale was not a problem and you could only be heard at scale via a trusted communicator. Freedom of speech was by default not to be immediately heard by everyone in the world. You could still be heard by everyone, but it would not be instant. Information was shared among trusted networks and filtered.

**Freedom of Speech at Scale:** Scale is achieved by the social networks built via the internet. Now everyone can push a button and be seen or heard by the whole world on social networks. This tremendous reach redefines the information flows facilitated by the freedom of speech and leads to mass misinformation.

**Question:** So what should happen if a piece of information is false?

There are many proposed solutions. Some suggest asking social networks to self-censor. Some seek solutions in machine learning models. None of these are long-term viable approaches because of the **information bottleneck**. Or, one could get off social networks and never use them again. But there are better ways to tackle this problem.

**Example:** [Taiwan got citizens activated](https://foreignpolicy.com/2020/11/11/political-disinformation-taiwan-success/) to help each other understand the limitation of information. Not taking things down, but adding comments to other sources. The comments come from users related to a reader. So the community is watching out for everyone in it and helping each other. Also, [humor over rumor](https://qz.com/1863931/taiwan-is-using-humor-to-quash-coronavirus-fake-news/) when fighting misinformation:

1. First, framing of the challenge is less about identifying lies and taking them down, but more about fostering a national community that helps each other to filter truths from lies. Volunteers help their local communities by commenting on posts.
2. Second, Taiwan uses humor to foster trust in the civil society to discredit fake news.

**Conclusion:** When thinking about disinformation, it is important to take into account how society has historically dealt with the problem. We cannot think just in a pure technologist approach. Removing a social network won’t fix the problem. It’s a fast removal but not solving the cause of the problem. Don’t choose the most scalable option but scale a movement of everyday people bringing trust and care into each other’s life. What’s the most compelling way to activate people to help their friends? That’s the good question to ask. It’s not a new issue. We’ve dealt with it before. Seek to use technology and scale these existing mechanisms so that the society is more ready to adopt the solution.

## Takeaway

Privacy technology is not just about privacy but about creating information flows in society that maximize social good.

When thinking about privacy and the uses of privacy, don’t ask just where do we need more privacy but ask how can our society accomplish a goal with less risk, higher accuracy, faster speed, and more aligned incentives through better flows of information.

It’s not about hiding data but enabling specific data flows to empower researchers, governments, and citizens.
