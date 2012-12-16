---
layout: blogpost
title: "Javaism, Exceptions, and Logging: Part 3"
published: false
description: "Javaism, Exceptions and Logging: Lessons from refactoring large codebases. Part 3 of 3"
---

<img src="http://tomerfiliba.com/static/res/2012-09-18-Callahans.jpg" class="blog_post_image" title="Over-logging"/>

> * [Part 1](http://tomerfiliba.com/blog/Javaism)
> * [Part 2](http://tomerfiliba.com/blog/On-Exceptions)

In the third part of the series, I want to address *logging*, especially when it intersects with
exceptions and exception handling.


, logging and
exceptions, and style.

## Logging ##


* What to log
* Where to log
* Avoid excessive logging
* Use exceptions
* include add info in exception itself, rather than log
* Oreror




## Style != Beauty ##

Lastly, I wanted to point out that **coding style is not just about looks**. Many people think that
style is a matter of individual preference; it might be true, but it usually reflects

if x in somedict.keys()
if kwargs.keys()[0] == 'foo'

try:
    x
except:
    raise

self.MUST_BE_SINGLE_PATH is True

divmod(offset, 512)[0]

---------------------------------------------------------------------------------------------------

## A Rant On Python's ``logging`` ##

In the first installment, I argued that Python's ``logging`` module suffers from extensive
Javaisms, which sparked a long discussion in the comments. Vinay Sajip argued that albeit
``logging`` "borrows" from [log4j](http://en.wikipedia.org/wiki/Log4j), it makes *easy tasks simple
and hard tasks possible*. But let's face it - how hard can *logging* ever get? At the most
sophisticated
is opening a file and appending lines to it! It's far from rocket science, so the most important
part is its software engineering.

Back in the day, a friend of mine coined the derogatory term **oreror**, to refer to "any
programming-related concept that ends with -er or -or", such as ``Adapter`` or ``Delegator``.
He wasn't referring to Java in particular, but to over-engineering in general and the introduction
of way too many abstraction layers: you begin with an ``Adapter`` and end with an ``Adapterer``, 
hence the name *oreror*. Note that there's **nothing inherently wrong** with such layers, but it 
usually suggests you're over-complicating the design, trying to be too generic.

Java lends itself to a great deal of such orerors, because of the way its OOP system works: it
requires adapters everywhere, and basically encourages you to "design for the worst case" from the
first step. While this might be good, it's more likely to just make simple cases complicated.
Now pop up a Python interpreter, import ``logging`` and type ``help(logging)``. This is what you'll
see in the first few lines:

    CLASSES
        __builtin__.object
            BufferingFormatter
            Filter
            Formatter
            LogRecord
            LoggerAdapter
        Filterer(__builtin__.object)
            Handler
                NullHandler
                StreamHandler
                    FileHandler
            Logger

They even have ``Filterer`` - it doesn't get any more *oreror* than that! I began working on a
minimalistic, proof-of-concept Pythonic logging framework. I'll keep you posted.