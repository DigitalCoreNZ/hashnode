---
title: "2 of 2: Welcome to the FAGANN Stack."
slug: 2-of-2-welcome-to-the-fagann-stack

---

In a previous article, we had a quick look at the elements that make up a technology stack. Then we had a peek at dynamic websites that are built using the client-server model and single page apps. Then we compared dynamic pages to static pages. And finally I ended the article by wondering if dynamic content - à la single page apps - is still possible in a world of static pages? This write-up hopes to answer that question.

## A Stack by Any Other Name... is Still a Stack.

David Axmark and Monty Widenius, two of the co-founders of the MySQL relational database, had coined an awesome term around 2000 or 2001 that described the open source movement at the time: LAMP stack (Linux, Apache, MySQL, PHP). Staffers at O'Reilly Media, the publishers of those *wonderful* technology books, embraced the LAMP stack term and evangelized what LAMP meant to the broader developer community.

Twenty years later, we still refer to a collection network-enabling services as a stack. There is the original LAMP stack, the MEAN stack, the MERN stack, the MEVN stack, the JAMstack, and now the FAGANN stack.

## What is the FAGANN Stack?

The FAGANN stack is a technical implementation of the JAMstack. We will sneak a glimpse at JAMstack later in this guide. It is fair to say that the FAGANN stack is a typical collection of web development technologies and services. FAGANN stands for:

* FaunaDB, a serverless database,
    
* Axios, a promise-based HTTP<sup>*</sup> client,
    
* GraphQL, a standard & API<sup>*</sup> architecture,
    
* AWS<sup>*</sup> Lambda, a serverless compute service,
    
* Nuxt, a JavaScript-based frontend framework, and
    
* Netlify, a serverless web host & CDN<sup>*</sup> for static sites.
    

The acronyms<sup>*</sup> used in the previous list includes:

* HTTP: hypertext transfer protocol,
    
* API: application programming interface,
    
* AWS: Amazon web services, and
    
* CDN: content delivery network.
    

There is also a collection of support technologies for the FAGANN stack, including:

* VS Code, a code editor,
    
* Git, a version control system,
    
* GitHub, a remote code repository,
    
* Node, an open-source server environment,
    
* NPM, a package manager for Node modules,
    
* JavaScript, a popular programming language,
    
* CSS3, the design language for presenting web pages, and
    
* HTML5, the markup language for creating web pages.
    

The following sections will provide a shallow skim, the complete opposite of a deep dive, into the technologies that make up the FAGANN stack.

### [#](https://digitalcore.co.nz/blog/2020-06-16-welcome-to-the-fagann-stack-2-of-2.html#a-toe-dip-into-faunadb) A Toe Dip into FaunaDB.

[FaunaDB](https://fauna.com/) is a serverless, distributed, ACID-compliant, graph-enabled database. It features native support for it's own dialect of GraphQL and ships with a native API (application programming interface) called FQL (Fauna query language) that is used to query FaunaDB.

FaunaDB also comes with a generous amount of free resources, more than enough to build and test your latest creations. When you start running out of free resources - because your latest app is a game-changer that everyone uses *everyday* - then the FaunaDB pricing structure is simple (you pay for what you use) and competitive.

Other graph databases include [Neo4j](https://neo4j.com/) and [Dgraph](https://dgraph.io/).

There is also a utility called FaunaDB Shell:

```bash
$ npm install -g fauna-shell
```

Mac users get to use Homebrew:

```bash
$ brew install fauna-shell
```

> NOTE: FaunaDB Shell does not currently support GitHub or Netlify logins so you may need to [follow these steps](https://docs.fauna.com/fauna/current/start/cloud-github)

> if you signed up to FaunaDB using your GitHub or Netlify credentials.

Check out the [Quick start with FaunaDB](https://docs.fauna.com/fauna/current/start/cloud.html) page for an introduction to the FaunaDB Shell.

### A Puddle Splash into Axios.

[Axios](https://github.com/axios/axios) is a popular, lightweight, promise-based HTTP client for frontend browsers and backend Node. It sports an easy-to-use API that processes fetch, and save, data requests. Other features include promises, browser independence, 4xx and 5xx error code promise rejection, cookie returns, and callback functions for `onUploadProgress` and `onDownloadProgress` that can display the percentage complete in your apps' UI (user interface).

Alternatives to Axios are the promise-based [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) that is built into modern browsers, and the battle-tested [XMLHttpRequest (XHR)](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) which dates back to 2000-2002.

> NOTE: In 2005, XMLHttpRequest would become one of the corner stones of an Adaptive Path article written by Jesse James Garrett called "[Ajax: A New Approach to Web Applications](https://courses.cs.washington.edu/courses/cse490h/07sp/readings/ajax_adaptive_path.pdf). Ajax, a term coined by Garrett, stands for "Asynchronous JavaScript and XML". The XML (eXtensible Markup Language) has effectively been replaced with JSON (JavaScript Object Notation) for most applications.

### A Timid Dip into GraphQL.

[GraphQL](https://graphql.org/) is a standards specification as well as an API architecture. The [FaunaDB database](https://fauna.com/) implements a custom dialect of GraphQL. Read the [FaunaDB documentation](https://docs.fauna.com/fauna/current/start/graphql) to learn how to use their dialect of GraphQL.

### A Wary Paddle into AWS Lambda.

[AWS Lambda](https://aws.amazon.com/lambda/) is a serverless compute service. The [Netlify web host](https://www.netlify.com/) implements a custom version of AWS Lambda. Read the [Netlify documentation](https://www.netlify.com/products/functions/) to learn how to use their version of AWS Lambda.

### A Shallow Wade into Nuxt.

[Nuxt](https://nuxtjs.org/) is a frontend framework that runs on top of [Vue](https://vuejs.org/), another frontend framework. The number one feature that Nuxt has over Vue is Universal mode, a way of building SPA's (single page apps) with support for SSR (server-side rendering). Other features include easy-to-render static pages, easy-to-forget automatic code splitting, easy-to-begin starter templates similar to those offered by Vue CLI (command line interface), an easy-to-use project structure, easy-to-build routes, easy-to-setup route transitions, easy-to-write single file components, easy-to-compile ES2015+ JavaScript thanks to Babel, easy-to-package code thanks to Webpack, an easy-to-run development server (`$ npm run dev`), and an easy-to-follow [Nuxt Community](https://github.com/nuxt-community).

Other leading frontend frameworks include [React](https://reactjs.org/) and [Angular](https://angular.io/) that I found not-as-easy to learn.

Scaffolding a Nuxt app is as simple as running an npx command in a terminal:

```bash
$ npx create-nuxt-app my-first-nuxt-app
```

After a moment of downloading, the CLI starts firing questions at you. After answering all the questions, and sacrificing your first-born to Complr the god of code, a sub directory called 'my-first-nuxt-app' appears and starts filling up with the files and folders that make up your new app.

There are a couple of caveats:

* an Internet connection is required for this process to work, and
    
* NPM version 5.2 or later needs to be installed, or `npx` can be installed separately (`$ sudo npm install -g npx`).
    

### A Bathtub Slosh into Netlify.

[Netlify](https://www.netlify.com/) is a modern platform for hosting static websites on a CDN (content delivery network). By their very nature, CDN's are great for delivering content very quickly. But that's just the begining. When you make changes to your site and push those changes to a remote git repository (GitHub, Bitbucket, or GitLab), Netlify pulls those changes and rebuilds your site from that git commit. Each build is atomic as well, which makes it easy to roll back your site to a previous git commit. The free plan - which supports a single user with additional users at $15/month - comes with:

* 1 concurrent build,
    
* 100 GB bandwidth/month,
    
* 300 build minutes/month,
    
* continuous deployment, and
    
* access to paid add-ons.
    

These features are more than generous for developing and testing your next killer app, hosting personal projects, building hobby sites, or running experiments. Other features include:

* quick builds (a build should only take minutes),
    
* preview links for every build (re: atomic builds),
    
* Netlify subdomains (yoursitename.netlify.com),
    
* custom domains (yoursitename.com),
    
* custom subdomains (using Netlify DNS),
    
* snippet injection (for analytics, meta tags, etc.),
    
* A/B split testing (from different git branches),
    
* outgoing notifications (for email, Slack, and other outgoing webhooks),
    
* Netlify serverless functions (which are actually AWS serverless Lambda functions),
    
* and many other features.
    

Some of these features are fee-based when you exceed your free allowance but the monthly fees are very reasonable because you only pay for what you use.

Netlify also has a CLI called... wait for it... [Netlify CLI](https://docs.netlify.com/cli/get-started/#installation):

```bash
$ npm install -g netlify-cli
```

There's also a local development server, that's currently in beta, called [Netlify Dev](https://docs.netlify.com/cli/get-started/#netlify-dev). After installing Netlify CLI, you can run a local development server:

```bash
$ netlify dev
```

And you can use Netlify Lambda if you want to work with AWS [serverless functions](https://docs.netlify.com/functions/overview/#manage-your-serverless-functions):

```bash
$ npm install netlify-lambda
```

Netlify even has an open-source, Git-based, headless CMS (content management system) called, you guessed it, [Netlify CMS](https://www.netlifycms.org/).

### What Eappened to Express?

[Express](https://expressjs.com/) is a fast, unopinionated, minimalist, routing and middleware framework for Node. You can use [Express in combination with Netlify](https://www.netlify.com/blog/2018/09/13/how-to-run-express.js-apps-with-netlify-functions/) (Lambda) functions with the help of a library called `serverless-http`. You get to use your favourite Express patterns and any existing middleware. However, there are resource limitations and 'stateless' cache issues. Besides, backend servers don't run on CDN's and defeats the point of JAMstack. We'll look at JAMstack in a moment.

Also, FAGANNE stack sounds like a pasta dish. Can't be havin' any 'at foreign muck at me age. It goes right fru me, it does. Causes a right mess.

## The world of JAMstack.

JAMstack describes a modern web development architecture based on client-side \[J\]avaScript, reusable \[A\]PIs (application programming interfaces), and prebuilt \[M\]arkup. Pre-rendering a site into a collection of static assets is one of the core principles behind JAMstack.

Modern static websites are similar to, yet completely different from, the static websites of the 1990's. A lot of changes have occurred over the intervening 25+ years. The Internet is much, MUCH bigger. The client (browser) can ask for resources directly. Programming languages have evolved, as have our programming tools. API's are exploding across the network. Social networking has brought people together, while simultaneously isolating everyone. And the classic sci-fi trope of making video phone calls from mobile devices is a reality. Yet some things remain the same. We battle against the stateless nature of the web on a daily basis. Spam continues its' relentless deluge. And porn still lacks any coherent story lines.

So here is my question: Is it possible to use dynamic content in a world of static pages?

An article from [CSS-Tricks](https://css-tricks.com/static-first-pre-generated-jamstack-sites-with-serverless-rendering-as-a-fallback/) that was penned by [Phil Hawksworth](https://css-tricks.com/author/philhawksworth/) back in 2019 seems to suggest that, with the help of serverless functions, dynamic content is a possibility.

You can also read a FREE ebook called [Modern Web Development on the JAMstack](https://www.netlify.com/oreilly-jamstack/) by Mathias Biilmann, technical co-founder and CEO of Netlify - and the guy who coined the JAMstack term, and Phil Hawksworth, principal developer advocate at Netlify, to find out if dynamic content can be squeezed out of a static page.

Or you can read the next section, instead.

Notice all the serverless services that make up FAGANN stack? FaunaDB, AWS Lambda, and Netlify are all serverless services. It's not that these services aren't running on servers. They are. It just means that provisioning and maintaining those servers is none of our concern. Which is fine by me. I grew tired of spinning up servers 15 years ago.

Now, back to the question at hand.

## Can Static Pages Show Dynamic Content?

Yes.

## How?

I'm not sure. It looks like JAMstack may have the answer so I plan to find out how deep the rabbit hole goes. (Yes, Neo. You are THE ONE.) I'm working on a new dev guide series called the Login dev guides where I'll use the FAGANN stack - a total rip-off of the JAMstack - to:

* scaffold a Nuxt app,
    
* deploy the app to GitHub,
    
* pull the app into Netlify,
    
* build a modal with Vuetify,
    
* authenticate and authorize with Nuxt and FaunaDB, and
    
* login to a user account from the frontend.
    

Later, I will use the Login dev guides as the foundation for the CRUD dev guides. I will use the CRUD dev guides to:

* build a CRUD-based appliance with Nuxt, and
    
* use the CRUD-based appliance from the frontend.
    

The Login dev guides will be released at the end of July 2020, so stay tuned for those guides to drop.

Who knows? If the Login dev guides work out I might start working on a FAGANN-centric website.