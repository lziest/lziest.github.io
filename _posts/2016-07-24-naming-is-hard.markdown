---
layout: post
title:  "Naming is modeling. Modeling is hard, so is naming"
date:   2016-07-24 00:00:00 -0700
categories: golang programming
---

> There are only two hard things in Computer Science: cache invalidation and naming things.
> -- Phil Karlton

I believe this is a quite famous quote. And it resonates quite well with people in engineering.
If I am saying it today, I would say they are hard things in Software Engineering, rather than
Computer Science. Especially, naming is pretty hard in engineering code. Or I would rather argue modeling is hard.

## Lost in Translation
No matter what programming language we are using, coding is a process of tranlating our modeling of
real-world logic into program. Human language is contextual. But the context changes from where
the name is created to where the name is actually referenced.

## We usually have only one shot to get naming right.
Once we define a public API name, it will be used by client code. Once we define our software pacakge name, it will
be referenced/recorded in some configuration files. Renaming an API means breaking compatibility of existing client.
Renaming a package name running in production? You need to rewrite part of the deployment code and the upgrade/rollback
process is so messy. So, in order not to break clients, not to break our stable running service, distrupting
our entire infrastructure, let's just keep the bad name and instead provide a lot of documentations and warnings.
But there are two sad facts about software engineering: 1. devs rarely read the documentation of an API, they simply
copy/paste from existing code, and use the name and existing usage as the documentation itself. 2. devs have spent
large amount of their time getting their code understood by computers, they rarely write
good documentations from users context/perspective. 

## Models evolve over time but names can't
A vague name is meaningless. However, if a name is perfect clear and concise right now, it is hardly future-proof.
Our code changes, names would stay.
