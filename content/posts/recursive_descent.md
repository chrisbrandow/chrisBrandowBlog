---
title: "Recursive Descent Parsing - Part 1"
date: 2020-05-05T09:31:10-07:00
draft: false
---

### The problem with the introductions that I have read

As a professional programmer in good standing, it came to my attention recently that I don't fully get recursive descent parsers. That's really probably fine, and there hasn't been a time as an iOS developer that I can see in my 5 year career that would have benefitted from the knowledge.

However, I do remember a few years back when I worked on a problem involving nested dictionaries in which I realized that the recursive solution was really so much better than the imperative/iterative approach. This was really the first time that I truly grokked recursion. It was quite revelatory, and helped me see where the pattern was applicable in ways that made the solution to a certain class of problems much simpler and potentially clearer, though probably not so for folks who hadn't made the jump across recursion canyon.

With that in mind, when I heard an offhanded comment in a Slack discussion at work about how a recursive descent parser (RCP) is a handy tool for a number of problems, I recognized that as a sign that this might be the kind of practical shibboleth that I might want to take another crack at understanding properly. To start, I just wanted to begin with the simplest kind of problem in this space. While I'm not certain what the fundamentally simplest problem is, I'm fairly certain that parsing a sequence of integers and mathematical operators is pretty close to the simplest.

I first did some searching for simple examples and explanatory implementations. I'm making progress, but what finally occurred to me today, is that essentially all examples conflate the tokenization step with the parsing process, which leads to at least some extra complications in the implementations. As I understand it at the moment, these are fundamentally distinct processes. Let me explain.

If we want to be able to take integer and mathematical operators as our basis for parsing an expression like this:

1 + 23 * 32 / 4

We would first describe what "tokens" our grammar consists of. To be clear about my understanding, the tokens are atomic units of the grammar. They do not in any way depend on order or arrangement, beyond the kind of arrangement described by a simple regex.[^2]:

number - *Anything that is a valid integer number* [^1]
operator: Any of the following characters: + - / \*

Then we'd describe the "grammar", i.e. what are the valid arrangements for the primitive tokens.

expression:
* number
* expression operator expression

But this is where most examples that I've seen take a step that complicates my ability to understand the implementation. They include the tokenization step as an implementation detail in the parsing implementation. This is understandable for a functioning parser, but I'd really like to see a RDP explanation that leaves this out. What this means is that the starting input cannot be a string, but rather an array of tokens

So instead of `"1 + 23 * 32 / 4"` as the input, I'd rather see `[num, op, num, op, num, op, num]` as the input for the introductory implementation.

So, I'll stop there, and work on an implementation with that as my starting point [^3], and see how things go.

[^1]: Implementation TBD

[^2]: i.e. distinguishing a comma in a number from a comma in a sentence. *maybe!*

[^3]: Although I do actually already have the tokenizer code working at this point. :-)
