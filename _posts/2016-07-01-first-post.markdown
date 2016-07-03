---
layout: post
title:  "To vendor or not to vendor, that is a question."
date:   2016-07-02 20:00:00 -0700
categories: golang programming
---

I have discovered that golang's vendoring could cause
serious confusion. I have made a example [here](https://github.com/lziest/splitbrain).

As a solution, my colleague has
suggested that go library package should not employ vendoring and only go
main package should. However, I still wonder how I can now write a new
library with dependency of other 3rd libraries. It would be a big
pain for any developer trying to resolve dependency compatibility
at the very end.

Scenario: An popular package `httpframework` has been completely
rewritten. Its v1 and v2 APIs are not compatible.
Since `httpframework` is very popular, many lib packages utilize
that package at different time. Since lib devs should not care
about compatibility. Some libsa metrics use v1
and others use v2.

Suppose Alice wants to write a simple http server using a popular metrics
server package and a popular Restful framework. But since
the two dependencies uses different versions of `httpframework`,
Alice is essentially unable to write the program. The dependencies
have failed to encapsulate their own dependencies.

Now people may ask, "isn't vendoring suppose to solve that problem?"
But here is another problem. Many Go's libaries have exported package
variables. Those variables can be viewed as certain global states
of a certain package.
Prior vendoring era, we can `go get` each imported package once
and the global state of each imported package can be shared within
all other imported packages. Some devs may take it as granted and
simply manipulate those global states at will. However, with vendoring
each imported package may have its own view of global states.
Now a dev may found it impossible to change other package's view of
global state.
The [splitbrain](https://github.com/lziest/splitbrain) example I listed
above illustrates this problem really well.

So to vendor or not to vendor, that is a question.

