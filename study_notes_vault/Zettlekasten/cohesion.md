---
aliases:
tags:
date: 10-31-2025
time: 09:27
references:
  - "[[general programming concepts]]"
---
# Concept
Cohesion is the thought that code which is "similar" enough should be placed together. It's the thought of grouping functionality. What this achieves, is that if you have to make a change you ideally do it in one place, or as close to a single place as possible. For instance if I have a service that is part of a larger micro service that needs to change, I can change it in that one micro service, and rebuild and re-deploy it without having to re-deploy the entire application.

> [!WARNING]- Premature Optimization
> This is easy to optimize for too early. For instance its ok to keep two things in the same area even if they're not 100% related at first. Maybe splitting them out right now doesn't make sense because it wouldn't get enough traffic or use by itself, but splitting it out into its own "unit" would add complexity in the form of having to modify/maintain a separate section of code.