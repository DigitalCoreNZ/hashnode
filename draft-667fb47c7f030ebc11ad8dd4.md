---
title: "1 of 2: An Introduction to Technology Stacks."
slug: 1-of-2-an-introduction-to-technology-stacks

---

Software engineers are constantly presented with new languages, new frameworks, and new libraries. Our magpie attraction to "new and shiny" trinkets is never satisfied. We actively trawl the Internet for the latest technical innovations and current programming trends. But we also have fun assembling the least amount of technology that achieves the most amount of work.

## My First Stack.

I have a soft spot for the LAMP stack, which included:

* Linux, the OS on which the servers ran,
    
* Apache, the web server,
    
* MySQL, the database server, and
    
* PHP, the programming language.
    

I adopted the LAMP stack in the early 2000s and stuck with it for ten years. Sadly, I never built anything substantial with those tools. Around the late 2000s I started using WordPress. Yes, I was pushing not-very-popular content out the door but I felt the WordPress CMS (content management system) was very restrictive. I was able to build a couple of personal plugins but the whole ecosystem felt oppressive. I was yearning to code without borders.

## Making the Switch.

2015 saw the release of PHP 7.x but, out of the corner of my eye, I also noticed the release of ES6 (later renamed ES2015, which stands for ECMAScript 2015). I had a choice: Should I stick with PHP and learn the differences between PHP 5.4 and PHP 7.x *or* switch to JavaScript and learn a whole new programming language? There was a single piece of technology that swayed my decision: Node. The idea of using a single programming language on the (client) frontend and the (server) backend seemed very attractive. So I made the jump to JavaScript. (I <s>sometimes</s> often regret my decision about switching languages.)

## The Freedom to Screw Up.

It has not been an easy five-year journey (at the time of writing). From JavaScript to Node, from Angular to React, from Vue to Nuxt, it has been a constant learning experience with occasional bouts of code. It may sound like I'm complaining but I am an old man and it is my prerogative to rail against the world.

## Other Stacks.

The original LAMP stack would use PHP to access the database. Therefore, PHP could run CRUD operations on MySQL: CREATE, READ, UPDATE, and DELETE. Looking at the whole stack, I can see that:

* The frontend used HTML pages as templates,
    
* The middleware used PHP statements as business logic,
    
* The backend used MySQL as storage, and
    
* Everything ran on Linux.
    

In the late 2000s, at the same time Node was released, another technology hit the developer community: Express. The tag team of Node and Express would eventually topple the dominance of LAMP stack. Node, as a server, would focus on responding to requests for web pages. Express, as a web framework, would focus on providing business logic. Together, these two technologies would perform the same operations as Apache and PHP.

Node and Express would be the foundation on which the next generation of stack solutions were built.

We have the MEAN stack (MongoDB, Express, Angular, Node), the MERN stack (MongoDB, Express, React, Node), the MEVN stack (MongoDB, Express, Vue, Node), and the JAMstack (JavaScript, APIs, Markup). These are all full stack solutions. Each element in a stack performs a specific task. For instance, MEVN uses:

* MongoDB as the database server,
    
* Express as the web framework,
    
* Vue as the frontend framework, and
    
* Node as the backend server.
    

Grouping these technologies together provides a programmer with a fully-rounded DX (developer experience). A technology stack provides a solo developer - like myself - with a DX that successfully emulates the original LAMP stack, except the PHP language gets replaced with ES6 (JavaScript) and Apache functionality is taken over by Node and Express.

## Stack Elements.

A typical stack brings together a number of technologies. Each technology has a specific task. These tasks work collectively to provide a consolidated DX. For example, when the MEVN stack receives a request from a browser:

* Node, the backend server, does two things: requests resources from Vue, and and responds by providing the browser with the results,
    
* Vue, the frontend framework, does two things: requests resources from Express, and responds by providing Node with the results,
    
* Express, the web framework, does two things: requests resources from MongoDB, and responds by providing Vue with the results, and
    
* MongoDB, a document database management system, does two things: queries the database(s) for records, and responds by providing Express with the results.
    

Let's have a look at how the web server, frontend framework, web framework, and database work together in a classic, client-server model.

## Dynamic Website using a Client-Server Model.

When a client - the user's browser - visits a dynamic website, the backend server returns a UI (user interface) and interaction layer that is built with a template from the frontend framework. This is how a typical result is generated:

* The browser sends a request for a web page to a backend server (e.g. Node)
    
* Node accepts the request from the browser along with any query strings,
    
* Node sends a request for the required page to the frontend server (e.g. React),
    
* React accepts the request from Node,
    
* React finds the needed template that uses the query strings,
    
* React sends a request for the required data to the web framework (e.g. Express),
    
* Express accepts the request from React,
    
* Express finds the route
    
* Express sends a request for the records to the database (e.g. MySQL),
    
* MySQL accepts the request from Express,
    
* MySQL runs a query to find the records,
    
* When found, the query returns the records to MySQL,
    
* MySQL responds to Express by returning the records,
    
* Express accepts the response from MySQL,
    
* Express responds to Node by returning the records,
    
* Node accepts the response from Express,
    
* Node builds the records into an HTML template designed by the frontend framework (e.g. React),
    
* Node responds to the browser by sending a freshly built HTML file,
    
* The browser accepts the response from Node, and
    
* The browser renders the HTML file.
    

This example describes a typical request-response scenario that is used by the client-server model. But now we now have an alternative way of doing things.

## Dynamic Website using a Single-Page App.

There is absolutely *nothing wrong* with building dynamic websites using the client-server model. So, what makes SPAs different to the client-server model?

A device - like a mobile phone, for instance - downloads an SPA from the backend server. The first-page load time may take awhile, but code-splitting helps to speed things up. Once the SPA is loaded, the JavaScript code within the SPA can request network resources that make up the different views of the SPA *without needing the backend server or a web framework*. The JavaScript code can request, and receive, networked resources as long as the SPA is authorised to use the API (application programming interface) that accesses, and then returns, those resources.

Another difference is that SPA frameworks like Vue and React decouple the frontend from the backend.

## Search Engines.

Search engines don't like dynamic websites, regardless of how they're built (client-server model or SPA). A dynamic website is built with code - JavaScript, PHP, Python, etc. - but search engines are looking for meta tags that are typically found in the HEAD section of HTML (hypertext markup language) pages. When a search engine scans a dynamic page for meta tags, the site will build that page. By the time the page is built, however, the search engine has already decided the page doesn't exist and moves on. Dynamic pages load really fast for humans - usually within a second or two - but they don't build fast enough for a search engine.

Luckily for us, there is a clever solution: Static pages.

## The Return of Static Pages.

I remember hand-coding HTML pages with a simple text editor back in the 1990's. That was my first exposure to online publishing and static pages. I also added CGI scripts to my pages that counted the number of visitors I had (the only time the counter changed was when I visited the page to see if the counter had changed.) Then I moved on to other editors like Netscape Composer, Microsoft FrontPage, Macromedia Dreamweaver, Sublime Text, and VS Code. Now static pages are back, like an old friend. Or a recurring STD.

The idea is simple: Take all the content that makes up a dynamic SPA, render that content as HTML pages, and host those pages on a CDN (content delivery network). It turns out that static pages load even faster than an SPA can render. That's amazingly fast. Another advantage - which is also a disadvantage that I will cover in a moment - is a lack of server-side rendering. Remember, the content is rendered first, and then the CDN hosts the resulting HTML pages. Yet a third advantage is that, with a bit of tweaking to each view, relevant meta tags for each HTML page are now available to every search engine.

But every solution comes with it's own problems.

## The End of Dynamic Content?

The main problem with a CDN is the lack of server-side rendering support. How can we access the content in a database - like SPA's - while supplying meta tags for search engines - like static pages?

Stay tuned for the next article where I look into a proposed solution using actual technologies. Wheee, down the rabbit hole we go...