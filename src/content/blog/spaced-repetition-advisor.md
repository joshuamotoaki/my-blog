---
title: "Human-Centered Spaced Repetition"
description: "A new approach to spaced repetition that I use to learn in a friendlier way."
pubDate: "Aug 23, 2024"
heroImage: "/posts/spaced-repetition-advisor.jpg"
---

When they

### What is Spaced Repetition?

Spaced repetition is based on Hermann Ebbinghaus's **forgetting curve**, which
demonstrates that if you re-learn information after you've forgotten it a bit,
the time it takes to forget decreases every time.

<img src="/posts/forgetting_curve.png" alt="Ebbinghaus's forgetting curve" width="60%">

This implies that the most efficient way to gain long-term memory of information
is to study in spaced intervals.

### My Problems with Spaced Repetition

While spaced repetition seems effective, I never have found it appealing for
several reasons:

#### It locks you into a rigid schedule

This kind of rigigity discourages breaks, which have been shown to be
neccesary to prevent burnout and increase study efficiency.

Studying a ton on one day forces you to keep up a consistently high
level of motivation on subsequent days.

#### It requires manual difficulty decisions

Most spaced repetition algorithms (like the popular <a href="https://github.com/open-spaced-repetition/fsrs4anki/wiki/ABC-of-FSRS" target=_blank>FSRS</a> algorithm
used by Anki), require users to manually input their confidence level after
reviewing each card (for example, easy, medium, or hard). While this improves the algorithm's ability to accuractely schedule cards, it forces
users to constantly stop and think, instead of focusing only on recalling
information for the flashcards.

Furthermore, user interpretation of the difficulty levels can greatly vary.
Even the judgements of a single user can vary over time (I don't remember
what an "easy" card felt like a week ago).

### The Spaced Repetition Advisor

The underlying principle behind spaced repetition -- that
studying at spaced intervals is effective for long-term memory -- is
still extremely valuable. How then, can that principle be incoporated into
a more human-centered design that takes into account the aforementioned
pitfalls?

A potential solution to these problems is a **spaced repetition advisor**. Instead of forcing you to study certain cards at certain times, the advisor determines an order
with which the cards should be studied.

### Conclusion

Pure spaced repetition isn't bad -- it just isn't right for everyone in
every situation. Like most things in life, having multiple options
to choose from is best, and I hope the idea of a spaced repetition advisor
can spur a discussion on human-centered flashcard review systems and
algorithms.

If you'd like to try out using a spaced repetition advisor, I created a
<a href="https://github.com/joshuamotoaki/gen-cards" target="_blank">prototype application</a> for personal use. It's completely free and runs locally on your computer. Eventually, I plan on streamlining this application to make it much
more suitable for general use.
