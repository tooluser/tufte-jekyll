---
layout: post
title: "Lab coats and toy problems"
date: 2015-04-27 12:21:23 -0700
comments: true
categories: hiring
---
{% newthought 'Someone clever once said' %} that modern analytical philosophers would wear lab coats to work if they thought they could get away with it. I think something similar can be said about software engineers.<!--more--> So many of our hiring practices revolve around toy problems and algorithmic complexity — the things we’re all impressed by from our experience getting degrees (or from not getting a degree). But we’re putting on airs when we do that. What we do in our careers is much more of a skilled trade than mathematically complex or scientifically rigorous; it's much more akin to skilled carpentry than it is to structural engineering.

For example, real algorithm *design* is really a small part of the work we do. I mean this in the strong sense. Yes, we design algorithms, and yes, you can’t be an idiot about algorithmic complexity. What I mean is by 'strong sense' is developing novel structures and extending the art and science. They happen, but they happen via weeks of research and experimentation into existing algorithms, not in an hour at a whiteboard. Otherwise, we need to do a complexity analysis of a process infrequently. 

On the other hand, every day, I design code that has to be non-astonishing and integrate with large architectures, be flexible but realistic in its goals, and be modifiable in the long term by myself and others. Mostly, implementing code is about modeling a problem well and selecting good common patterns. This is the opposite of what a good CS degree teaches and what a 'toy problem' interview problem examines. 

You don’t evaluate the real day-to-day skills of our profession with toy problems. Yes, an excellent engineer will usually make a good showing of any toy problem — but plenty of very good engineers won’t, on that particular problem. But worse, plenty of people who will do well on toy problems will then utterly fall apart in the long term problem of building systems their other engineers can interact with. I think toy problems make us feel scientific, but are a very bad way to actually judge candidates. 

Better I think is real code review. Show a project you have built, and walk a panel though it. Encourage conversations about trade-offs; make it a non-confrontational (another huge problem w/ toy problem style questions — they’re exams. I say this as the kid who loved exams. They are bad for this goals; they don't mimic how we will want to work for real) and conversational. Use it as an opportunity to dig deeper as appropriate to the target skill level (“When would you not use a protocol? What about delegation instead of blocks here? You used a mutable array; have you used the new mutable ordered sets? etc.”).

People are more comfortable when they’re explaining something they know solid — and you can see their skill better. (The argument that you ‘want to shake people off their feet’ and ’see how they think outside the box’ is both sadistic and unilluminating; our work is rarely shaking, or discomforting, nor does it usually benefit from stress. The rare stress situations are usually failures of systems we built and know, rather than random exam questions.) 

I analogize here from somewhere that hiring is similarly very expensive: the academic world. Interviews are not run as exams; you read the work people have done and let them talk about it, asking them questions. They know there very well that exams are brittle.

I think toy problems are useful if you have a huge pool of incoming engineers and you really want only CS degree types -- when you could actually benefit from the solo genius generating cleverness in a silo. There's a place for that. Google, certainly, can benefit from it. They also have a massive scoring database for reviewers AND candidates, so they can do some amazing math and both calibrate and improve their process with it. Most companies are too small and do too few hires for numerical analysis to overcome statistical noise.

What sort of project should be used? A number of people suggest take-home work. Implementing take-home problems is perhaps acceptable for very junior people — but no one advanced will have the time, and projects of scale aren’t comparable to toy projects, due to their infrastructure, testing, etc. Complexity emerges in real systems, not in take-home problems. Better is a real project that has had to engage with messy reality. 

Such project walkthroughs need not reveal trade secrets etc. No code needs to leave the candidate’s laptop, either. A whiteboard and a projector screen will suffice. The candidate can choose what to demo, and if reasonable flexibility is given 