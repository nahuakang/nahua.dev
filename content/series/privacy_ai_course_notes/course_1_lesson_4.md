+++
title = "Course 1 Lesson 4: Summary - Structured Transparency"
date = 2021-01-06
slug = "course-1-lesson-4-summary"
draft = false
in_search_index = true
[taxonomies]
tags = ["openmined", "privacy", "privacy-preserving AI"]
+++

This post is a summary of Course 1, Lesson 4 of OpenMined's new private AI series, [Our Privacy Opportunity](https://courses.openmined.org/courses/our-privacy-opportunity) and covers topics on structured transparency, including input/output privacy, input/output verification, and flow governance.

<!-- more -->

> For a Google Doc version of the summary, [click here](https://docs.google.com/document/d/1qez3zK_-BUz4iI1tM81Xd5nBwtFIkmljWr-6LlBfCxk/edit?usp=sharing). Feel free to comment in the Gdoc to help improve the summary notes.

This lesson focuses on solutions.

## Introducing Structured Transparency

**Definition of Structured Transparency:** The goal to enable desired uses of transparency without enabling misuse. Gain the benefits of transparency in a structured approach.

**Examples:**

1. Secret ballots are a form of structured transparency: Allowing citizens to vote for their political beliefs without being subjected to shaming or verbal/physical assaults.
2. Sniffer dogs alerts about contrabands such as drugs and bombs without announcing what else is in the luggage.
3. Researchers trying to detect genuine nuclear warheads drew inspiration from progress made in cryptography (transfer of knowledge across disciplines).

**Importance of Solving Structured Transparency:**

1. There has never been a greater need for structured transparency. The rise of digital technology allowed the collection of analysis of sensitive information at an unprecedented scale. It presents an enormous threat to privacy and social stability.
2. There has never been a more promising time to solve structured transparency thanks to techniques that are being created, developed, and improved. But this requires cross-disciplinary knowledge synergy.

## 5 Components of Structured Transparency

Components:

1. Input privacy
2. Output privacy
3. Input verification
4. Output verification
5. Flow governance

Input privacy & input verification are guarantees for the input information flow. Output privacy & output verification are guarantees for the output information flow.

Input privacy and output privacy are guarelates referring to information in the flow that must be hidden. Input verification and output verification refers to information that should be revealed in a verifiable manner.

Flow governance is about who can change the flow as well as who is allowed to modify the input/output privacy and verification guarantees.

Focus on the goal rather than the technique for implementing the guarantees.

## Input Privacy

**Definition:** A guarantee involving one or more people so that they can participate in a computation in such a way that none of the parties can know anything about any other party’s input to the computation, intermediate variables, or outputs other than the output specifically designed for them.

**Examples:**

1. You write a letter, seal the envelope, give it to the post office. The post does not need to know what you wrote in the letter to deliver it to its recipient. The input privacy here is that the mailman won’t be able to see your input in the process of facilitating your information flow.
2. Special case: If your letter is addressed to the mailman’s mother and, upon receiving the letter, she reads the letter aloud to the mailman, does the mailman violate input privacy? No. Input privacy only counts if the information flow is in process.

**Takeaway:** Input privacy only guarantees protection of the input through the information flow and the intermediate variables in the information flow, but not the outputs. Nor does it matter if the mailman saw you writing the letter before sealing the envelope.

**Important:** Input privacy is the pipe that does not leak. If the water you pour into the pipe leads back out to you, it does violate input privacy and only means that the flow is designed to output to you as a recipient.

If input privacy is satisfied, both the copy problem and the bundling problem can be solved.

### Tool 1: Public Key Cryptography

**Definition:** A branch of cryptography allowing a piece of information to be encrypted and decrypted using a pair of keys: a public key and a private key. It’s a straight one-way pipe to the recipient. Your private key only protects information sent to you.

**Example:** In secure messaging, you generate a public and a private key. The private key is never shared with anyone but the public key is broadcasted to anyone you want. Your public key encrypts messages in a way that only your private key can decrypt. Therefore, no matter who intercepts the message, only you can decrypt the message.

### Tool 2: Homomorphic Encryption (HE) for Input Privacy

**Definition:** A magical tool (a set of algorithms) for 3rd parties to perform computation on _encrypted data_, without decrypting the data or knowing what actual information is in the data. This means you can delegate others to compute on your encrypted data in a secure approach without them gaining any unintended knowledge of you.

**Important:** The output of a homomorphically encrypted data will always be encrypted with **_the same key as the input data_**. HE allows service providers to give their users a guarantee of privacy so that the users truly stay in control of their own information.

Imagine a bank allows you to store your money encrypted by HE. The bank would not know how much money you have, but you can still withdraw or deposit money as normal, knowing how much money you have.

**HE is very general-purpose:** multiple parties can use some information encrypted with a public key and run various computation and programs on the encrypted data. The encrypted output of all these operations can only be decrypted by who has the corresponding private key. We can also store information in HE-encrypted manner, waiting for computation later on.

**Question:** What could you never do that was too risky? That’s where you can use HE.

### Tool 3: Secure Multi-Party Computation (SMPC) for Input Privacy

**Definition:** SMPC defines any algorithm where multiple parties can calculate the output of a function while keeping their inputs secret from each other. It’s a formal group of algorithms that satisfy input privacy.

**Additive Secret Sharing:** One of the most interesting SMPC algorithms. It allows multiple people to share ownership of a number and solves the copy problem.

**Example:** Take a number `5` and split it randomly into `-1` and `6` to give to Bob and Alice. The numbers add up to `5`, but each number on its own does not reveal information about number `5`. The relationship between the two numbers, however, stores the information of `5`. Unless you have both shares, you will not know more about the number. The copy problem is solved because neither Bob nor Alice knows the number they store means `5`. It requires 100% consensus among the shareholders to decrypt the information. It’s a shared control over number `5`. But both Bob and Alice can perform meaningful computation on the numbers they hold on behalf of the actual number `5`. Since everything can be boiled down to numbers, files, videos, and more can be encrypted in this approach.

**Nuances for HE and SMPC:** HE and SMPC excel in different contexts. SMPC puts a huge load on the network among shareholders but requires low computational resources for each computer. HE does not require high network computation but must do a lot of computational steps to keep the data secure. If you have low internet speed and a powerful computer, HE shines. If you have high internet bandwidth but less powerful computers, SMPC shines.

## Output Privacy

**Definition:** If there exists an information flow with input and output, how much insight can someone gain on the input by reverse engineering from the output. Even an information flow that perfectly satisfies input privacy can leak insights of its content since input privacy only protects the pipe that sends the information, not before or after.

Output privacy ensures that certain attributes of the input information do not leak from reverse engineering of the output. It is chiefly concerned with the bundling problem, conveying exactly and only what the central message is without revealing additional information.

### Differential Privacy

**Definition:** Differential privacy provides output privacy in a very specific context: _aggregate statistics over a large group of people_. DP makes it possible to disentangle learning about the population as a whole from learning idiosyncratic information about individuals in the population.

**Example:**

- Suppose Andrew wants to know about the average age of all students participating in Course 1. A privacy-intrusive way is to ask everyone to type in their age. Andrew does not need to know each person’s age to get the information.
- Even if we use HE to provide input privacy, Andrew could still find ways to reverse engineer. Suppose Andrew learned that there are `1000` students in the course and the average age is `27`. Now, Andrew excludes you from the email and asks the other `999` students to re-submit their age. Assume the new average age of the other `999` students is `27.007`. Oh, now Andrew knows you are around `20` years old `(1000 * 27 - 999 * 27.007 20)`.
- Alternatively, Andrew could pretend to be the other 999 students and asks you to give him your encrypted age. The end result is the same: Andrew can reverse engineer and obtain information about you.
- Now, with DP, what if you get to pick a random number from `-100` to `100` to add to your age first before encrypting it and sending it to Andrew? So say you are `30` and add `-50` before sending `-20` to Andrew. That makes no sense? But interestingly, if you have good randomness, then the average of the random numbers people choose will approach `0`. A few random numbers can be noisy, but infinite choices between `-100` and `100` cancels out the noise.
- Andrew now can average over all the “ages” of the class to get close enough to the true average age of the class, but he has no way to reverse engineer anymore. So maybe Andrew knows you submitted `-4`, but...he learned nothing about your true age since you could have picked any numbers from `-100` to `100`.

### Robust Output Privacy Infrastructure

**Epsilon (`ε`):** Measurement in differential privacy. The more randomness people add to their data, the better the privacy protection is. So we need to be able to measure a strong versus a weak privacy protection. For instance, the range of `(-100, 100)` is better than the range of `(0, 1)`.

**Privacy Budget:** A hospital with `3,000` patients wants to let researchers use patient data to cure cancer. How does the hospital ensure that no researcher could reverse engineer the output they get from a ML model back to individual medical records that served as input? By giving each researcher something called a **_privacy budget_**.

**Important:**

- Privacy budget is a measure that ensures that all the results a researcher generates from the input data must, when taken together, represent less than ` X ε` of information. `X` is a measure of your maximum tolerance for information reconstruction risk. If you are not too worried about someone trying to reconstruct your data, you could set `X` to `100`; but if you are really worried, you could set it to `1` or `0.1`. It does not matter what specific algorithms the researcher uses as long as it can be measured by `ε`, you get a formal guarantee that by the probability that a researcher can reconstruct your data from the statistical results.
- We just mentioned that every researcher gets their own `ε`. Suppose there are `10` researchers and each of them receives `20 ε` of privacy budget, does that add up to `200 ε`? What if the researchers pool their results together? In theory, if they combine the results in the right way, they could achieve as much information leakage. If this is a concern, you should track a **`global ε`** against all researchers who work with your dataset. But if you are not worried about researchers pooling results together, then an individual basis for privacy budget should be fine.
- Now, think from the perspective of a patient. How does `ε` apply to you? If you are a patient at `2` hospitals and both hospitals allow researchers to use data about you? If each hospital allocates `20` of information about you, then there could be `40` information about you leaked out! Just because your hospital doesn’t think they leak private information about you does not mean they don’t actually leak it.

**Example:** Netflix used to run the biggest anonymized dataset for machine learning competition. They replaced movie titles and usernames with random numbers. So Netflix thought user privacy should not be a problem. Well...if only IMDb did not exist. IMDb also keeps a big list of movies and a list of users. Sometimes people post their ratings about a movie on IMDb while posting ratings about the same movies on Netflix. So Netflix released some `ε` of information about its anonymized users. IMDb leaks a lot of `ε` about some overlapping users. So much `ε` is in the public that some researchers could successfully launch a **_deanonymization attack_**.

**Question:** How much `ε` should we care about? Transform `ε` by calculating `β = e ^ ε`. If a medical study guarantees no more than `2β` will be released. If `β` is `2`, pick any event in the future (your partner leaving you, your insurance premium raised, etc.) and `β` guarantees that if you participate in this medical study, the probability of that event going up is `2x` current probability. From the perspective of DP, the guarantee does not care whether the event seems related. So the probability of an event happening after you participated in this medical study will be **_no greater than `β` times the current probability_**.

**Takeaway:** is our protection, a formal upper bound of bad things that can happen to you in a statistical analysis (surveys, usage on Chrome, Firefox, texting apps, or health monitoring apps, etc.).

## Input Verification

Now you may wonder, with all the input & output privacy techniques in place, if I’m doing data science and cannot look at the data, how do I know I’m training on data that I’m supposed to train on!? How do I know if the information is good or true?

**Definition:** Input verification is about verifying specific attributes of input to an information flow.

**Internal Consistency:** refers to when someone in the real world can recognize how things are usually constructed and laid out. Internal consistency is what people look for when they examine for fake-ness. It’s one of the most powerful tools for communicating trust.

**Problems:** Use internal consistency to verify the authenticity of an information flow output has 2 major problems:

1. With enough effort, internal consistency can be faked (e.g. dollar bills can be faked, DeepFake can fake images, videos and audios).
2. It requires sending more information than is required for communication. It necessitates information leakage!

### Tools: HTTPS

**Question 1:** What tools exist that can allow us to verify a piece of information that ideally can’t be faked and does not require revealing other information in the process?

**Examples:**

1. The internet is one of the most powerful input verification technologies deployed. You asked the internet for a URL and servers around the world help you find the correct server to render the website for the URL. “A man in the middle attack” is a hack that disrupts such input verification. It takes one person in the middle of the chain to change the message you send and receive back, especially for the internet.
2. The little lock in your URL field indicates that you loaded your webpage using HTTPS, which represents the most important tool for input verification: **_cryptographic signature_**, a kind of signature that solves input verification.

**Cryptographic Signature:** _Remember public & private keys?_ You create a pair of public and private keys and you broadcast the public key to the entire world so that they can send you messages. But we hide our private keys because our private keys allow us to sign a signature in a way that no other key could do and only our public key can verify. As long as the recipient holds your public key and your signature, they know it’s from you.

**Question 2:** _What does the signature mean?_ Just a mark attached to an object that is affiliated to us that only we can mark. Unlike real-world signatures, digital signatures are sent in a separate file that is called a **_certificate_**.

**Question 3:** _So back to the original topic, how do I know that webpage content coming back from all the passing hands of servers is the actual site I typed into my URL field?_ Every signature is on a certificate registry on the web. The signature attached to this webpage content can be verified against the signature in the certificate registry. So only the owner of this webpage content can sign the signature, not the “man in the middle”.

**Question 4:** _But can’t someone just find out the signature in the certificate registry and copy it!?_ Well...signatures are protected by **hash**. Hash is a big, deterministic number. Given two inputs that are the same, the hashes are the same. But two the inputs vary just slightly, the resulting hashes won’t be the same. So when the original server signs a webpage before sending it to you, it hashes the whole webpage into a single number and creates a signature for that number so that signature is unique to that webpage. No one could use that signature for anything else. If a “man in the middle” changes a single character in the webpage content, the signed hash wouldn’t match the page so the signature wouldn’t match.

**NOTE:** [This video](https://www.youtube.com/watch?v=T4Df5_cojAs) really helps if any of the notes above is complicated.

### Tools: Active Security & Zero Knowledge Proofs

Now we know there are tools that ensure input verification in the information flow, but can we somehow perform computation on the input along the pipeline and still maintain the verifiability of the input without corrupting it?

Yes, two approaches can fix this issue, verifying a flow and its input:

1. Zero-Knowledge Proofs.
2. Encrypted computation (e.g. homomorphic encryption, etc.) with Active Security.

If a computation is agreed upon, then a signature can be created when the information within an information flow is processed such that there is cryptographic evidence allowing everyone who participated in the computation that their involvement is included in the output. This approach can be used for machine learning or voting or other activities.

**Important Points:**

1. **A public/private key pair doesn’t have to be tied to an exact identity.** It could be tied to your anonymous identity. Others don’t need to know who you are or what your gender is or what your name is. They just need to know that you are that random person who is consistently signing with that key pair. The key pair can even represent a group of people, not just you. So you can identify as a member of a group without disclosing your exact identity.
2. **You can have an infinite number of public/private key pairs.** If you wish that not everyone can tie you down to an exact key pair, you can use multiple key pairs to communicate with different people.

### Reputation:

If you are a data scientist and you are connected to 365 data owners who claim to have access to breast cancer data. Since the data is private, you cannot peek into it. They all charge you `$10/day` to train ML models on their data.

**Question:** How do you know which of the data from the 365 data owners to train on?

First, some of them might already be entities, such as well-known hospitals, that you know and trust. What about the other data owners? If you are the very first person to work with this strange data owner, you won’t know. You have to be the first to try it. If you trained on this data and evaluated the model on another well-known dataset, then the data probably worked and you can leave a review for this data owner, proofing that you did the analysis with a **_signature_**. Now the world has someone who left cryptographic evidence that they evaluated the data from this data owner.

A second person came along and saw your review and they tried, leaving a review. Then the third came along, and the fourth. They all signed that this dataset, which we cannot see, is good.

**_[Note: this bit is a bit hard to take notes on]_** All that you had to go on is a bunch of anonymous reviews on a secret dataset. **_Since you cannot invent trust out of nowhere._** You can take a tiny bit of trust, try it, review it, and scale this trust to the whole community.

## Output Verification

**Definition:** The guarantee that output from a hidden information flow (with hidden input transformation) contains the properties that we want. It is one of the most important components of structured transparency because it enables us to verify that an algorithm is desirable.

**Examples:**
DL models might be biased or unfair because of the intrinsic bias built into the datasets they are trained on. There are ethical concerns about these models. Therefore, we should develop techniques to assess the model outputs for bias or unfairness.

**Question:** _If all the decisions in the world are made by humans by hand, do we know whether any particular decision is made in a fair way?_

If there’s a procedure being followed, we could evaluate the procedure. But if the person made it based on gut feelings, then we enter a slippery slope. To truly know the mind of a person who made a decision is close to impossible.

A Formal Set of Procedures: So it is quite clear to us that human brains, similar to ML models, are blackboxes. We have procedures for what people can or cannot do and use procedures to ensure that their decisions are fair and just. This brings the decision and the decision-making process out in the open.

**Takeaway:** Law is a formal set of procedures. An algorithm is a formal set of procedures. Algorithms, with the right output verification technique, can become vastly more transparent than human brains. Algorithms might not be ready for all cases, but they present a long-term potential to help society to become more transparent. It is, after all, easier to audit an algorithm than the human mind.

## Flow Governance

**Question:** _If an information flow that achieves input privacy is set up, who has the ability to turn the input privacy guarantee off? Same for output privacy, input/output verification._

**Definition:** Without proper flow governance, the integrity of the other 4 guarantees can be entirely at risk.

**Examples:**

- **Public key:** If Andrew sends Nahua a message, Andrew would use Nahua’s public key to encrypt the message. The content of this message is now governed by Nahua, who holds the secret key to decrypt the message. Other people can steal or store the message but the content of the message can only be used by Nahua. This is **unilateral governance**. One key holder, one person that controls the data.
- **Homomorphic Encryption:** If someone hands you a bit of information encrypted with their public key, you have some governance over the data: You can compute over the encrypted information and transform it. You cannot act on it in the real world but you still have some more power than if it were encrypted by public keys. The decryption still belongs to the person holding the private key. Governance to act on a piece of information in the real world lies with the one entity that holds the private key.
- In Secure Multi-Party Computation, we have **consensus governance:** Only when all parties agree on some computation, would the computation be allowed. Each shareholder has veto power to stop an information flow from happening.
- What about a governance of democratic majority? This is called **_threshold schemes_**. You can set an arbitrary percentage so if enough shareholders agree, they have enough cryptographic permission to perform some computation. Groups of people, given checks and balances, are possible to work together towards a shared goal.
