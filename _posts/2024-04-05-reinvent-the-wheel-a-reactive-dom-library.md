---
layout: post
title:  "Reinvent the wheel: a reactive DOM library"
author: alessio
categories: [ framework, library, react, solidjs, javascript, typescript, nodejs, npm, reactivity ]
image: assets/images/reinvent-the-wheel.jpg
---
<script src="https://platform.linkedin.com/in.js" type="text/javascript">lang: en_US</script>

The term "reinvent the wheel" is often used to define a waste of time, something best avoided.
However, let me say it is not really bad. It constantly helps me to be a better software developer.

<center>Reinventing the wheel is often essential to delve deeper. To simplify. To innovate.</center>

The last wheel I reinvented was a reactive library with DOM components. I've done it from scratch and without dependencies other than build and testing stuff and I've managed to release it on [npmjs.com](https://www.npmjs.com/package/doom-reactive-state).

Please <script type="IN/Share" alt="share" data-url="{{site.url}}{{page.url}}"></script> **this article on LinkedIn and tag me** if you want to start a public conversation on this topic or [**contact me**](/contact) if you prefer to talk about it privately.

## A reactive library from scratch
These days I have resumed a project that I started last year. The project is to create a library like React or SolidJS that allows you to create reactive web applications.

I was never convinced that in React the entire component is re-rendered on every state change. Not even that when I declare an `effect` I have to indicate all dependencies in a second parameter. I thought that there could be a simpler approach.

So by experimenting and trying different things I found myself going in a very similar direction to SolidJS. I only later discovered the existence of some very useful articles to understand the reactivity concept in general. ([introduction-to-fne-grained-reactivity](https://dev.to/ryansolid/a-hands-on-introduction-to-fine-grained-reactivity-3ndf), [building-reactive-library-fronm-scratch](https://dev.to/ryansolid/building-a-reactive-library-from-scratch-1i0p))

I used the GitHub repository that I already had from last year, but I decided to start by deleting everything. I started from 0. There is even a commit "Cleanup the project. Restart from scratch".

I must admit, I copied some things from the past years commits. More out of laziness than anything else. For example the `h` function that creates any HTML DOM element.

However, I permanently eliminated some other things. I thought they increased the scope of the experiment too much and I thought I internalized the meaning behind that concept more or less. For example, how to compile TSX with custom functions. I skipped it.

This cleanup allowed me to start off with less weight, the baggage was lighter, and I was able to simplify a lot of things.

Precisely because it was a continuous exploration for me I did almost everything in TDD, it helped me so much to keep a direction and check if what I was adding/improving really behaved as I expected. It was the essential tool that allowed me to verify and understand for sure how JavaScript or the DOM elements behave in certain situations.

For the reactivity part, I decided to take a more [sociable approach to unit testing](https://martinfowler.com/bliki/UnitTest.html#SolitaryOrSociable). This is because I wanted to have the freedom to refactor and move responsibilities to different functions and classes without breaking tests. Of course these tests can break for multiple reasons and there are multiple components involved, however, this way I made my tests very resilient to internal implementation changes. Great for my exploratory use case.

For the DOM management part, which I took as is from what I had done the previous year, I kept the tests I had done at the time. They are more integration tests. In fact, the `h` function that deals with generating a responsive `DOMElement` (such as a `DIV`) goes to interact directly with the browser DOM. There is no virtual DOM. In the tests I used a [library that simulates a real DOM](https://github.com/jsdom/jsdom) which does not require opening a real browser. This way the tests are much faster.

Last year I slightly modified an algorithm retrived from [dom-expressions](https://github.com/ryansolid/dom-expressions) to make it fit into my library. I had to do a lot of work to cover it with tests in order to modify it. It was about the reconciliation of arrays of dom elements to update only the nodes that had really changed. So you'll forgive me if I didn't have the hussle to do it from scratch once again.

I also rediscovered how to publish to [www.npmjs.com](https://www.npmjs.com/package/doom-reactive-state), how to package a Typescript library with Vite, how to handle the different methods of resolving modules (cjs, esm, iife), how to expose the Typescript types to those are using the library.

I also relearned many things about Javascript (which I had studied by now some years ago by reading [You don't know JS](https://github.com/getify/You-Dont-Know-JS/tree/1st-ed)). To better handle reactivity and automatic dependency discovery, I had to refresh my memory and consciously use some Javascript paradigms that are little known or not consciously considered by many self-defined javascript developers like the `this` keyword, closures and scoping to name a few.

## Conclusions
Insomma, sicuramente ci sono ancora tantissime cose da migliorare, ma sono molto contento di quello che sono riuscito a scoprire durante questo progettino.

Ah! se guardando il repository  avete suggerimenti o spunti su come migliorare qualcosa, scrivetemi pure 🙏🏽 così possiamo confrontarci e magari imparo qualcos’altro!

Ps: Ho lasciato fuori molte cose:
- inserimento/eliminazione dal dom di un elemento in modo condizionale
- i signal derivati potrebbero essere migliorati ancora
- e tante altre cose a cui sicuramente non ho ancora pensato

Please let me know your opinion <br /><script type="IN/Share" alt="share" data-url="{{site.url}}{{page.url}}"></script> this article on LinkedIn and tag me if you find it interesting.