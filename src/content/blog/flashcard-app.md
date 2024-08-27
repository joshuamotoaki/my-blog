---
title: "Rapid Prototyping a Custom Desktop Flashcard App"
description: "Using Tauri and Svelte to rapidly build a flashcard app that I actually want to use."
pubDate: "Aug 22, 2024"
heroImage: "/posts/gencards.png"
---

Recently, I built a flashcard application which implements an original spaced-repetition-based system. This post outlines the rapid prototyping of the app.

### Why?

Honestly, I've wanted to build a flashcard app for years. When I first started programming a couple years ago, I was in the process of learning German. I was inspired by <a href="https://conjuguemos.com/" target="_blank">Conjuguemos</a>, an app I had used in middle school Spanish to memorize vocabulary, to create a flashcard app that made the user type the answer, as opposed to traditional flashcard apps where you manually enter whether you knew the card or not. Some apps like Quizlet had this feature, but I wanted a solution that ran locally so I could use it without internet (or a premium fee). I had attempted to build the application with extremely little programming knowledge and ultimately gave up.

Recently, as a German minor needing to review some vocabulary before the semester began, I revisited the idea of making a flashcard app. However, I had also developed strong opinions about spaced repetition (a system for determining exactly when you should study and review cards), and wanted to make my own custom system. I tried out <a href="https://apps.ankiweb.net/" target="_blank">Anki</a> (a popular spaced repetition app) one last time, and upon being dissatisfied, decided to finally build the app.

_If you're interested in reading more about my rationale behind building a custom flashcard app, see <a href="https://motoaki.dev/blog/spaced-repetition-advisor/">this post</a>._

### Planning

When I built some of my earliest projects, my number one mistake was not doing enough planning. I used to jump right into the code, and this would lead to an absolute disaster the moment there was any kind of complexity. So, this time, I wanted to make sure I knew roughly what features I wanted to include, the data structures for implementing these features, and the general look and feel of the application.

In my programming journal, where I record my thoughts and often do planning, I wrote down all the ideas that popped into my head and made sketches if I had an idea for the UI. Eventually, I had several pages worth of brainstorming, so I consolidated it into a feature list with accompanying sketches. I intentionally kept the feature set limited so that I could pull it off in a short period of time (I did need to urgently study some German).

Alongside this, I wanted to have a simple, yet intuitive editor for the flashcards, as well as a way to upload a CSV file to bulk add cards. For selecting decks, I wanted a dashboard that would display recent decks, and a library page with a search feature to see all decks. I also always love having custom colors and theming in an app, so that would be another small feature to add.

### Choosing a Tech Stack

As someone who has primarily been a web developer, there were really 2 main options: Tauri and Electron. <a href="https://tauri.app/" target="_blank">Tauri</a> is a relatively new framework which combines a Rust-based webview with web frameworks like React and Svelte to create desktop-native applications. It is very lightweight with small bundle sizes, and has plugins for things like using a local database or interacting with the file system.

On the other hand, <a href="https://www.electronjs.org/" target="_blank">Electron</a> is a much more established framework in the desktop-native space. Like Tauri, you can use your favorite frontend web framework. Due to being more established, there is a larger community around it and thus more support in case you get stuck. The main downsides are that it ships a NodeJS-based backend, making the bundle sizes much larger than Tauri, and it is also a bit less performant. Large apps like Discord and Visual Studio Code use Electron for their desktop applications.

There are also cross-platform options like <a href="https://reactnative.dev/" target="_blank">React Native</a> or <a href="https://flutter.dev/" target="_blank">Flutter</a>, which are primarily used for mobile-app development, but can compile to desktop. For example, the Facebook Messenger desktop application is built using React Native.

Ultimately, I chose to use Tauri since I've been meaning to do a Rust-based project and since it's a rapidly growing technology. I really considered React Native because I've worked with it a bit before, but I didn't really enjoy the developer experience. As for the frontend web framework, Svelte was an easy choice. I've used Svelte for my largest projects, and it's always a joy to work with. React was a potential option since I'm also quite familiar with it, but since this is a solo side project and I enjoy using Svelte more, Svelte it was.

I also wanted a UI library to go along with Svelte to make building the UI much easier. I went with <a href="https://www.skeleton.dev/" target="_blank">Skeleton</a>, a Svelte-specific UI library with prebuilt UI components. I like the way Skeleton looks and the fact that it has custom themes. I've also used it before for much smaller projects and liked the developer experience.

For data storage, I wanted to use a database instead of just writing to files. A database allows for the data to be structured and queried more efficiently, and can be very helpful to ensure performance with larger amounts of data. If I went with a file-based system, it would probably have been a bit simpler at first, but I would've ended up writing my own bad database as the project grew, which wouldn't have been ideal. For a database, SQLite made a lot of sense. It's the easiest to ship with the bundle, is very lightweight and fast for local use, and is the established choice for smaller projects like this. The main issue with SQLite is concurrency (if many users are trying to access the database at once), but since this is a local Desktop application, that isn't a problem at all.

Choosing a tech stack can be difficult. There are a ton of options out there, and they all have their ups and downs. Even while doing the project, I sometimes wished I used Electron for the larger community or React Native for familiarity. I think the most important thing is to try to get some idea of the technologies that are out there, pick something that sounds good, and just stick with it. There will be many more projects in the future to use other frameworks, and the fundamental concepts stay the same no matter the technology. That said, if I could go back in time, I would still choose the same tech stack for this project.

### Building the App

Building an application always takes more time than initially planned. After looking over the feature set, it seemed like this would be a quick and easy project for a few days, putting in 3-4 hours a day. However, it ended up taking about a week of a half at that pace.

#### A Rough Start

One of the first things I needed to do was to connect the SQLite database to my frontend code. Fortunately, Tauri has a plugin for SQLite that handles a lot of this. Unfortunately, there is very little documentation for this plugin. It didn't seem to work, and I couldn't find any info or examples about how to get it working. I found an example project and copied it line for line, but it didn't work on my machine (turns out the example couldn't run because of a versioning issue... classic).

After a full day trying to fix this issue, I considered building my own SQLite plugin in Rust from scratch. I dove into a couple of tutorials on how to do this, but then noticed that there was a Discord server for Tauri. On the Discord server, I found an easy answer: the plugin automatically creates a database file, but you need to add a single line of code to specify the name. After all that work, a very, very easy solution.

**Lesson:** if you're having a problem, it's likely that others are having a similar problem and that an answer is out there somewhere.

#### Scaffolding

With that issue solved, I was ready to dive into the bread and butter of the project. A huge thing I've learned from previous projects is to separate different layers of the application. For example, I have a module for the code that interacts directly with the database, a module that handles deck metadata, and a module that does the actual logic while studying flashcards. In Svelte, I do this by extended stores (which provide global state) with custom functions to interact with the state. A lot of this actually resembles object-oriented programming (perhaps Java really is the best). 

This part actually went pretty straightforward. TypeScript is super helpful in making sure that the data types are correct, and a few unit tests catch errors before they build up too much.

#### User Interface Work

One of the most tedious parts of frontend development is developing the user interface. Nothing too out-of-the-ordinary happened on this project -- with the exception of having to clear some of the defaults of WebKit (Apple's web view framework) so that SkeletonUI could look good. 

Some of the most important work is on things that aren't often considered at face value. For example, when you edit cards, you want to be able to keep on tabbing on the inputs to get to future cards. Normally, this would tab over buttons like the priority star and the delete button, so tabindex is set manually on these elements to skip over them. Furthermore, a nice feature I added (that other flashcard apps also do) is to add a new card to the deck when the last input of the last card is tabbed out of. This allows the user to continually input new cards without having to move off the keyboard. 

<img src="/posts/gencards-edit.png" alt="edit page" width="80%">

#### Optimization

There's always a ton of optimization you could do for any app, but there were a few main optimizations that really mattered for this project.

Even though the database is on the same machine (so there's no network delays), I overestimated its efficiency while working with large data. Even with 1000 cards, the app felt slow, and with 20,000 cards, you couldn't edit anything without a few second delay. The main problem stemmed from having all the cards in a flashcard deck being stored in the same row, instead of having a different row for each card. This would cause one massive (and slow) row read.

Another optimization came from fetching the cards from the database. When you first load into the app, to keep load times fast, only the metadata for each deck is loaded. Then, when a deck is clicked on, the cards were fetched. While this normally felt fine, for decks with thousands of cards, there would be a slight delay. I solved this by **caching** the cards when the button to click on a deck was hovered over, as well as the 6 most recent decks asynchronously after loading the app.

On the UI-side of things, when a JS framework like Svelte has a lot of items to render to the page, whether or not they are visible, the page load can be slow. There are 2 main strategies for dealing with this. The first is **virtualization**, a system where items are not rendered until they are in or near the viewport. An issue with virtualization is that you need to explicitly know the heights of items, and while this was possible, there would have been a lot of moving parts.

The second strategy -- the one I went with -- is **pagination**, where there's buttons to exchange the items that are on the page. Fortunately, Skeleton had a prebuilt component for pagination, so it was a very quick addition that led to a lot of performance gains.

### What's Left? (A Lot)

At the time of writing, while the app is useable (I already use it), there are a lot more features to be implemented and quality checks to be done before it is truly production-ready.

For example, I want users to be able to add tags to cards so that they can easily set an entire tag to priority. I want to implement conflict detection to avoid duplicate cards. Very importantly, I want to add a system to export an entire deck with the current progress so that a deck can be shared across devices. Each of those features will come with their own set of unforeseen challenges, and may potentially inspire even more features.

On the UI/UX side of things, the app isn't quite as beautiful as I'd like it to be. Right now, it looks like a quick side project (because it is), but if the goal is to have a flashcard app that just feels really nice to use in terms of the studying algorithm, the UI should match that niceness.

I haven't even mentioned the non-coding side. Even though this is a free and open-source application, I still need to have a place for the code to be downloaded. While Tauri has a prebuilt GitHub Action to build the code and add it to GitHub releases, just having a massive list of executables for each operating system is confusing to choose from. Eventually, I want to have a website that detects the operating system and picks the correct executable to download. Furthermore, I want to do at least some kind of marketing so that people actually use the app, even if it's just word-of-mouth.

I've found that even when you've implemented the core feature set of an application, there's still so much more to do. Minor bugs, both functional and visual, hide in every crevice of code. Ensuring responsiveness and accessibility for every element can be time-consuming. Even if everything works perfectly, once you use the app, you will certainly find areas for UI/UX improvements and potential features to add.

### Conclusison

There are a few general lessons that I learned from this project. The efficiency of handling large amounts of data should be considered, even on programs that run locally. Caching is usually a good idea whenever possible. When feeling stuck, seeking out human-created resources and answers (instead of AI) can really help to resolve problems. Triple or quadruple the time estimate of getting the project done. While some (or all) of these may seem trivial, hindsight is 20/20, and often learning a lesson the hard way is the best way to fully understand it.

If you're interested in trying out the app, you can download it at
<a href="https://github.com/joshuamotoaki/gen-cards" target="_blank">the GitHub repository</a>.
