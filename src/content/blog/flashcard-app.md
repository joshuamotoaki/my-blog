---
title: "Rapid Prototyping a Custom Desktop Flashcard App"
description: "Using Tauri and Svelte to rapidly build a flashcard app that I actually want to use."
pubDate: "Aug 22, 2024"
heroImage: "/posts/gencards.png"
---

Recently, I built a flashcard application which implements an original spaced-repetition-based system. This post outlines the rapid prototyping of the app.

### Why?

Honestly, I've wanted to build a flashcard app for years. 


_If you're interested in reading more about my rationale behind building a custom flashcard app, see <a href="https://motoaki.dev/blog/spaced-repetition-advisor/">this post</a>._

### Planning 


### Choosing a Tech Stack

As someone who has primarily been a web developer, there were really 2 main options: Tauri and Electron. <a href="https://tauri.app/" target="_blank">Tauri</a> is a relatively new framework which combines a Rust-based webview with web frameworks like React and Svelte to create desktop-native applications. It is very lightweight with small bundle sizes, and has plugins for things like using a local database or interacting with the file system. 

On the other hand, <a href="https://www.electronjs.org/" target="_blank">Electron</a> is a much more established framework in the desktop-native space. Like Tauri, you can use your favorite frontend web framework. Due to being more established, there is a larger community around it and thus more support in case you get stuck. The main downsides are that it ships a NodeJS-based backend, making the bundle sizes much larger than Tauri, and it is also a bit less performant. Large apps like Discord and Visual Studio Code use Electron for their desktop applications. 

There are also options like React Native or Flutter, which are primarily for mobile-app development, but can compile to desktop. For example, the Facebook Messenger desktop application is built using React Native. 

Ultimately, I chose to use Tauri since I've been meaning to do a Rust-based project and since it's a rapidly growing technology. I really considered React Native because I've worked with it a bit before, but I didn't really enjoy the developer experience. As for the frontend web framework, Svelte was an easy choice. I've used Svelte for my largest projects, and it's always a joy to work with. React was a potential option since I'm also quite familiar with it, but since this is a solo side project and I enjoy using Svelte more, Svelte it was. 

I also wanted a UI library to go along with Svelte to make building the UI much easier. I went with <a href="https://www.skeleton.dev/" target="_blank">Skeleton</a>, a Svelte-specific UI library with prebuilt UI components. I like the way Skeleton looks and the fact that it has custom themes. I've also used it before for much smaller projects and liked the developer experience. 

For data storage, I wanted to use a database instead of just writing to files. A database allows for the data to be structured and queried more efficiently, and can be very helpful to ensure performance with larger amounts of data. If I went with a file-based system, it would probably have been a bit simpler at first, but I would've ended up writing my own bad database as the project grew, which wouldn't have been ideal. For a database, SQLite made a lot of sense. It's the easiest to ship with the bundle, is very lightweight and fast for local use, and is the established choice for smaller projects like this. The main issue with SQLite is concurrency (if many users are trying to access the database at once), but since this is a local Desktop application, that isn't a problem at all. 

Choosing a tech stack can be difficult. There are a ton of options out there, and they all have their ups and downs. Even while doing the project, I sometimes wished I used Electron for the larger community or React Native for familiarity. I think the most important thing is to try to get some idea of the technologies that are out there, pick something that sounds good, and just stick with it. There will be many more projects in the future to use other frameworks, and the fundamental concepts stay the same no matter the technology. That said, if I could go back in time, I would still choose the same tech stack for this project.

### Building


### What's Left? (Hint: A Lot)

At the time of writing, while the app is useable (I already use it), there are a lot more features to be implemented and quality checks to be done before it is truly production-ready. 

For example, I want users to be able to add tags to cards so that they can easily set an entire tag to priority. I want to implement conflict detection to avoid duplicate cards. Very importantly, I want to add a system to export an entire deck with the current progress so that a deck can be shared across devices. Each of those features will come with their own set of unforeseen challenges, and may potentially inspire even more features.

On the UI/UX side of things, the app isn't quite as beautiful as I'd like it to be. Right now, it looks like a quick side project (because it is), but if the goal is to have a flashcard app that just feels really nice to use in terms of the studying algorithm, the UI should match that niceness. 

I haven't even mentioned the non-coding side. Even though this is a free and open-source application, I still need to have a place for the code to be downloaded. While Tauri has a prebuilt GitHub Action to build the code and add it to GitHub releases, just having a massive list of executables for each operating system is confusing to choose from. Eventually, I want to have a website that detects the operating system and picks the correct executable to download. Furthermore, I want to do at least some kind of marketing so that people actually use the app, even if it's just word-of-mouth.

I've found that even when you've implemented the core feature set of an application, there's still so much more to do. Minor bugs, both functional and visual, hide in every crevice of code. Ensuring responsiveness and accessibility for every element can be time-consuming. Even if everything works perfectly, once you use the app, you will certainly find areas for UI/UX improvements and potential features to add. 