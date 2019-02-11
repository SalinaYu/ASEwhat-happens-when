# What Happens When...

![browser_bar](./ref/ref1.png)

## Introduction

Today's exercise is an attempt to answer the age old interview question "What happens when you type a URL in your browser's address box and hit _enter_?".

The point of this question in an interview is to test how the candidate can articulate and link the various layers of the HTTP request/response process across domains of IT knowledge. For today's exercise, we will narrow that down a bit to focus on the parts of the stack that will be applicable to ASEs.

I will attempt to demonstrate each step that discuss (within reason) using [wireshark](https://www.wireshark.org/download.html), command line tools, and browser tools/developer mode. Content in this repository was borrowed generously from [this repo](https://github.com/alex/what-happens-when).

```Presentation Notes: 
Start Wireshark capture at this time
Use capture filter: not net 104.219.104.0/24
```

## Starting Point

Some answers to this question will go into excrutiating detail about physical key presses, OS interupts, etc. 

```
...the Enter key bottoms out on the keyboard... 
...an electrical circuit is closed (either directly or capacitively)...
...current flows into the logic circuitry of the keyboard...
```

We're not concerned about physical input process for this session. Suffice to say that the input (_www.google.com_) was populated in the browser bar. The _Enter_ key has been pressed.

## OSI model callback

As we walk through this we'll try to keep context through each step.

![OSI model simple](https://i.vimeocdn.com/video/546484970.webp?mw=1100&mh=619&q=70)

* What are we doing in this step?
* What happened leading up to this step?
* What layer(s) of the OSI model does the current activity related to?

[Start: Parsing the URL](./1-ParsingURL.md)

