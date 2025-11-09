---
aliases:
tags:
  - coupling
date: 10-31-2025
time: 09:33
references:
  - "[[general programming concepts]]"
---
# Concept
The ***concept of things relying or depending on each other being "coupled" together***.

In terms of "***domain coupling***" this is ok, and in fact unavoidable. For instance, you would couple a "**Driver**" and a "**Payment**" service(s) under a "**Trip**" service because both would need to exist for a **Trip** to be possible. You would need a **Driver** to drive the trip, and a **Payment** processor to process the payment for the trip.

Where coupling is detrimental is "***content coupling***". For example Trip, and Driver using the same database, or "being dependent" (coupled) on the same DB. Instead both should have their own database so as not to step on each other or interact with the same areas as much.

Another good example of poor **component based coupling** is in the **hexagonal architecture** having your **core business logic** depend on a third party library directly. The **core "business logic"** and the library are so tightly coupled that if the library maintainer were to say go in a direction you didn't approve of, the uplift to swap out that library would force you to modify the core logic. Instead an **adapter** and **port** should be in place allowing you to swap out the underlying third party library for another library serving a similar function without changing the **core business logic**.