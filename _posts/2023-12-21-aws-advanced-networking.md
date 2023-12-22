---
layout: post
title: AWS Certified Advanced Networking - Specialty
---

Today I passed the AWS [ANS-C01 exam](https://aws.amazon.com/certification/certified-advanced-networking-specialty/), earning the Advanced Networking - Specialty certification:
[![aws-adv-net-badge](https://images.credly.com/size/680x680/images/4d08274f-64c1-495e-986b-3143f51b1371/image.png)]({{ site.baseurl }}/aws-advanced-networking)

[Validate](https://aws.amazon.com/verification) with code ```YBV2R0RLY1F4QN99```

I have updated the [Certifications page]({{ site.baseurl }}/active-certifications/).

My main prep for the exam has been extensive experience over the last ~8 years, designing/implementing/troubleshooting countless AWS VPN and/or Direct Connect setups/migrations. My main area of responsibility has typically been customer on-prem network devices, on the other side of the VPN/DX, however I've often had to help out on the AWS side of things.

Initially this would be from customers providing screenshots or screen sharing on a troubleshooting call - for the cases where they manage their own AWS environment - where I would be able to offer more guidance as familiarity built up. But since Rackspace also [manage AWS environments](https://www.rackspace.com/newsroom/rackspace-technology-wins-three-2023-aws-partner-awards), for these cases I am able to login to the AWS console and view the resources and their configs/states, in order to gain a complete end to end view of what I'm working on from the data center(s) on the other side, which is invaluable when trying to troubleshoot an issue, or fulfil a request where this additional context completely changes how you decide to solve it.

I've had to build several proof of concept solutions, and lab up various scenarios as part of this work, where I've configured the AWS side of things from scratch, so this built up a strong understanding of VPN, DX and TGW, as well as common use cases such as S3 access. In addition, I've had the privilege of assisting numerous solution architects putting together all sorts of different solutions involving DX, so am familiar with all of the associated limitations and features, and how they have changed/improved over the last ~5 years by keeping track of all the relevant new announcements (this in itself probably deserves a separate post - for a long time my preferred way to do this has been using Slack with RSS feeds (```/feed```) using a separate channel for each feed category with custom keyword notifications.) so had a strong head start for the first and largest of the four exam domains:

• **Domain 1: Network Design (30% of scored content)**

• Domain 2: Network Implementation (26% of scored content)

• Domain 3: Network Management and Operation (20% of scored content)

• Domain 4: Network Security, Compliance, and Governance (24% of scored
content)

I should clarify that at no point in my career have I been specifically focused on AWS over the other hyper clouds, however they have in my experience been the most commonly used cloud provider by customers. If I had to estimate I would say now for ~50% of hybrid connectivity cases, which is a little lower compared to a few years back, as Azure and especially more recently, Google setups have been increasing.

So while I was mostly covered for what I would loosely refer to as the main topics of the exam with the above, there were several products and topics which I had not touched at all before, at least in AWS.

In order to fill the gaps, I worked through the AWS Skill Builder [Networking Core - Knowledge Badge Readiness Path](https://explore.skillbuilder.aws/learn/public/learning_plan/view/1944/networking-core-knowledge-badge-readiness-path) as mentioned in this recent [blog post](https://aws.amazon.com/blogs/networking-and-content-delivery/new-aws-networking-core-digital-knowledge-badge/).
![aws-net-core](https://images.credly.com/size/680x680/images/e75f222b-7f75-4d7b-8a6a-67d68aa59d62/image.png)

The learning path was comprehensive and covered all topics from their foundations, which on the one hand meant I had to bear through yet another 'networking basics' class, but on the other, provided reassurance from the intentional structure of all the various sub-courses, that while you now may be learning about a new products you've never encountered or even heard of before, having started from the very beginning, you should now have enough background knowledge for this new information to make sense and be appropriately contextualized. I found this valuable as one of the main challenges when learning networking initially, once you manage to somewhat make sense of all the individual topics, is how to map and fit them all together. While the structure of the networking core learning path was helpful, it wasn't until I had completed all the topics that I felt like I was able to start piecing them together and comprehend the intended scope and depth of the exam.

I didn't realise when I started the learning path, but the strong focus on the exam for the last parts was a very nice surprise. The topic reviews, practice questions, video review of practice questions, flashcards, and then the final Networking Core Knowledge Badge Assessment were all very helpful. I failed the final assessment by a few points on the first attempt a few days back, and then passed on second attempt the evening before taking the exam, with a very similar score to the exam - so the badge assessment felt like a realistic gauge of preparedness.

Given the exam focus, I didn't need to venture to third party learning providers, however I did run through some of the exam question walkthroughs from [LearnCantrill](https://youtube.com/@LearnCantrill) as I had been meaning to check out some of Adrian's content for a while:
{% include youtube.html id="4k2QdUknbtU" %}
