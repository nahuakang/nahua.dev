+++
title = "Course 1 Lesson 3: Summary - Limitations of Information Flows"
date = 2021-01-03
slug = "course-1-lesson-3-summary"
draft = false
in_search_index = true
[taxonomies]
tags = ["openmined", "privacy", "privacy-preserving AI"]
+++

This post is a summary of Course 1, Lesson 3 of OpenMined's new private AI series, [Our Privacy Opportunity](https://courses.openmined.org/courses/our-privacy-opportunity) and covers the limitations of information flow, including the copy problem, the bundling problem, and the recursive enforcement problem.

<!-- more -->

> For a Google Doc version of the summary, [click here](https://docs.google.com/document/d/15qWAgbaXcyriJJio8__jGfahpr9UZjRx-I8mlloUUmA/edit?usp=sharing). Feel free to comment in the Gdoc to help improve the summary notes.

**Recap:** This course is about improving and fixing the information flows. To fix information flows, we must pinpoint and articulate exactly what is not working and what sub-problems are preventing us from having both improved privacy and transparency.

This lesson specifically discusses 3 types of problems:

1. The Copy Problem
2. The Bundling Problem
3. The Recursive Enforcement Problem

## The Copy Problem

**Definition of The Copy Problem:** If I share a piece of information, e.g. a document, a photo, or a video, with another party, I immediately lose control of how this other party might use the information later. To share the information, I must trust the other party.

**Challenges:**

1. Legal enforcement is difficult: Even though regulations such as GDPR are in place, it is extremely difficult to enforce that everyone complies with the law.
2. Limiting the power of computers: Truly solving the copy problem could mean limiting the power of our computer.
3. Surveillance: Or, machines must be able to detect when you are recording information that is not yours. That’d require very invasive surveillance software.

**Examples:**

1. The entertainment industry suffers from digital piracy. Digital rights management (DRM) software came into being to prevent your computer from playing files that you did not purchase. They represent a central authority threat to individual privacy. But if the creators cannot capture value from their creation, the industry suffers.
2. [Dropbox](https://techcrunch.com/2014/03/30/how-dropbox-knows-when-youre-sharing-copyrighted-stuff-without-actually-looking-at-your-stuff/) monitors what you upload and see if it contains copy-written material.

**Question:** _Given the problem and the challenges, should we stop the uncontrolled copying of data?_ No. Controlling copying is a double-edged sword. When you store other people’s information, you copy. Limiting this ability could have serious problems.

## The Bundling Problem

**Definition of The Bundling Problem:** It is often extremely difficult to share a piece of _intended information_ without revealing additional _unintended information_ to verify the intended information. This is also called **_data lumpiness_**.

**Examples:**

1. When you enter a bar, they check your ID and see your full name, date of birth, and address. But they only need to know that you are older than the legal age in your country! Technically, they don’t even need to know your exact birthday.
2. If you set up a home security system, the camera does not just record intruders but also every passing person and car, 24/7, 365 days a year. You have to hope that the majority of such video records are not misused.
3. In medical research, researchers usually only care about high-level correlations and don’t care about information from individual patients. But it is difficult to conduct research without being in the position to learn something about the individual patients.

**The Other Side of the Coin:** Alternatively, information that could be unbundled is not unbundled because the person in authority does not want it. For instance, is the CIA acting according to regulations and conventions in their clandestine operations overseas? The CIA can refuse such inquiries and state that they cannot unbundle information due to national security reasons.

**Takeaway:** The bundling problem is a key issue for data governance. It is important for designing information flow for accountability.

## The Recursive Enforcement Problem

**Definition of The Recursive Enforcement Problem:** When reinforcing data privacy regulations or accountability, we often end up in a never-ending recursive loop, where each authority that supervises other entities must themselves be supervised by an authority.

**Example:** If you are worried about an organization, like a PhD at a university that uses medical data to do research, you could ask a 3rd party authority to supervise (such as the PhD’s supervisor). But how would the supervisor actually detect that the PhD misuses the data? The data is on the PhD’s computer and they can do anything about it. For the supervisor to detect the misuse, the data must be on the supervisor’s machine and not the student’s. But this becomes very inconvenient for the student. Now, who’s watching the supervisor? We still need to monitor the supervisor to be watched. Then the university, but who monitors the university? This is the recursive enforcement problem.

**Question:** _Who makes sure that nobody is misusing data?_

**Takeaway:** This is also a core problem challenging data governance. Authority without authority is hard to solve when it comes to data because data must live on a single machine. But in the next lesson, we will discover how age-old political science ideas can help us solve this problem.
