---
title: "A Year With node.js"
layout: post
---

For the past year I've been a part of a node.js project (my first). 
I've always been a technology-agnostic programmer, but have mainly lived in 
the Microsoft/.NET world for the past 13 years. I was eager to be a
part of a node.js project in order to learn something new and to 
understand new ways of building web apps. Here's what I think I've
learned so far.

The intent of this writing is to categorize my own thoughts at a 
high level rather than being a technical post of how things do and
don't work. 

I'll put my thoughts into the following buckets:

- node.js web frameworks
- Promises in JavaScript
- dealing with the JavaScript beast
- npm and reliance on OSS

## node.js web frameworks

I'm aware of three main node.js web frameworks that can be used to
build web apps:

- express.js
- sails.js
- mean.io

### express.js

On the <a href="//expressjs.com/">express.js web site</a> they call 
it an "unopinionated, minimalist web framework". I agree with "unopinionated"
and "minimalist" but I'm not so sure about "framework". It's so minimalist and
unopinionated that there isn't much of a guiding path for how to build a web app
with it. Nothing wrong with that though.

For medium/large apps, this example project structure is a good starting point:
<a href="https://github.com/focusaurus/express_code_structure">github.com/focusaurus/express_code_structure</a>.

The advantage of using express.js is also its disadvantage: you can use whatever
packages you want to access your data and handle the flow of requests though
the system. If you have a very custom system to build, then this might be a good 
approach for you, but if you are building a content management system or a simple
CRUD app, then you'll have to implement a lot of plumbing just to get some
basic things to work.

### sails.js

The strength of <a href="http://sailsjs.org/">sails.js</a> is real-time communication 
between browsers. It's also much more of a <em>framework</em> than express.js as it 
forces you down a particular set of conventions for objects and file organization. 
It's MVC, so you're creating models, controllers, services, and views. It's a familiar
pattern for many web devs.

What's nice about sails.js is that it has adapters for different data stores, loggers, 
and other integration points. Want to use SQL and server-rendered views? No problem.
Want to use MongoDB to create a SPA with Angular? Sure thing. sails.js is the glue
that holds it all together, providing conventions along the way.

sails.js could be used for quickly building CRUD apps with a nice side effect of
real time browser communication. User A makes a change, and User B sees the change
in real time in their browser. If I needed to be productive quickly, I'd consider
building my app with sails.js. 

### mean.io

Like sails.js <a href="http://mean.io/#!/">mean.io</a> is a <em>complete</em> and very
opinionated framework for building web apps in node.js. "MEAN" stands for Mongo, 
Express, Angular, Node. 

When I tried mean.io for the first time, I disliked its size and how rigid it was. It
depends on a very large number of npm packages and the npm install took a while. It felt like
mean.io was including so much stuff that I might not need. It's also rigid in that it 
forces you into a very specific and single way of doing things. It's opinionated, 
after all. If you don't want to use Angular or Mongo, then this isn't for you.

I want to be cautious about giving an opinion of mean.io because I haven't used it much.
I was a little turned off by it early on and haven't come back to it. The types of
apps I build (corporatey apps with a lot of system integrations) wouldn't fit mean.io well.
That being said, if you are a newcomer to full stack web development, I could see
mean.io being a good introduction to full-stack web programming.

## Promises in JavaScript

Any operation involving input/output or some network call in node.js is asynchronous. 
Consider this trivial express.js example:

```
app.get('/', function(req, res){
	res.send('Hello world!');
});
```

Above, there's one async callback function being used to handle a GET request. Instead of
hard-coding the Hello World message, let's get it from a database:

```
app.get('/', function(req, res){
	
	db.collection('message').find({ /* query criteria */ })
		.toArray(function(results){
			res.send(results[0].message);
		});
});
```

In the hypothetical example above, there are now three async callbacks - with the third one nested 
within the second, and the 2nd one nested within the first.

This is commonly referred to as <em>callback hell</em>. No sane person would write a complete
application like this. This is where JavaScript Promises come in. Promises are not new in the 
JavaScript world, but you don't get them out of the box with JavaScript (at least not in ES5, which
much of the world still uses). So how do you incorporate Promises in ES5?

On my current project we've been using the <a href="https://github.com/petkaantonov/bluebird">bluebird</a>
promise library to create promises and "promisify" JavaScript