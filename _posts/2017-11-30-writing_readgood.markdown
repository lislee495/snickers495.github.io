---
layout: post
title:      "Writing ReadGood"
date:       2017-11-30 23:27:07 +0000
permalink:  writing_readgood
---

> Of course, a book lover (nerd) would spend a few weeks coding a replica of GoodReads. 

For the book haters, GoodReads is a website that's primarily used to find, log, and save books, with some level of social interaction. A person can sign up and immediately gain access to a personal library where they can save books. They can also find friends and follow what other people are reading. For the most part, books exist independent of users -- while users can add to and delete from their library, normally they can't touch the status of the book. 

I wanted to make GoodReads (or ReadGood) because when I was learning about CRUD, this was the first thing that jumped out to me. It was a complex enough project that it employed multiple controllers and had a user class, but simple enough that I could see the way it was structured and built. But most importantly, it was a project of passion -- I loved Goodreads, even if I don't read as much as I used to. To me, this was a perfect blend of my love of literature and new passion of coding. 

I had practiced making CRUD apps enough that I knew where to begin, though it was still intimidating to start completely new. I tried to make outlines of the models and databases. I wrote out the views. But for all my planning, what really happened was that I would write lots and lots of code that seemed to be correct, test each function out in the browser, see a failure, and then try to fix it. Essentially, ol' trial and error. Lots and lots of trial and error. 

For example, when I created the tables for the models, I hadn't anticipated exactly how they would interact with one another. Somehow, I had thought that Books and Genres needed to be joined. Things weren't working properly. Looking over old code, and using the gem "tux" to peer under the hood, I realized my mistake. Instead of Books and Genres, it should have been Books and Users--users can have many books, books can have many users. This simple logic had escaped me. 

Throughout the project, making sure all of the models and databases correctly interacted with one another was the hardest part. For example, creating a book should create the author and genre, if they didn't exist. If they already existed, the book should be added to their books. Deleting a book from a user library shouldn't delete it altogether. All of these nuances had to be perfectly coded into the controller. If nothing else, the one thing I took from working on this project was how to master the flow between coding and using the gems "shotgun" and "tux" to check my code. Essentially, a mini-version of create, read, update, and delete. 

Once I had this down, it was smooth sailing. Well, not really. There was still a lot to do, and at times, I felt extremely discouraged by the amount I had to do. **Cue Twitter Bootstrap** Thankfully, Bootstrap was holding my hand every step of the way. I owe a lot to this front-end framework, which not only helped me polish the front-end part of the app, but bring everything together through the navigation bar. 

The navigation bar is where a user can navigate through the site. It holds the links to everything a person can do--look at the books/authors/genres, add to their library, delete, logout. Without it, my app would just be a series of pages loosely strung together. The user experience would horrible. Bootstrap was also helpful in arranging content in an presentable way. Instead of looking like a '96 GoDaddy blog, ReadGood looked half-way decent. And as a writer, creator, I think there's something deeply satisfying about seeing something so barebones become attractive. It just makes everything seem like it works. 

I spent a couple of days just looking through the Bootstrap documentation and thinking of ways of implementing these features. Definitely, it expanded what I thought was possible and even necessary. For example, I dreamed of (literally dreamed of) implementing a search bar (currently put onhold for time issues). I also wanted to make a Friends sidebar (also onhold). It made me go from seeing this as just a cute project to fulfill requirements to seeing it as something that I could actually build upon. 

But for now, implementing this basic features, seeing things work in harmony, I'm happy. I'm ready to submit. Even more importantly, I'm proud and hopeful there's more features to come for ReadGood. 

----- 

Here are some potential features: 
* Friends function: adding other users as friends 
* Creating shelves: and adding books to shelves. Popular shelves: currently reading, to read, and already read. 
* Fleshing out the author and genre creation controls. 
* Adding a search function
