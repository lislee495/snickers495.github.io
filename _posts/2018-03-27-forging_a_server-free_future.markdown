---
layout: post
title:      "Forging a Server-free Future"
date:       2018-03-27 17:30:39 +0000
permalink:  forging_a_server-free_future
---

Most of the web as we know it relies on servers. Websites, computers, and phones all communicate with physical servers in order to receive and send information. Backend developers ensure that websites correctly communicate with servers housing the database. 

But despite our highly server-dependent world, more and more people are switching to serverless technology to house their database. Why, and how? 

## What are serverless tech's advantages? 

In general, the traditional, three-tiered servers are expensive to setup and manage. From the developer's POV, even making simple changes to an app could turn into a grueling process ensuring that the changes work on every level.

With serverless tech, it's quick to scale and delivers high performance. Additionally, companies only have to pay for the resources that are used. This means it's good for apps that have fluctuating users. Serverless frameworks also ensure a direct correlation  between the efficiency of the code and the amount that clients have to pay. More efficient code = less resources needed. Thus, developers simply have to focus on streamlining their code, rather than managing and maintaining the servers. 

## Who offers it? 

Serverless tech exploded in recent years due to Amazon Web Services offering it in their AWS Lambda, as well as Microsoft Azure's Function. Since then, IBM and Google have also begun offering serverless frameworks, like OpenWhisk and Cloud Platform, respectively. 

## How can it be done? 

Serverless tech promises that developers don't have to worry about big surges in traffic. That's because the system will automatically handle load-balancing and traffic provisioning. Additionally, this system is managed for the clientele, who don't have to waste time or resources to provision servers or administer software. 

Another thing to note about serverless tech is that it associates Functions as a Service (referred to as FaaS). This allows developers to develop code in response to events without the complexity of building and maintaining an infrastructure.  

To start, we can use a simple but popular package like [serverless](https://github.com/serverless/serverless) to get our serverless framework  running.

First, install via npm: 

`npm install -g serverless`

Then, set up your provider credentials for the host you're using. This is usually an access key of some sort. Further instructions are available [here](https://github.com/serverless/serverless/blob/master/docs/providers/aws/guide/credentials.md).

Create a service or deploy existing services.

`
// Create a new Serverless Service/Project
serverless create --template aws-nodejs --path my-service
// Change into the newly created directory
cd my-service`

Then deploy using: 

`serverless deploy -v`

With serverless, you have a variety of options for deploying or removing specific Functions.

You can use this to deploy the Function, here named 'hello': 

`serverless deploy function -f hello`

Or invoke the Function: 

`serverless invoke -f hello -l`

Or fetch the specific logs for the Function:

`serverless logs -f hello -t`

To remove all the Functions, Events, etc. from your account, simply use: 

`serverless remove`

To install a service and go, serverless also makes that easy by offering dozens of links to compatible services. Some of these include [ES6, Babel, and Jest](https://github.com/americansystems/serverless-es6-jest), [Facebook Messenger ChatBot](https://github.com/pmuens/serverless-facebook-messenger-bot), or [authentication boilerplate](https://github.com/laardee/serverless-authentication-boilerplate).

All you need to do is get its github url and type into the console: 
`serverless install --url <service-github-url>`


## What are its drawbacks?

Now that we know how to implement serverless tech, what are some of its drawbacks? 

### Third-party API systems

Since you're relying on third-party API systems, there can be risks related to vendor lockdown, control, forced API upgrades, and [security issues.](https://www.whitesourcesoftware.com/whitesource-blog/serverless-security/?utm_campaign=wss&utm_content=serverless-security-application&utm_medium=social&utm_source=quora&utm_term=serverless-security). And since you're forced to build to the systems of one vendor, it becomes difficult to migrate your software to any other vendrs. 

### Loss of control in debugging

Developers usually depend on vendors for debugging and monitoring tools. Learning the Debugging Distributed Systems can be challenging and getting to the root cause entails going through layers of complexity. 

### FaaS itself

The reliance on Function as a Service means that often times, an app is fragmented into hundreds or possibly thousands of discrete functions. While they work for short, simple transformations of data to and from persistant storage, when there are more of them, it becomes a greater challenge to organize and decipher the interactions between them. 

### Stateless operations 

Everything operates statelessly, so developers have to do more overhead work to pass variables that require multiple transformations -- like storing each variable in a DB and chaining them like that. 






