---
ID: 575
post_title: Comparing Excerpt Creation to Localhost
author: Pierre Crutchfield
post_excerpt: ""
layout: post
permalink: >
  http://devdevblogs.wpengine.com/blog/comparing-excerpt-creation-to-localhost
published: true
post_date: 2018-07-17 18:09:38
---
So, you’ve heard that VB (and C#) are open source now and you want to dive in and contribute. If you haven’t spent your life building compilers, you probably don’t know where to start. No worries, I’ll walk you through it. This post is the first of a series of blog posts focused on the Roslyn codebase. They’re intended as a primer for prototyping language features proposed on [the VB Language Design repo][1]; and contributing compiler and IDE features, and bug fixes on [the Roslyn repo][2], both on GitHub. Despite the topic, these posts are written from the perspective of someone who’s never taken a course in compilers (I haven’t).

# Phases of compilation

At a high level, here’s what happens:

1.  Scanning (also called lexing)
2.  Parsing
3.  Semantic Analysis (also called Binding)
4.  Lowering
5.  Emit

Some phases overlap and infringe on others a bit but that’s basically what the compiler is doing.

# Compiling is a lot like reading

By analogy, when you read this blog post you look at a series of characters. You decide that some runs of letters form words, some is punctuation, some is whitespace. That’s what the scanner does. Then you decide that some punctuation groups things into a parenthetical, or a quotation, or terminates a sentence. Some dots are decimal points in numbers or abbreviations or initialisms. That’s what the parser does. Then you import your massive vocabulary of what words mean and look at all the words and decide what those words refer to and in combination what the sentences mean. Occasionally, you find a word with multiple meanings (overloaded terms) and you look at some amount of context to decide which of the multiple meanings is intended (like overload resolution). All of that assignment of meaning is semantic analysis. Lowering and emit don’t really have natural language equivalents other than perhaps translating from one language to another (think of it like translating an article from modern English to simplified English to another very primitive language).

 [1]: https://github.com/dotnet/vblang
 [2]: https://github.com/dotnet/roslyn