---
layout: post
title:  "Go's standard heap interface has poor function naming choices"
date:   2016-07-24 01:00:00 -0700
categories: golang programming
---

package `container/heap` aims to provide a somewhat generic heap implementation for any type as long as there is a total order
defined. However, the naming choices of functions defined in `heap.Interface` are really poor. `Pop` and `Push` collides with
`heap.Pop` and `heap.Push`. To correctly do heap push/pop, users have to define those two interface functions, which should only be
utilized by `heap`'s internal implementation, and always remember to call `heap.Push(myHeapVar, object)` rather than `myHeapVar.Push(object)`.
 In my opinion,  `myHeapVar.Push(object)` looks more natural as heap operation, especially if they are part of `heap.Interface`.
Worse, as I have to define exported `Pop` and `Push` functions with my heap type, I have no way to control they are only used
by `heap.Push` and `heap.Pop`, they can be used everywhere, I can forsee confusions/bugs be introduced.

I believe `PopBack` and `PushBack` are more proper names:

* `heap.Interface`'s `Pop` and `Push` moves the object around the end of a list-based heap as `PopBack` and `PushBack` fits very well.
   Also,  they are not strage names. we have been using `pushback` and `popback` in C++ std template library for years.
* We now don't have to deal with name collision, and it is highly unlikely we would use `PopBack` to pop the least element from the heap.
