---
title: "Human-Centered Spaced Repetition"
description: "A friendlier approach to efficiently studying flashcards."
pubDate: "Aug 23, 2024"
heroImage: "/posts/spaced-repetition-advisor.jpg"
---

When they

### What is Spaced Repetition?

<a href="https://en.wikipedia.org/wiki/Spaced_repetition" target="_blank">Spaced repetition</a> is a
rote-memorization strategy based on psychologist Hermann Ebbinghaus's **forgetting curve**, which
posits that re-learning information after forgetting it reduces
the time it takes to forget and strengthens long-term memory. If you have a test coming up in a month, it's more efficient and effective to study at a few spaced intervals over the entire month than to cram into a single intense study session, even if the time spent studying is identical.

<img src="/posts/forgetting_curve.png" alt="Ebbinghaus's forgetting curve" width="60%">

Many studies have scientifically proved that spaced repetition is an extremely effective technique (see <a href="https://pcl.sitehost.iu.edu/rgoldsto/courses/dunloskyimprovinglearning.pdf" target="_blank">this paper</a> by Dunlosky et. al -- one of my favorite educational psychology papers in general). When massive amounts of information (in situations like language learning or medical school) need to be learned, spaced repetition is a reliable strategy to memorize everything without having to study day-in day-out.

#### Anki

With the efficacy of spaced repetition being so high, it's only natural that programmers would make flashcard apps that employ spaced repetition. The most popular of these is <a href="https://apps.ankiweb.net/" target="_blank">Anki</a>, a free software which utilizes extremely optimized algorithms for determining when cards should be studied.

While I often find myself needing to learn large amounts of rote information (mostly from classes and language learning), I don't use Anki. I find it too difficult to use, with the user interface not being very intuitive and too many settings to configure. There are plenty of guides on how to properly configure and use Anki, but my goal is to study flashcards, not to learn how to use an app. However, even if Anki were easier to use, I still wouldn't find that it fits my lifestyle.

### Why I Don't Like Spaced Repetition

While spaced repetition seems effective, I never have found it appealing for
several reasons:

#### It takes away control

This kind of rigidity discourages breaks...

To make matters worse, studying a ton on one day forces you to keep up a consistently high level of motivation on subsequent days.

_But shouldn't people be encouraged to study every day?_
While this may be theoretically true -- building good, daily study habits can be very useful -- I find that taking periodical breaks is far more helpful for long-term learning and mental health. I would much rather give up a little bit of efficiency than burn out and feel miserable for a week, which might completely throw the efficiency out the window anyway.

Even if you never needed to take a day off, what if you just have a busy day? Or what if there's an emergency? Studying flashcards shouldn't be a full-time job that you're on-call for. The hard part should be the studying itself, not the process.

#### It requires too many decisions

Most spaced repetition algorithms (like the popular <a href="https://github.com/open-spaced-repetition/fsrs4anki/wiki/ABC-of-FSRS" target=_blank>FSRS</a> algorithm
used by Anki), require users to manually input their confidence level after
reviewing each card (for example, easy, medium, or hard). While this improves the algorithm's ability to accurately schedule cards, it forces
users to constantly stop and think, instead of focusing only on recalling
information for the flashcards.

Furthermore, user interpretation of the difficulty levels can greatly vary.
Even the judgement of a single user can vary over time (I don't remember
what an "easy" card felt like a week ago).

### A Potential Solution

The underlying principle of spaced repetition -- that
studying at spaced intervals is effective for long-term memory -- is
still extremely valuable. How then, can that principle be incorporated into
a more human-centered design that takes into account the aforementioned
pitfalls?

A potential solution I've created is a **spaced repetition advisor**. Instead of forcing you to study certain cards at certain times, the advisor determines an order in which the cards should be studied.

For example, let's say I have 1000 cards to study. On day 1, I study 50 cards. Then, on a future day, the spaced repetition advisor strikes a balance between reviewing and introducing new cards. This depends on how long the 50.

Additionally, since the precision of times when cards should be reviewed less important than in traditional spaced repetition (by design, users are free to choose when they study), a less optimized scheduling algorithm can be used. While this initially may seem counterintuitive, users can more easily understand a simpler algorithm. This way, users can tune the algorithm according to their preferences -- for example, do they want to focus more on learning new cards or reviewing others -- whereas with a more complex algorithm, tuning may not be possible (at least in a way that doesn't induce headaches).

### Conclusion

Traditional spaced repetition isn't bad -- it just isn't right for everyone in
every situation. Like most things in life, having multiple options
to choose from is best, and I hope the idea of a spaced repetition advisor
can spur a discussion on human-centered flashcard review systems and
algorithms.

If you'd like to try out using a spaced repetition advisor, I created a
<a href="https://github.com/joshuamotoaki/gen-cards" target="_blank">prototype application</a> for personal use. It's completely free and runs locally on your computer. Eventually, I plan on streamlining this application to make it much
more suitable for general use.
