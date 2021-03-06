---
layout: layouts/post.njk
title: >
  092 AiA webpack with Sean T. Larkin
date: 2016-05-12 07:00:35
episode_number: 092
duration: 47:18
audio_url: https://media.devchat.tv/adventures-in-angular/AiA092WebPack.mp3?rss=true
podcast: adv-in-angular
tags:
  - adv_in_angular
  - podcast
---

01:53 - Sean T. Larkin Introduction

- [Twitter](https://twitter.com/TheLarkInn)
- [GitHub](https://github.com/TheLarkInn)
- [Stack Overflow](https://stackoverflow.com/cv/seanlarkin)
- [Mutual of Omaha](https://www.mutualofomaha.com/)
  02:17 - Configuration02:56 - [webpack](https://webpack.github.io/)06:17 - [Grunt](https://gruntjs.com/) and [gulp](https://gulpjs.com/) vs webpack 08:02 - Plugins and Loaders
- [ng-annotate](https://github.com/olov/ng-annotate)
- [ng-annotate-loader](https://www.npmjs.com/package/ng-annotate-loader)
  09:49 - Downsides10:46 - Writing Less Code?12:50 - Configuration (Cont’d)
- [NgWebpackStarter](https://github.com/btroncone/NgWebpackStarter)
  14:23 - Metrics and Speed
- [Sightspeed.io](https://www.sitespeed.io/)
  18:12 - Migration Risk20:29 - The Learning Curve22:04 - webpack with Angular 224:21 - webpack and Angular 126:05 - Getting Started with webpack
- [angular-starter-es6-webpack](https://github.com/TheLarkInn/angular-starter-es6-webpack)
  27:34 - Why use webpack with your Angular 2 build?
- [Systemjs](https://github.com/systemjs/systemjs)
  36:32 - webpack Integration

### Transcript

**CHUCK:&nbsp;** Well, should we do an episode?

**_[This episode is sponsored by Hired.com. Every week on Hired, they run an auction where over a thousand tech companies in San Francisco, New York, and L.A. bid on JavaScript developers, providing them with salary and equity upfront. The average JavaScript developer gets an average of 5 to 15 introductory offers and an average salary offer of $130,000 a year. Users can either accept an offer and go right into interviewing with the company or deny them without any continuing obligations. It’s totally free for users. And when you’re hired, they also give you a $1,000 bonus as a thank you for using them. But if you use the Adventures in Angular link, you’ll get a $2,000 bonus instead. Finally, if you’re not looking for a job but know someone who is, you can refer them to Hired and get a $1,337 bonus if they accept a job. Go sign up at Hired.com/AdventuresInAngular.]_**

**_[Ready to master Angular? Oasis Digital offers Angular Boot Camp, a three-day, in-person workshop class for individuals or teams. Bring us to your site or send developers to ours classes in St. Louis or San Francisco – AngularBootCamp.com.]_**

**_[This episode is sponsored by Telerik, the makers of Kendo UI. Kendo UI integrates seamlessly with both AngularJS 1.x and 2.0. It provides everything you need to integrate with AngularJS out-of-the-box bindings, component configuration, directives, template directives, form validation, event handlers and much more and yet Kendo UI tooling does not depend on AngularJS. So, if you want to use it with Angular or not that’s totally up to you. You can check it out at KendoUI.com]_**

**CHUCK:&nbsp;** Hey everybody and welcome to episode 92 of the Adventures in Angular show. This week on our panel we have John Papa.

**JOHN:&nbsp;** Hello.

**CHUCK:&nbsp;** Jules Kremer.

**JULES:&nbsp;** Hello.

**CHUCK:&nbsp;** Joe Eames.

**JOE:&nbsp;** Hey everybody.

**CHUCK:&nbsp;** Lukas Reubbelke.

**LUKAS:&nbsp;** Yo.

**CHUCK:&nbsp;** I'm Charles Max Wood from DevChat.tv. And this week we have a special guest. That's Sean Larkin.

**SEAN:&nbsp;** Hey, how's it going, guys?

**CHUCK:&nbsp;** We're doing alright. Do you want to introduce yourself?

**SEAN:&nbsp;** Yeah. My name is Sean Larkin, obviously. I'm a user experience developer at Mutual of Omaha. I'm not originally from Nebraska but I've lived here for the past five years. And I'm obsessed with Angular 2 and Webpack. And I've had the fortunate opportunity to be able to talk about that in a workshop for ng-conf.

**CHUCK:&nbsp;** Now, when I heard people compare Webpack to Ember, they say it's configuration over configuration. Is that the case? I hear it's like this configuration nightmare sometimes.

**SEAN:&nbsp;** Well, I think that it really depends. At first glance it is daunting because you look at 50 lines of code that could accomplish what it takes about 500 lines of Grunt or Gulp code. Changing that mindset that you're right, it is configuration. And there is a learning curve because there is new, just like AngularJS there are new terminologies or there'd be compilation loaders, plugins, that we haven't really seen before in web app building processes.

**CHUCK:&nbsp;** Gotcha. So, I went right for the jugular. Do you want to explain really quickly what Webpack is? And I know we've done a show on build tools before but give us the 10,000-foot view. What is it? What does it do? And why are people using it?

**SEAN:&nbsp;** Well, Webpack lets you… 'What doesn't it do?' is the first question. At least that's usually what I tell everybody. Webpack is a web application bundler. Even more than just a web application, it's a module bundler. It's a JavaScript and static asset bundler. What Webpack does is it takes one or multiple entry files which serve as the contextual root of your dependency tree through your application or module. And then Webpack walks through its dependencies whether it be JavaScript, CSS, HTML, Icon files, anything. And it treats it like a module and then bundles it up into a single or many JavaScript bundles.

**JOE:&nbsp;** That was a lot of big words.

**SEAN:&nbsp;** [Laughs] That's the elevator pitch. [Laughs]

**JOE:&nbsp;** Alright. So, I'm going to act totally confused here and say, I want you to give me an example of why I should care about that. I've got a project, Angular, using script files to load my files. Everything seems to be working good. Why should I care?

**SEAN:&nbsp;** So, I guess you'd say the way that people are developing JavaScript files is that it changes every two months or three months. Module dependency has…

**JOE:&nbsp;** I wish it was that stable.

**SEAN:&nbsp;** [Laughs] That's true. Okay, two weeks. But [laughs] the way that modules are declared, defined, required, imported, it changes so much. So, whether it be CommonJS, your traditional script tag, variables in the globals window scope, or in Node, AMD, UMD, Webpack can handle any of those files and understand what their imports are. So, the first thing is it's really flexible to any development stack. So, let's say you're using PHP and Laravel and you have to serve your assets up at a specific path. Well, Webpack can do that. Let's say you want to build a Node module that targets Node for CommonJS. Well, you can do that. Let's say you want to load all of your LESS files into one file and bundle it in a JavaScript file. Webpack can do that.

The power behind Webpack is that you can define what are called loaders which essentially tell Webpack how to treat a file based on its extension. So, if it sees .less or .css or .stylus, anything, you can define community-driven plugins that will handle those assets appropriately. Some of my favorite things about it are let's say like image loaders or URL loaders. You have the opportunity to take image files that you'd traditionally have to serve up statically aside from your build process and Webpack can automatically encode them into base64 inline. So, there are a lot of enhancements and optimizations that in the current platform for web being HTTP 1, having one or two sole bundle files or applications is really great and convenient.

**CHUCK:&nbsp;** So basically, it just manages your entire build process?

**SEAN:&nbsp;** Everything. Yeah, it manages every aspect of the build process.

**JOHN:&nbsp;** So, how does that compare with… so, Webpack is a lot configuration. And we've had something in the past like Grunt was just all configuration. How do those two compare? And then if you could take this further and say, how does Webpack overlap or not overlap with things like Grunt and Gulp?

**SEAN:&nbsp;** So, Grunt and Gulp is more of a task runner. So essentially, you're performing a series of tasks that we'd probably just deem time-consuming such as concatenating a JS file. Or Grunt will go ahead and run, well actually in Gulp as well, they iterate through all the files that you pass it and then you perform tasks on it. It's similar in terms of the syntax where Webpack, to configure it you'd define it as an object and then you export it. But Webpack treats it differently as it's compiling and bundling through these files. You have the ability to take and augment a behavior through every step. And there are a lot of plugins that are baked right into Webpack [such as] handling different types of exports, to code splitting, to using occurrence order. You can take and apply a whole bunch of different plugins. Simply said yeah, I could [inaudible]

**JOHN:&nbsp;** Yeah, I mean what [we're] really saying [inaudible] the things that it's doing is the same stuff that Gulp or Grunt does. So I guess, the things that it accomplishes are the same. I guess I'm trying to understand how would you differentiate the value or the pros and cons of Webpack compare to the other two then?

**SEAN:&nbsp;** I'd say one can do it with about 50 lines of code and Grunt and Gulp it might require 200 or 400 lines of code. Some of the experiences that I've had with Grunt and Gulp is that after they're set up you don't want to touch it. And you kind of step away and you're afraid to go back and configure it because it's hard to maintain.

**CHUCK:&nbsp;** So, does Webpack manage a lot of this stuff through plugins? Or is it all just there and you just have to have the right dependencies installed? Or how does that work?

**SEAN:&nbsp;** Okay. So, it's a combination of both actually. When it comes to loading JavaScript files there are some native CommonJS compatibilities that Webpack automatically can pick up and require JavaScript files and JavaScript files. But let's say you want to use TypeScript or let's say you want to use ES 6 style classes. You have to use specific loaders based upon what kind of files you're importing. So yeah, Webpack is really driven by a collection of plugins and loaders that augment the behavior or what Webpack does.

**CHUCK:&nbsp;** So, how does this relate directly to Angular? I remember back in the day we would have these build tools for Angular and it would minify and that would goof everything up so we had to use the funny syntax to make sure that we had the string and the import library and then it would inject everything properly and not rename the wrong variables.

**SEAN:&nbsp;** Yeah.

**CHUCK:&nbsp;** Are there tools that are just built into Webpack or is there some kind of system that you use for that?

**SEAN:&nbsp;** Like I said there are lots of community-driven plugins and loaders. So, in your case that you've talked about right there, the ng-annotate-loader. Essentially what you do is you chain it to the JavaScript loader. And essentially what happens is that when the ng-annotate-loader runs through any of your Angular directives or files that have the dependency injection it includes automatically for you the specific comment required to use string DI. And it's as simple to implement as installing ng-annotate-loader and then chaining it onto your loaders in your config.

**CHUCK:&nbsp;** It was ng-annotate, that's what I was trying to remember.

**SEAN:&nbsp;** Yep.

**CHUCK:&nbsp;** So, are there any… it seems like okay, it's a build tool like any other build tool. Are there any downsides?

**SEAN:&nbsp;** Yeah, absolutely. And [Laughs] I'm starting to figure it out now more than anything because speaking at ng-conf my original… I went into the mindset that I need to make something incredible and ridiculous and kind of break the ground in terms of what Webpack can do and push the limits. And then I realize that really, Webpack is maintained by one developer, and his name is sokra, Tobias Koppers, on his free time for about three to four hours a week. At least that's what he's mentioned before. And so, when it comes to the core Webpack functionality that's one of my concerns is that it's a huge project that I wish some company would just pay him to write full-time. Only because there's such community backing and in terms of trending and bundlers and process management systems, Webpack has the market share right now.

**JOHN:&nbsp;** So, you said a few things that I think are really interesting. And I love build tools. I love Grunt and Gulp. I haven't used Webpack as much but I use it a little. It sounds like you're saying that you'll write less code in Webpack. So, I'd like to clarify if that's what you meant. And then on top of that if you are writing less code in Webpack I'm assuming that you're implying that the plugins in Webpack and the design of it make it such that you don't have to write as much custom code like you do in Gulp or Grunt to do the same things. If that's the case then, how do you customize things? Like if you have a very specific type of build process you want, how do you tap into that so it's not black-boxed?

**SEAN:&nbsp;** Yeah, absolutely. The best way is to write a custom loader or a custom plugin. Essentially, the way that Webpack was written is that when you create a custom loader all you're doing is returning a function that takes a compilation argument. You essentially… 'this' or 'this.' is within the compiler context.

And so, what I really like about it is that by simply creating a test string which is a regex string for let's say JavaScript files or TypeScript, I'll use the example because I just wrote a custom loader because there was something that was really irritating me. Let's paint the scenario. Say I want to not have to write requires in my Angular 2 components to pull templates and styles. Originally in Angular 1 with just Babel or regular JavaScript I could do an import template from template.html and it would return me the string. But with TypeScript and typing that import is a reserved namespace for TypeScript compiler. And so, it throws a lot of errors. So, what you can do is I wrote a custom plugin that would take and read my TypeScript files first and it would just do a regex replace of an import with a require. And so, that way I can continue to write imports but then it turns it into a require and then passes it to the TypeScript loader.

**JOHN:&nbsp;** Right. So, like in Gulp or Grunt you would just create a custom talk in Gulp or you create your own custom task in Gulp or Grunt. One is code, one is configuration. You're the same thing. But what about this config that Charles alluded to in the beginning? We hear a lot about Webpack like you generate a basic Webpack and you end up with this massive config. Is that real? Is that false? What's in there?

**SEAN:&nbsp;** You know what? I blame Patrick Stapleton because he's made some of the most awesome full-featured Webpack configurations.

**CHUCK:&nbsp;** [Laughs]

**SEAN:&nbsp;** [Chuckles] But they already…

**CHUCK:&nbsp;** Full-featured. I like that term.

**SEAN:&nbsp;** Full-featured. Well, it's like the beauty in Webpack is it's like a sword without a sheath where you accidentally shank yourself at the same when you hold it. Where essentially the fact that it can do anything makes people want to do anything. So for example, let's say [chuckles] a good example is if you look at the NgWebpackStarter. There are three different configs and they're using a Webpack merge which essentially is doing an object merge. And essentially [chuckles] what that does is it allow you to customize your environments for specific reasons. But on top of that there are all these extra features that allow you to let's say, oh do you want to use and target web workers? Okay, you can do that with Webpack. There's a web worker target. Do you want to target Node and Electron? Do you want to target Node-Webkit? Do you want this to be a Node library? Do you want to export UMD? And so, all these awesome, amazing features, people get really grandiose ideas and want to make the Angular 2 Webpack advanced seed ultra-mega do anything Internet of Things repository. And yeah, it does look a little daunting. [Chuckles]

**LUKAS:&nbsp;** So, I want to change gears here for just a moment, because you've been talking a lot about raw code goes into Webpack and it comes out and I think that's super beneficial. But I had a situation maybe a week ago that I think is worth chatting about. And that is I delivered a project to a client and there were some political things going on and the story came back that “Oh, you're using Angular. That's heavy. We need to stop and see what's going on here. This may not be the right solution.” And incidentally I was using Angular 1 with ES 6 and I used the NG6-Starter from AngularClass which I love. And what I did is I got Sitespeed.io, the Gulp plugin which is really, really awesome, and I was able to just run some metrics on this application. And so, Sitespeed.io was based on these industry accepted best practices. And so, right out of the box because of what Webpack was doing by taking all of the JavaScript, all of the CSSs, all of the HTMLs, basically all of these assets and bundling them into one or two files, that I basically hit I think it was a 90 out of a hundred right out of the gates.

And so, that's something [when you're talking about] Webpack I don't hear very often. But you actually get this really optimized build right out of the gates because it's taking everything and bundling it into these really optimized files that's really nice to consume. One of the things that I did get dinged on was the larger file size. But when you are on a mobile device, the worst possible thing that you can do is actually making remote calls, especially over 3G on a mobile device. That's the most expensive operation. And so on this case, it was fine to take that large payload hit upfront because you're minimizing resource requests over the mobile network.

And so, that kind of… one, is now I had these clear, defined metrics of no, Angular is not huge. This site is actually very optimized thanks to Webpack. And I pretty much walk into a meeting, put these numbers out there and did a mic drop and walked away. And the nice thing is I didn't actually even have to think about any kind of performance or what was coming out of… I didn't think about it at all because Webpack actually bundled that all up for me. And then I just had to use Sitespeed.io to verify to basically put some numbers around it. And I was extremely pleased about the outcome around that.

**SEAN:&nbsp;** Yeah, absolutely. That's one of my favorite parts. And the analogy that I'm always reminded of that I heard at a local NebraskaJS talk was that HTTP 1 when it comes to loading files is like a train. So, it's slow to start and slow to stop. But when it actually picks up speed, the transfer is actually really fast. And so, a single build file or maybe one or two build files is really, really great for HTTP 1 and it allows your assets to be loaded really quickly. For me personally in the projects that I work on at Mutual of Omaha I might sometimes split them up into a vendor bundle so then that can be cached. And my app won't be cached. But overall you're right. A biggest pull that most, like you said, people don't talk about is that it's really optimized for the current landscape of web loading in HTTP.

**LUKAS:&nbsp;** For free.

**SEAN:&nbsp;** For free, exactly. Yeah, [chuckles] that doesn't even count tree-shaking.

**CHUCK:&nbsp;** [Chuckles]

**SEAN:&nbsp;** [Chuckles]

**JOE:&nbsp;** One of the things that I think is interesting is the fact that Webpack is coming along after Gulp and Grunt. Sorry, I put those in the wrong order. We had Grunt then we had Gulp and now we've got Webpack. And it's like the flavor of the day. In some cases you feel like, we're doing Grunt. Now we're all doing Gulp. Now we're all doing Webpack. Is there a risk you think that we're going to be seeing everybody migrating to yet another tool here in six more months and we're all going to be wondering, “Ah, now what do I do?”

**SEAN:&nbsp;** I guess you could ask React developers the same thing, because my joke is that we see a new app seed or boilerplate using a different bundler quicker than React state libraries. But I guess the best thing is that if something better comes out that does what Webpack does and more, heck year, why not switch to it?

**JOE:&nbsp;** Because it's a pain in the butt. [Laughs]

**JOHN:&nbsp;** Yeah, that's where I get to, and this isn't just Gulp or Webpack or Grunt, but anything you have to switch to, a lot of large businesses [or even medium-sized businesses], they want to take a bet on something they can stick with for an indeterminate amount of time. Maybe it's a year. Maybe it's three years. They have something in mind where they're like, “You know what? We're going to place a bet on one of these. As long as it does the job and we can handle it, we're going to live with that for a couple of years.” And I don't think any of these [inaudible] frankly are bad choices. They're all a good choice. I also don't think you're going to be in a hole if you choose any of them, meaning [inaudible] choose Grunt, Gulp, or Webpack you're going to have a build process. And you're going to be able to do what you want. It's not like one of them is going to lead you at a cliff somewhere and you just can't get past it. So on that side, I don't think it's worth just changing just because it's flavor of the week. And I'm [inaudible] percent sure there'll be a new one [inaudible] another year.

**JOE:&nbsp;** Yeah. I'm still using script.aculo.us because I'm not sure about this whole jQuery thing.

[Laughter]

**JOHN:&nbsp;** You know what's funny is…

**JOE:&nbsp;** There might be something new coming out.

[Laughter]

**JOHN:&nbsp;** What's funny is I think classifying these is interesting. So, we've said for a while before Webpack came out we said Grunt is great if you're not a developer even. You just want to have a config file, a JSON file. So, a non-dev can actually do it because they just need config. The downside is you can't really breakpoint into it or debug it. The sequence of events isn't very obvious. Gulp on the other hand is great if you're a dev because you can breakpoint and walk through that. And it's a little more intuitive for devs. But the downside there is if you're not a dev you have no idea what you're doing because it's code. Webpack the way I'd look at it, and tell me what you think Sean, is that's a little bit more on the Grunt side where it's configuration. But it's a little easier than Grunt in a sense. A lot of that stuff has come out of the box. And instead of pulling in a task and having to plug it in with configuration, you're really just tapping into preexisting plugins.

**SEAN:&nbsp;** Yeah, absolutely. Trying to work Webpack into your stack is as hard as doing an npm install and adding the extra functionality. Or like you said, yeah…

**JOHN:&nbsp;** Which is hard for some people, Sean. So…

**SEAN:&nbsp;** Well…

**JOHN:&nbsp;** I wouldn't underestimate that. I've seen a lot of people [struggle with] npm.

**SEAN:&nbsp;** Yes, [that's true]. That's true.

**JOE:&nbsp;** Oh yeah, corporations that don't allow certain things, right?

**SEAN:&nbsp;** Well, I do work with insurance companies. So, I can relate to that. Yeah, I would say in terms of the learning curve it's a little daunting at first. But it combines the best things about Grunt and Gulp together and adds sugar on top of it and extra features that you're like, “Can I do this?” and “Yes” again. There has been a case where, okay I'll give one example. And somebody on Stack Overflow said “Can I use Webpack to include a CSS file in my email templates?” So, yes I'm sure it's possible. But that's probably the first case that anybody's asked me in terms of configuration or stacks if Webpack can meet their needs.

**JULES:&nbsp;** So, if I could change the topic a little bit as well, I'm curious what your opinion will be on Webpack with Angular 2.

**SEAN:&nbsp;** Well, what's awesome about Angular 2 is that now that it's using TypeScript you don't have to do as much with Webpack to fit it into the ecosystem in terms of JavaScript and importing dependencies. In terms of typing and definitions, it's maybe another story. I've spent… a lot of my first frustrations with Angular 2 and Webpack really just resolved around configuring the TypeScript config files and making sure where to tell TypeScript where all these definitions where. And maybe that's even separate from Webpack itself. But you get a lot of the same awesome features like being able to inline your CSS with a require statement. You can inline your templates with a require statement which in my opinion, I use Sublime Text 3. And so, being able to actually have the awesome features like [Emmet] in my HTML makes it easier to write templates for Angular 2 components. And so, I like being able to not only have a separation of concerns for readability but it's faster than template URL because you never have to make a request.

There are also things like when it comes to I guess if you looked at Angular 2 seed advanced, which is a really, I'm not going to say feature-rich again, but it's a repository that aims at trying to use a core set of Angular 2 components and then a development platform that targets three whole platforms, so desktop, mobile, and in the web itself. What's really neat about, and that's written in Gulp. I think one of my goals for the future is to maybe try and make a Webpack version of that if Patrick Stapleton doesn't beat me to it. What's awesome is that Webpack can not only handle optimizing and removing any duplicate code between your dependencies but you can automatically target different systems. So, one of them is for Node-Webkit or Electron. Well, automatically off the bat Webpack can wrap your code and make it bootstrappable for Electron or NativeScript or any of these frameworks that are out today.

**JOE:&nbsp;** So, what about Webpack and Angular 1?

**SEAN:&nbsp;** [Chuckles] So, that's where kind of I fell in love with Webpack in general was working in Angular 1. The first exposure that I had was like you said, the NG6-Starter I believe is what it's called.

**LUKAS:&nbsp;** That is correct.

**SEAN:&nbsp;** I created a repository at my first few weeks at Mutual of Omaha that the whole point was I wanted to give people something that they could instantly spin up a single page application. But at the same time, a designer could jump in and could immediately be able to edit templates and work hand-in-hand with the developer and push changes. And so, I used that and ripped out some pieces that I disagree with, added some extra functionality that I really liked from a couple of different repos, and I came up with two obnoxiously named to speak about it on the air Webpack Angular 1 repository that I use every day. I think maybe the best part is the generators that allow you to build the structure as well as… since you are using requires and exports, instead of every having to use the Angular setter/getter more than once you can essentially define your app module at your entry file and then as you have your components or in this case your directives, your controllers, everything is a function which is exported that takes an argument which is your app module. And so, what I really like is that you never have to call angular.module and call your module and then define something on it. It makes it really nice because you can rip out a component and put it in a completely different project that uses this structure. It's really modular and it makes the Angular development really nice.

**CHUCK:&nbsp;** So, is there a good place to get started with Webpack if you're building an Angular app? Or if you don't really have a solid build process, inserting it into an existing Angular app?

**SEAN:&nbsp;** I could shamelessly promote the two repos that I use. In terms of Angular 1 and Webpack you can certainly take a look at the NG6-Starter. The one that I have is called angular-starter-es6-webpack on GitHub but you could just find my repo on TheLarkInn with two N's and take a look at it. It hooks up a little bit more than what the ES 6 starter had, but both are really great resources. If you want to learn Webpack and the fundamentals, some of the best links that I can provide are those, the repos to AngularClass. What they're doing right now in terms of building all these repositories and bootstrappers that give you an application shell and let you start off right away, that's the kind of way that I learned. It lets you pull out pieces, break things, and put it back together, and figure out how it works

**LUKAS:&nbsp;** I would also like to point out, because Joe will not say this but he actually has an excellent course on Pluralsight. That's [how I learned] Webpack.

**JOE:&nbsp;** Aw, thanks.

**SEAN:&nbsp;** I just [inaudible]. Yeah.

**JOE:&nbsp;** Sorry, what did you say? You just what?

**SEAN:&nbsp;** I just saw, or I just found out about that Pluralsight course. So, I want to take it myself and see what I [inaudible]

**JOE:&nbsp;** [Laughs]

**SEAN:&nbsp;** In terms of the knowledge.

**JOE:&nbsp;** Let me know if there's anything I missed as well.

**CHUCK:&nbsp;** Any other things that we should tackle on this?

**JOE:** Can we talk about how… the different Angular 2 builds.

**SEAN:&nbsp;** Like how many different ones there are?

**JOE:&nbsp;** Like Webpack's relationship with Angular 2 builds. And there are plenty of other ways to do it.

**SEAN:&nbsp;** Are you saying like different… Webpack being one and the other like SystemJS, JS [inaudible], Browserify?

**JOE:&nbsp;** Yeah. Yeah, so alright. Let me ask. Let me make this into a question. When you're considering Angular 2, a lot of the tutorials out there are using SystemJS basically, TypeScript as their build. No Webpack. There are definitely Webpack starter kits out there that make things easier. But why should you even… those are not the de facto let's say. Why should you look and say, “Take the extra effort” to look at using Webpack with your Angular 2 build?

**SEAN:&nbsp;** Well, it's tough because in the weeks coming I've been really conflicted after talking with some of the developers for the Angular 2 CLI as well as Pascal Precht. I was getting advice and saying, “I really want to provide people with the simplest, easiest exposure to Angular 2 and Webpack because one, what's out there right now is complex and the configurations with TypeScript are a little daunting at first. But what's nice about SystemJS is it's really more about how it requires files in the browser or emulates a file system, which is cool and allows things like Plunker to work awesome with Angular 2. But it's not a bundler and it can't take and convert your LESS files into CSS or it can't allow you to use PostCSS plugins.

I see Webpack as bridging the gap or filling all the excuses for not wanting to use a new build system or a new framework. So many times I hear, “Oh, well we don't have support for this,” or, “We're using LESS now,” or, “We're using Sass,” or, “We can't use TypeScript,” or let's say, “We can only export our code in script tags.” [Chuckles] You'd be surprised how many times I've heard that. Webpack can really handle all of those things. What I've seen in the past is that it pushes people over the hill to be able to start using something like Angular 2 which they thought was a huge, daunting task.

**JOE:&nbsp;** Speaking of over the hill, Ward, do you have any questions?

[Laughter]

**SEAN:&nbsp;** Correct me Ward, [inaudible]

**CHUCK:&nbsp;** Man.

**WARD:&nbsp;** Well dude, I am… this is not my strength though. I'm just sitting here, well letting it wash over me. But there are things that I swear I'm watching in SystemJS 2 like transpiling, like LESS and Sass. And anyway, I've seen in used in combination with other things. And I know it can be used to bundle. So, I'm confused by some of the claims. But I'm not an expert. And I try very hard not to know anything about either of them. So, I'm lost. But I swear that it does these things.

**SEAN:&nbsp;** Well…

**WARD:&nbsp;** But ah, John knows better. See John…

**SEAN:&nbsp;** The [best thing about my life] is that Google answers most of my questions as a developer of the day. And so, it looks like you're right, is that it can support preprocessors. So…

**WARD:&nbsp;** It's got [inaudible] and all kinds of things, yeah.

**SEAN:&nbsp;** So [inaudible].

**JOHN:&nbsp;** Yeah, SystemJS does do some build things. But it doesn't do nearly what Gulp and Grunt and Webpack do. Mostly it's a simple, a very simplistic preprocessor. But mostly it's there for module loading, which is a different story than a build process.

**WARD:&nbsp;** But doesn't it also do bundling, John? I thought there was all of this…

**JOHN:&nbsp;** Jspm does. Jspm does bundling which has a piece of SystemJS. But it's really not the same thing. And that's where I kept thinking it's a little weird is SystemJS, forget build systems for a minute. If we're just trying to find something that does module loading, today that's what the Angular team is using SystemJS for. They're not using it for a build process. But they could if they wanted to but I don't think it will be the right choice. If you didn't want to use SystemJS could you use Webpack to do module loading, Sean?

**SEAN:&nbsp;** You wouldn't want to because SystemJS replaces the need to bundle the files.

**JOHN:&nbsp;** Not entirely. So, SystemJS in a [inaudible] system you can load one file and let them load one at a time. But you can also use jspm to create bundles. So, it's loading sections at a time too if you want. But if you wanted to, forget how I work with it, but if you just wanted to use import module and then go, how do you do that with Webpack? What code would you write to kick off a project in Webpack?

**SEAN:&nbsp;** In Webpack to allow it to import files?

**JOHN:&nbsp;** No, like let me [inaudible] of the way. In the Angular 2 examples right now the first line of code is system import main. It starts with a single main.ts file. That would go away if you weren't using SystemJS because that's part of SystemJS. How would we replace that to call the starting point in an Angular 2 app with Webpack?

**SEAN:&nbsp;** In that case all you'd have to do is use bundle.js because what happens is that Webpack takes and converts it into, transpiles all those TypeScript files in the entire dependency tree into one or multiple bundles. So, it's just like putting a script tag inside the browser. Are you saying without or with SystemJS?

**JOHN:&nbsp;** Without. Because I've often heard it referred to as, “Hey, we can also do module loading with Webpack” and one of the things module loading does is you tell it “What file do I start with? Where in this code whether it's in a bundle or not, where do I start my code so I can continue the dependencies?”

**SEAN:&nbsp;** Oh, I think that… you know what? This is actually the exact same with that I talked with somebody on the Angular CLI team about. Are you talking about on-demand module loading?

**JOHN:&nbsp;** No, just kicking off the project. Like you've seen the samples right? Where it says system.import main.ts? That says “Go look at this file. That's where I'm going to call the bootstrap code for Angular.”

**SEAN:&nbsp;** Correct.

**JOHN:&nbsp;** If that code isn't there, because that's part of SystemJS, the system there, if we don't do that line of code something has to tell it where does my project begin? And I know Webpack's got to have it. I'm just not familiar enough with it to know how you do that.

**SEAN:&nbsp;** Webpack takes and defines an anonymous, I don't want to call it anonymous function, but it wraps all of the code inside of the project inside its own private scope. And then Webpack chains all the modules that it has loaded in the dependency tree and requires them based upon… it essentially builds a syntax tree to know exactly what files are needed by which. But they are called not on demand yet, but they're all essentially loaded at once to be able to tell what, let's say your Angular 2 bootstrap where to load or pull your dependencies from. It's like it makes a mini-environment that allows you to import files within the browser runtime. I wish I could pull up and show a Webpack build file without the UglifyJS so I could explain a little bit better. But this is one of the biggest hurdles that trying to explain the configurability. You can say “Hey, you can split your code into five chunks and then share some of your code or your vendors and make them all instead of having to duplicate dependencies to reach to modules that you're using.”

**JOHN:&nbsp;** Yeah. So, let's say you do that. You make the different chunks and stuff. That's just the chunks of the modules of the dependencies. But some place in your app you have to tell it “Where do I start my code?” Is there like a configuration setting in Webpack that says…

**SEAN:&nbsp;** Yeah, that's your entry file essentially.

**JOHN:&nbsp;** Okay, that's why I'm saying, is there's got to be something that tells it “Start here”.

**SEAN:&nbsp;** [Laughs] Sorry about that. [Chuckles]

**JOHN:&nbsp;** No, no. No worries. It's hard to talk about it and not look at it. So, instead of system.import main which I do in SystemJS, I would just set an entry file inside of Webpack?

**SEAN:&nbsp;** Yeah, absolutely.

**JOHN:&nbsp;** Okay.

**SEAN:&nbsp;** The entry file serves as your contextual root, I guess. That's the best way I've been able to describe it. The root of [the] entire app.

**JOHN:&nbsp;** I think that's good. You explained it well, because that's really… forget Angular. Forget the internet. Forget any set of technology. If you take over someone else's project or you're learning a new technology one of the first things people look for whether they admit it or not is if I start this app, what's the first line of code to run?

**SEAN:&nbsp;** [Laughs] It's [so true].

**JOHN:&nbsp;** It really is. And it helps you to get context, especially when you're looking at an app that… some of the apps I deal with are thousands upon thousands of files. And it's like, “Oh my gosh. Where do I start?” You know what? In an Angular app I'm looking for main. [Chuckles]

**SEAN:&nbsp;** That's been actually one of the most enjoyable parts, even Webpack aside, about working with Angular 2 is that you don't have to just automatically know where core functionality comes from. If you want to extend something all you have to do is follow the import tree to see exactly where it comes from. Follow the exports and the imports and you can see exactly where core classes are or what they're trying to do.

**JOHN:&nbsp;** Very cool.

**SEAN:&nbsp;** And [inaudible] especially when it's typed to see what they're expecting. And in the same way, that was half the fun of being able to work with Angular 1 and Webpack is that it provided that same functionality that you're getting now in Angular 2.

**JOHN:&nbsp;** So, Sean I have one last comment and I think this is something I hope you're signing up for. And that's the Angular CLI team, one of their goals is to try to work with things like Webpack, SystemJS, Gulp, Grunt, Broccoli, whatever you want to use. I know they would love to hear from you about how do we best integrate Webpack into CLI if somebody wants to go that path? Are you going to help them?

**SEAN:&nbsp;** Yeah. Mike Brocchi already said he was going to deny my pull request if I tried to implement Webpack with CLI [laughs]. I think that… I brought it up a couple of times actually because it's so popular. It feels like it would be a shame or a crime to not include Webpack into the CLI functionality. So yeah, that's actually one of the… there are two things that I really wanted to tackle in terms of Webpack and Angular 2 development, at least in open source. One is being able to incorporate Webpack into the CLI and two, being able to have one Webpack config to build all the things repository. Which may have been taken care of now that… as weeks go on. But yeah absolutely. Right now their current stance or at least the kind of feel that I've gotten from it is that because Webpack doesn't support things like on-demand loading modules, that it’s not optimized for Angular 2. It’s a feature that's coming in Webpack 2, the tree-shaking dead code elimination on-demand module loading. But I would love to see it, because there will be nothing greater than having a bootstrapped project instantly created for you with the Webpack configs that you need.

**JULES:&nbsp;** Well, I know that we have talked to the CLI team, or I clearly work on the Angular team and we have had discussions in the CLI team about ensuring that it works with Webpack and that we don't ignore the fact that Webpack does have such a huge audience. So, it's on the list. But probably just something that the team hasn't looked at yet.

**SEAN:&nbsp;** Yes. I think what I was told is, wait 'til after the conference. [Chuckles]

**JULES:&nbsp;** I'm pretty sure I've uttered that at least 15 times today alone.

**SEAN:&nbsp;** [Laughs]

**CHUCK:&nbsp;** Wait, there's a conference?

**JULES:&nbsp;** There's a conference? What conference? I'm watching Brad Green create the keynote slides as we speak. What conference?

**CHUCK:&nbsp;** Ooh, can you give us some inside knowledge?

**JULES:&nbsp;** Can I give you some inside knowledge?

**JOE:&nbsp;** He's going to talk about Angular 2.

**JULES:&nbsp;** I think he's going to talk about Angular 2. I could be wrong. But I'm fairly sure that's the topic, yeah.

**CHUCK:&nbsp;** You guys suck. Okay.

**JULES:&nbsp;** It might have something to do with web applications. Maybe, maybe he'll talk a little bit about performance. I'm just spitballing here.

**SEAN:&nbsp;** I'd like to hear about Universal working with PHP and Drupal since that's my company's stack kind of for some applications.

**JULES:&nbsp;** Oh yeah? Actually there's going to be a longer talk on that at DrupalCon if you're going. Igor will be going there to give that talk.

**SEAN:&nbsp;** Where can I find more information about that? Because I would love to see that.

**JULES:&nbsp;** If I had been prepared for that question I would have had the conference website at my fingertips. But it's DrupalCon so there's this other website called Google. And I'm pretty sure if you google DrupalCon you'd find it.

**SEAN:&nbsp;** What? Okay. I'll look for it.

**JULES:&nbsp;** Beautiful.

[Chuckles]

**SEAN:&nbsp;** [Inaudible]

**JULES:&nbsp;** It actually should be at Angular.io/events as well since it is Igor attending.

**SEAN:&nbsp;** [Inaudible]

**CHUCK:&nbsp;** Alright. Well let's go ahead and get to some picks.

**JULES:&nbsp;** Alright, my pick, I can go first because my pick is in an attempt to make myself less lonely, sort of. [Laughs] So, I hike a lot and I like to hike on very long hikes. I found that the average friend when I say “Hey, let's go on a hike,” they're expecting a one and a half mile hike to somewhere very popular. But I'm more like the “Let's find a really secluded place where if we get lost no one will find us and go 10 miles out and hope for the best.” And so, usually my phone doesn't work. But I recently ran across this thing called goTenna. It's at goTenna.com and it basically lets you create your little mesh network within a certain mileage footprint. So, I'm up in Mountain View right now. I live in San Diego as you know and they're sitting on my doorstep. And I cannot wait to find a very long and secluded hike and a friend to go with me over the weekend.

**JOE:&nbsp;** Wait, I don't understand. What does it do?

[Laughter]

**CHUCK:&nbsp;** So Joe, you climb a tree first…

[Laughter]

**JOE:&nbsp;** I understand that. That I understand. I've done that many a time.

**JULES:&nbsp;** So, it basically allows you guys to, or allows people to be able to create their own small network within a certain mileage capacity. And I don't remember exactly what that is off the top of my head, so that you can connect to each other via text. So, imagine you get off trail, you've lost one of your friends, and you all have these goTennas, it's a little teeny thing that just sticks inside on the outside of your backpack, and it allows you guys to have your own little network so you can connect. Kind of like a walkie-talkie of today.

**CHUCK:&nbsp;** That sounds a lot more practical than what I was envisioning. Alright Joe, what are your picks?

**JOE:&nbsp;** I've only got one pick today. So, I've been recently listening to an audio book called 'Black Man in a White Coat'. And it is, I don't know if it's called a memoir but it's the writings of a guy, an African American medical doctor and his experiences in the medical community with racial issues. And I really liked it. He's so far at least been fairly non-judgmental. He's just describing his experiences, not necessarily blaming anybody for things, just talking about the issues and his direct experiences with them and larger systemic things when it comes to health in relationship to race issues. And I really enjoyed the book too and it opened up my eyes to a lot of things. So, if you're interested in something like that, I highly, highly recommend 'Black Man in a White Coat'.

**CHUCK:&nbsp;** Alright. Lukas, what are your picks?

**LUKAS:&nbsp;** I have two picks this week. My first pick is, I mentioned it earlier, Sitespeed.io, Gulp plugin. I recommend if you care about performance at all, super easy to hook up, super easy to run, and gives really nice metrics and information about how performant your site is based on some industry best practices.

My second pick and I'm contemplating about how much I'm going to share here, I recently read a book called 'The Power of Vulnerability' by Brené Brown. And safe to say that it's absolutely going to change your life. It did change my life and she just talks about really how people, when they base their actions out of shame, how it affects their behavior and ways [too] to tackle that. And [is] a content creator and somebody who is dedicated really my entire career to producing content, helping people, I wrestle with that. So, every time I go to publish a blog post or release a video or announce a workshop, I kind of wrestle with that internal dialog. And [inaudible] Brené is amazing. Just super funny dialog. Really, really great book, and I recommend that everybody read it. And it was a bit emotional for me but I think everybody deals with behavior that comes from a place of shame, scarcity. And I think it really [inaudible] some of the things that she had to say and share.

**CHUCK:&nbsp;** Cool. I've just got one pick. It's kind of…

**SEAN:&nbsp;** [Pretty good].

**CHUCK:&nbsp;** What was that?

**SEAN:&nbsp;** It sounds powerful.

**LUKAS:&nbsp;** Extremely. It kind of made me weepy actually. So there, I said it. I was like, do I admit it or not? But it did.

**SEAN:&nbsp;** Real men cry, man. Real men cry.

**LUKAS:&nbsp;** Yes, over ice cream in a parking lot. [Inaudible]

**CHUCK:&nbsp;** Alright. So, I'm going to throw a pick out there real fast. I got this Manfrotto LED light. I've got this, I don't know what to call it. But I put my phone in it. It goes on the top of my tripod and then I can do videos with it. And especially the last couple of days it's been rainy. It's nice to have a light that I can aim and direct. So, I got this Manfrotto LED light that goes on, it clips onto there. And it's pretty awesome so I'm going to go ahead and pick that. I'll put a link to it in the show notes. And Sean, what are your picks?

**SEAN:&nbsp;** Alright. So, I have four but I'll be really quick with them. First is a video that Pascal Precht put on. I think I'm pronouncing his name right, called 'Dependency Injection in Angular 2' that he had recorded at I think a NewTechBerlin meetup. It is probably the best description of dependency injection that I've ever heard, in Angular 1, in Angular 2. And I think the more people we get to watch that, the more people will understand just how everything hooks together. And it's really awesome. He talks about injection not only as a design pattern as an architecture as well.

And pick number two is a GitHub repo done by Uri Shaked which is angular2-iot. And the companion which is ng2-simon. So, essentially it is an Angular 2 port to the Internet of Things. It hooks up with Johnny-Five which is a JavaScript library that essentially ports to any Internet of Things device whether it be an Arduino or a Raspberry Pi. Super cool.

And then the last thing would be anybody who's interested in Webpack in Angular or wants to see 50 different ways on how to set up Angular 2, go to the AngularClass GitHub and check out any of those repositories. You're going to have a whole [bunch] of boilerplates.

**CHUCK:&nbsp;** Alright. Well, thanks for coming, Sean. If people want to follow you on Twitter or see what you're working on these days where do they go?

**SEAN:&nbsp;** On Twitter I'm @TheLarkInn except with two N's. So the Lark I-N-N. And then on Medium you can find me posting about hacking Angular 2 also @TheLarkInn. Otherwise you can check out my GitHub or find me on Stack Overflow at the same username.

**CHUCK:&nbsp;** Alright, cool. Well, thanks for coming. We'll go ahead and wrap this up and we'll catch everyone next week at ng-conf.

**_[Bandwidth for this segment is provided by CacheFly, the world’s fastest CDN. Deliver your content fast with CacheFly. Visit CacheFly.com to learn more.]_**

**_[Do you wanna have conversations with the Adventures in Angular crew and their guests? Do you want to support the show? Now you can. Go to AdventuresInAngular.com/forum and sign up today!]_**

**_[End of podcast]_**
