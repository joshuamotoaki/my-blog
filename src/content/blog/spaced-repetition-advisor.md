---
title: "Human-Centered Spaced Repetition"
description: "A friendlier approach to efficiently studying flashcards."
pubDate: "Aug 23, 2024"
heroImage: "/posts/spaced-repetition-advisor.jpg"
---

Whether it be for coursework, exams, or competitions, students often need to do rote-memorization of flashcards. This can be tiring and time consuming, so many reach for spaced repetition, a strategy that promises efficient learning. However, no matter how much I try to like it, I just don't find spaced repetition enjoyable or effective for me. In this post, I explain why I don't like spaced repetition, and a potential solution that I've designed to remedy its flaws. 

### What is Spaced Repetition?

<a href="https://en.wikipedia.org/wiki/Spaced_repetition" target="_blank">Spaced repetition</a> is a
rote-memorization strategy based on psychologist Hermann Ebbinghaus's **forgetting curve**, which
posits that re-learning information after forgetting it reduces
the time it takes to forget and strengthens long-term memory. If you have a test coming up in a month, it's more effective to study at a few spaced intervals over the entire month than to cram into a single intense study session, even if the time spent studying is identical.

<img src="/posts/forgetting_curve.png" alt="Ebbinghaus's forgetting curve" width="60%">

Many studies have scientifically demonstrated that spaced repetition is an extremely effective technique (see <a href="https://pcl.sitehost.iu.edu/rgoldsto/courses/dunloskyimprovinglearning.pdf" target="_blank">this paper</a> by Dunlosky et. al -- one of my favorite educational psychology papers in general). When massive amounts of information (in situations like language learning or medical school) needs to be memorized, spaced repetition is a reliable strategy to learn everything without having to study day-in day-out.

#### Anki

With the high efficacy of spaced repetition, it's only natural that people would make flashcard apps that employ spaced repetition. The most popular of these is <a href="https://apps.ankiweb.net/" target="_blank">Anki</a>, a free software which utilizes extremely optimized algorithms for determining when cards should be studied.

While I often find myself needing to memorize large amounts of rote information (from classes and language learning), I don't use Anki. I've attempted to use it many times, but I find it quite difficult, with the user interface being fairly unintuitive and having too many configurable settings. There are plenty of guides on how to properly configure and use Anki, but my goal is to study flashcards, not to learn how to use an app. However, even if Anki were easier to use, I still wouldn't find that it fits my lifestyle.

### Why I Don't Like Spaced Repetition

While spaced repetition seems effective, I never have found it appealing for
two main reasons:

#### It takes away control

Spaced repetition is designed to optimize exactly when you review cards. Every day, you're given a set of cards that you must study that day. Failure to do so piles the cards up onto the next day. Not studying all the cards assigned for a day for a few days can cause a pile of cards so large that it may take hours upon hours that day to get through. 

This kind of rigidity discourages breaks, one of the most important things for long-term learning and mental health. Not taking breaks when you need one can cause burnout, which ultimately decreases long-term learning. 

To make matters worse, studying a ton on one day forces you to keep up a consistently high level of motivation on subsequent days. Sometimes you just get a random bout of motivation -- an app should encourage you to apply this motivation instead of making you worry about  repercussions. 

I've never met anyone who has the same exact motivation every single day. Sure, optimizing study strategies is a good thing, but that optimization shouldn't feel like a punishment. Your mental state is perhaps more important to study success than any method, and so your system of studying should feel great to use, and allow you to do whatever you want, whenever you want. 

But shouldn't people be encouraged to study every day? While this may be theoretically true, I still find that taking periodical breaks is far more helpful. I would much rather give up a little bit of efficiency than burn out and feel miserable for a week, which might completely throw the efficiency out the window anyway.

Even if you never needed to take a day off, what if you just have a busy day? Or what if there's an emergency? Studying flashcards shouldn't be a full-time job that you're on-call for. The hard part should be the studying itself, not the process.

#### It requires too many decisions

Most spaced repetition algorithms (like the popular <a href="https://github.com/open-spaced-repetition/fsrs4anki/wiki/ABC-of-FSRS" target=_blank>FSRS</a> algorithm
used by Anki), require users to manually input their confidence level after
reviewing each card (for example, easy, medium, or hard). While this improves the algorithm's ability to accurately schedule cards, it forces
users to constantly stop and think, instead of focusing only on recalling
information for the flashcards.

Furthermore, user interpretation of the difficulty levels can greatly vary.
Even the judgement of a single user can vary over time (I don't remember
what an "easy" card felt like a week ago). Also, you don't know what you don't know, and it's easy to over or underestimate your knowledge of a card. 

Having to make this decision also gives you an easy way out if you're feeling lazy. If you're really not in the mood to study more, you may not actually actively recall the cards (which is the main thing that actually gets you to memorize the cards) and instead just click "easy" because the card seemed a bit familiar. 

An ideal system would not require the user to reflect on the strength of their knowledge of a card at all. 

### A Potential Solution

The underlying principle of spaced repetition -- that
studying at spaced intervals is effective for long-term memory -- is
still extremely valuable. How then, can that principle be incorporated into
a more human-centered design that takes into account the aforementioned
pitfalls?

A potential solution I've created is a **spaced repetition advisor**. Instead of forcing you to study certain cards at certain times, the advisor determines an order in which the cards should be studied.

The advisor doesn't tell you when to study cards. You're free to choose your own study frequency and breaks. When you're ready to study, the advisor strikes a balance between introducing new cards and reviewing old ones. 

You can also mark certain cards as "priority" to ensure that they get introduced and reviewed before the other cards. This can be helpful if you have an upcoming exam or just feel like some words are more important than others. 

Additionally, since the precision of review times is less important than in traditional spaced repetition, a less optimized scheduling algorithm can be used. While this initially may seem counterintuitive, users can more easily understand a simpler algorithm. This way, users can tune the algorithm according to their preferences -- for example, do they want to focus more on learning new cards or reviewing others -- whereas with a more complex algorithm, tuning may not be possible (at least in a way that doesn't induce headaches).

As for not requiring decisions, users need to type out their answers. If they don't know the answer (or provide a wrong one), the correct answer appears and they must copy the answer. Doing this forces active recall (you need to know the answer in order to type it). It's much easier to see an answer and then remember that you knew it; it's harder (and more effective) to recall an answer and see the answer in case you didn't know it. This also allows the system to determine the difficulty of a card based on when the card is answered correctly or incorrectly. 

### Conclusion

Traditional spaced repetition isn't bad -- it just isn't right for everyone in
every situation. Like most things in life, having multiple options
to choose from is best, and I hope the idea of a spaced repetition advisor
can spur a discussion on human-centered flashcard review systems and
algorithms. The advisor is not groundbreaking (it shares most of the principles from spaced repetition), but rather a slight shift to make something that I previously felt was punishment into a great learning experience. 

If you'd like to try out using a spaced repetition advisor, I created a
<a href="https://github.com/joshuamotoaki/gen-cards" target="_blank">prototype application</a> for personal use. It's completely free and runs locally on your computer. Eventually, I plan on streamlining this application to make it much
more suitable for general use.

_If you're interested in reading more about the process of building a custom flashcard app, see <a href="https://motoaki.dev/blog/flashcard-app/">this post</a>._