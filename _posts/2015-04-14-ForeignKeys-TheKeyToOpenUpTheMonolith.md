---
layout: post
title: Foreign keys - the key to open up the monolith
---
I had a discussion yesterday with a developer that just created a service to expose a part of the big monolith. He had separated out a small business domain, created an API and was now advocating people around him to use it. 

Having a first look at the service I was surprised to find the data tables still in the same big monolith relational database. Asking if he had any thoughts on breaking out his new domain into its own separate database or maybe just its own schema, he replied

>I can't, because it is connected everywhere with foreign keys. 

Here I realised a problem. To get the full picture, and in fear of loosing important parts of a product, we naturally want to bind things together. The order has a customer and to ensure that the customer on the order exists we enforce a hard coupling, the foreign key. This is the way we learnt to model a database for decades, it is the "best practice".

But does the model really need these restriction? What's the risk of removing the foreign key? For the price of possible inconsistent data we gain a more decoupled system that has a built in software seam. A seam that means we can move the relationship away from the database, and get full control over where, how and which part we later choose to sew together.

Just like how agile tells us to embrace uncertainty, and living with eventually consistency helps us achieve high availability in distributed computing, maybe we should just accept that incorrect data can exist, and try to handle it, instead of putting all our effort in fighting against it. 

To split the monolith we must remove the foreign key database constrain.
