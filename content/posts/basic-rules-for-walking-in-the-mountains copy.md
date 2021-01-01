---
title: Benefits and trade-off of a Serverless strategy
date: 2019-11-04T00:00:00Z
thumb_img_path: images/1.jpg
content_img_path: images/1.jpg
excerpt: Looking at the landscape of cloud transformations, three main strategies
  stand out
template: post
subtitle: An exec summary of the cloud-native Serverless strategy

---
Digital is an amazing leveller that allows small dedicated teams to achieve outcomes that would have been considered impossible two decades before. When Instagram was acquired by Facebook for $1 billion it had achieved a reach of 30 millions users with a team of only 13. In digital it's not the big that eat the small, it's the fast that eat the slow.

One requirement to achieve the speeds required to compete on the IT side is using the latest cloud innovations. In the series we will see the three main cloud strategies that make sense today, by order of decreasing achievable speed.

Digital is an amazing leveller that allows small dedicated teams to achieve outcomes that would have been considered impossible two decades before. When Instagram was acquired by Facebook for $1 billion it had achieved a reach of 30 millions users with a team of only 13. In digital it's not the big that eat the small, it's the fast that eat the slow.

One requirement to achieve the speeds required to compete on the IT side is using the latest cloud innovations. In the series we will see the three main cloud strategies that make sense today, by order of decreasing achievable speed.

## Serverless in a nutshell?

Serverless describes a cloud architecture where the infrastructure and operating system have been abstracted away. Instead of dealing with how to install and configure your app in a linux environment, it becomes about combining ready-made services provided by the cloud vendor. Developers can integrate these services using APIs and write small custom functions to glue them together. The small custom functions are run by a service called "AWS Lambda", "Azure Functions" or "Google Cloud Functions" that abstracts away the underlying operating system.

As an simple example, take the boring task of dealing with users uploading their profile pictures in various sizes, which then need to be normalised to be displayed in your application. With a Serverless architecture, you can leverage the AWS S3 service to deal with the upload and scalable storage of the pictures, removing the need to write any code dealing with that. You can then configure a "trigger" on AWS S3, that will, everytime S3 receives a new photo, run an AWS Lambda containing the few lines of code dealing with the resizing. And that's it you're done! Which means you have written a few dozen lines of code rather than a few hundreds for a much more scalable and robust outcome.

> _Serverless technology is up 22% between December 2017 and August 2018 with 70% of respondents using AWS Lambda_ - CNCF 2018 Survey

## **For whom?**

It's for new applications or services that are built cloud-first and do not mind the constraint of being wedded to a specific cloud provider.

## **Main benefits?**

### **Benefit #1: write a _lot_ less code.**

A great Steve Jobs quote to illustrate the value of this:

> _"The way you get programmer productivity is not by increasing the lines of code per programmer per day. That doesn’t work. The way you get programmer productivity is by eliminating lines of code you have to write. The line of code that’s the fastest to write, that never breaks, that doesn’t need maintenance, is the line you never had to write"_ - Steve Jobs, 1997

Leveraging as many as possible of AWS’s new “serverless” services allows to abstract complex pieces of architecture and focus on the business-specific logic. Resulting in apps containing sometimes 10x less lines of code than before.

> _"I did a Twitter poll recently asking how many times people have rewritten basic user registration functions. And from that poll I extrapolate that the basic user registration function has been written at least a million times. \[...\] A lot of what we do in IT, I’m sorry to say, is waste."_ - Simon Wardley

Some examples of the many game-changing abstractions currently provided by AWS serverless services:

* Lambda to run functions without any concern for the underlying operating system
* API gateway for routing a URL to your service (or in other words: publishing, routing, monitoring and securing API endpoints)
* Cognito for a ready-made authentication
* Step functions to design and run workflows that stitch together different services. Your workflow becomes a state machine diagram that is easy to understand and monitor.
* SQS is a messaging service, the core component of an event-driven architecture. It's the Amazon equivalent of RabbitMQ.
* DynamoDB, a fully-managed NoSQL database. It's the Amazon equivalent of Cassandra.
* Amplify, a JS framework to help create frontends connected to a serverless backend, with ready-made components for React and React-Native. The Amazon equivalent of Bootstrap and Google Firebase
* and many others

### **Benefit #2: scaling up infinitely out of the box**

The simplicity of scaling up a serverless app is based on two complementary aspects. The technical aspect: the goal of the serverless products offered by the cloud vendors is to abstract all the infrastructure challenges of “adding CPUs” if more users are using your app. But this would not work easily if it weren’t for the second human aspect: serverless architecture nudges devs strongly into separating code in many simple stateless functions that can be run in separate Lambdas. And strongly recommends the usage of horizontally scalable data stores like S3, SQS and Aurora DynamoDB. This means that experienced serverless dev teams are able to write without any overhead applications that are infinitely scalable.

### **Benefit #3: scaling down - cost and energy optimisation.**

The stateless and on-demand architecture that allows for easy up-scaling should also allow to scale down to zero and shut down everything when the app is not used. This is not as straightforward as one could hope. The challenge here is the “cold-start” time : the time it takes for Serverless products like lambda or Aurora to wake up from “hibernation”. Some stacks can take hundreds of ms to wake up, which could be quite problematic in many use-cases. To avoid that, some lambdas are usually kept “warm”, just in case a user needs them now. However if you choose the right stack (NodeJS, Python, Go\]), you can have a very fast cold-start which, combined with some performance optimisation and smart UX tricks, make the boot up time completely transparent to the user. Imagine the savings in terms of energy and costs for B2B applications that are rarely if ever used at night and on week-ends!

## **Main trade-offs?**

### **Trade-off #1: Getting married to a cloud provider**

Serverless is based on the productisation of software and infrastructure components that you can leverage as services rather than build yourself. It is still a very competitive space and cloud vendors are trying to create unique services that will help you save the most coding time. Leveraging that value means using their latest innovations, which are vendor-specific. And therefore creating a tight coupling with the vendor you have chosen.

Opensource implementations of serverless on top of Kubernetes, which would provide a cloud-agnostic solution, are still very experimental and only provide the equivalent of AWS lambdas or Google Cloud functions, not the rich ecosystem of services that are leveraged when doing serverless on AWS

### **Trade-off #2: a different way to write code**

Getting the most of serverless requires to architecture code in a very different way to standard web applications. The most efficient serverless architecture is: a rich client, with one stateless lambda per api path, connected to a nosql backend, leveraging event-driven architecture wherever possible. This is incredibly scalable (up and down) but miles away from a traditional monolithic architecture and also very different from a micro service approach. This means that migrating to serverless requires rewriting. And it means that dev teams need specific training.

### **Trade-off #3: the technology is still quite new**

A consequence of both the creation of new services and a different architectural approach is that developers and architects with large scale production experience of serverless architectures are still rare. But the good news is they exist and they are super positive about their experience.

_"We used serverless at Movivo where I was CTO, and we scaled at a fraction of the cost of what is standard for such scale."_ Paul Johnston, interim CTO and serverless "guru"

### **Trade-off #4: “devops teams” will not like serverless**

Serverless experts will probably be people with strong software dev and architect backgrounds. This opinion is based on the fact that the main ops challenges are abstracted by the cloud vendor, so the key challenges are on how to architect your app. This has an impact for what is currently called “devops teams”, often ops teams up-skilled on cloud services. They will not be the right people to help on the software architecture challenges and will probably not be the ones embracing serverless, even if it’s the next step in cloud transformation.

> "_Well, as we continue to shift up the stack toward a new change lof practice with serverless, I think you’ll find that the new legacy is going to be DevOps. And that won’t be popular either." - Simon Wardley_