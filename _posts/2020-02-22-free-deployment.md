---
layout: post
title: Free Side-Project Deployment
---
A while ago I came upon [this](https://alexolivier.me/posts/deploy-container-stateless-cheap-google-cloud-run-serverless) 
great blog post by Alex Olivier that introduced Google Cloud Run, where you can deploy your webservers for next to nothing.
This was perfect timing as I’m currently working on a side project of my own, and had come to the point where I needed to deploy 
the first version of it.

The project consists of 4 different parts:

- React client
- NodeJS server
- MongoDB database
- Neo4j database

I had expected that it would cost about $100/month to host all of these, but reading Alex’s blog post encouraged me to find ways to optimize my costs. Here’s what I found:

### React client
My friend William recommended that I check out [Netlify](https://www.netlify.com/) for deploying the React client. 
I was positively surprised. First, it’s free for simple projects and you get up to 300 build minutes. 
Second, it’s really easy to set up as you just link it to your Github repo and point to the relevant folder. 
Third, it builds and deploys automatically when you push to Github.

### NodeJS server
For this I used [Google Cloud Run](https://cloud.google.com/run), as explained in Alex’s blog post. Technically it's not free, but
since Google is handing out US$300 in GCP credits, it pretty much is.


### MongoDB
This is where I thought that I’d have to pay a lot, even during development.
Turns out that this is not the case. [MongoDB](https://cloud.mongodb.com/) has its own fully managed databases across AWS, Azure, or GCP, 
with a free tier of 512MB of storage. This is plenty for me now in the development phase of the project.

### Neo4j
Since Neo4j is more niche than MongoDB I didn’t expect to find something for free here.
Neo4j has [Neo4j Aura](https://neo4j.com/aura/), but that has a minimum cost of $64/month. After some searching, I found [GrapheneDB](https://www.graphenedb.com/).
GrapheneDB provides managed Neo4j and has a hobby tier which is free for up to 1k nodes and 10k relationships.
This won’t take me too far, but at least I can use it while developing. If I’m content with what they are providing, 
I might switch to their development tier which gives you up to 100k nodes and 1M relationships for $9/month. Pretty good deal.


There it is, a short post on my deployment setup during the development phase. I hope you found it useful, and don’t hesitate to reach out if you have any questions about it.
