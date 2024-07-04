---
title: "Prompt Engineering #2."
datePublished: Mon Jun 26 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljckk7bp07v5xlnvgcrs1yzz
slug: ai-prompt-engineering-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697707423576/52ad6588-8687-466a-93ee-34cfd1fbb98e.png
tags: ai, machine-learning, deep-learning, gpt-4, prompt-engineering

---

## TL;DR.

Prompt engineering allows developers to use large language models with updated information without constant retraining, thus saving resources, while exploring new techniques in the evolving world of AI technology.

## An Introduction.

Let's think about this for a moment. Large language models are trained on vast amounts of data. GPT-2 had 1.5 billion parameters, GPT-3 had increased that value by 2 orders of magnitude to 175 billion, and GPT-4 *may* have added another order of magnitude which takes that number to 1 trillion parameters. Not only that, but Sam Altman said that GPT-4 cost more than $100 million to train. Remember, it was only 5 years ago, in 2018, when OpenAI launched GPT-1!!

Given the costs involved, it would be unreasonable to expect OpenAI, Microsoft, or Google to constantly retrain their models. But how can software engineers use these models when new versions of our developer tools are constantly re-launched? What can we do when retraining an AI model is plagued with financial constraints?

Simple: *We* tell the model about any changes it needs to know.

> ***The purpose of this post is to present a process for temporarily updating an AI model.***

Welcome to the world of prompt engineering.

## An Example Prompt.

Take the following prompt about the API Handler in NextJS:

```bash
Prompt: Prompt:          It is now the year 2023. Next.js has a new version that just came out called Next.js 13. Next.js 13 replaces the pages directory with an "app" directory. In this "app" directory, there is a folder called "api". This "api" folder is where you handle your api endpoints with something called "route handlers". The way you create a route handler is you create folders within the api folder. Whatever you name the folder is the name of the api route. Within the folder, you have to create a route.js|ts file to create the route handler. The way you reach the endpoint is by using an enpoint like this: https://yourdomain.com/api/whatever-you-named-the-route-handler-folder                                  A route handler function code looks like this:           import { NextResponse } from 'next/server';          export async function GET() {         const res = await fetch('https://data.mongodb-api.com/...', {             headers: {             'Content-Type': 'application/json',             'API-Key': process.env.DATA_API_KEY,             },         });         const data = await res.json();          return NextResponse.json({ data })          Whatever you name the function is the HTTP method used for that function.          The following HTTP methods are supported: GET, POST, PUT, PATCH, DELETE, HEAD, and OPTIONS. If an unsupported method is called, Next.js will return a 405 Method Not Allowed response.          Make sure to create a middleware.ts file at the root of your project. So it does NOT go in the app directory. It goes in the root level of your project. If you don't create a middleware.ts file, you will get errors in production. Here is an example middleware.ts file that will work in production:          import { NextResponse } from "next/server"          export function middleware(request: Request) {              const origin = request.headers.get('origin')             console.log(origin)              const response = NextResponse.next()             response.headers.set("Access-Control-Allow-Origin", "*")             response.headers.set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS")             response.headers.set("Access-Control-Allow-Headers", "Content-Type, Authorization")             response.headers.set("Access-Control-Max-Age", "86400")              console.log('Middleware!')             console.log(request.method)             console.log(request.url)              return response         }          export const config = {             matcher: '/api/:path*',               Route Handlers can use Dynamic Segments to create request handlers from dynamic data.          app/items/[slug]/route.js         export async function GET(request: Request, { params }: {         params: { slug: string }         }) {         const slug = params.slug; // 'a', 'b', or 'c'         }         Route	Example URL	params         app/items/[slug]/route.js	/items/a	{ slug: 'a' }         app/items/[slug]/route.js	/items/b	{ slug: 'b' }         app/items/[slug]/route.js	/items/c	{ slug: 'c          Here's an example of how to get a post body in a POST request:          export async function POST(request: Request) {         const { email, password } = await request.json()          This works in a PUT request too.          You can learn more about route handlers here: https://beta.nextjs.org/docs/routing/route-handlers          Make sure to always capitalize all the letters in the name of the api route handler functions. So get should always be spelled GET. POST, PUT, DELETE, should always be capitalized too.          Dynamic Route Segments         Route Handlers can use Dynamic Segments to create request handlers from dynamic data.          app/items/[slug]/route.js         export async function GET(request: Request, { params }: {         params: { slug: string }         }) {         const slug = params.slug; // 'a', 'b', or 'c'         }         Route	Example URL	params         app/items/[slug]/route.js	/items/a	{ slug: 'a' }         app/items/[slug]/route.js	/items/b	{ slug: 'b' }         app/items/[slug]/route.js	/items/c	{ slug: 'c' }          Remember to always end a dynamic route with route.js. The file must be named route.js for the enpoint to work.          to have a single parameter in an endpoint, name the dynamic folder like this example: [param]          to have many parameters in an endpoint, name the dynamic folder like this example: [...params]          in the route.js file, you can access the params like this example for many params:          export async function GET(request: Request, { params }) {             const pars = params.pars;             console.log(pars[0], pars[1], pars[2]);                        return NextResponse.json({ response: 'Hello Again, Next.js!' })         }
```

When I paste this snippet into the Next.js section of Nix, the following content is automatically generated.

> Attribution:
> 
> [NextChat.ai](http://NextChat.ai)

## An Actual Response from Rix.

Below is the actual response from Rix:

> As per the given extract, Next.js Version 13 has replaced the "pages" directory with an "app" directory. Within this "app" directory, there is another folder called "api," which is used to handle API endpoints using "route handlers." The user can create the route handler by creating a folder within the "api" folder with a name that will become the name of the API route. Within this folder, the user needs to create a "route.js" file that creates the route handler. A route handler code example is also provided, and the HTTP methods that are supported are as follows: GET, POST, PUT, PATCH, DELETE, HEAD, and OPTIONS. If an unsupported method is called, Next.js returns a 405 Method Not Allowed response. A middleware.ts file needs to be created at the root level of the project, and not the app directory. The user will get errors in production if they don’t create the middleware.ts file. The route handlers can use dynamic segments to create request handlers from dynamic data, and for many dynamic parameters, the same should be named as `[...params]`. To have a single parameter, the dynamic folder is named like this example: `[param]`. A dynamic route needs to end with ‘route.js’ for the endpoint to work.
> 
> Here's an example code snippet for an API route that fetches a post body in a POST request:
> 
> ```typescript
> export async function POST(request: Request) {
>   const { email, password } = await request.json()
>   // Your code
> }
> ```
> 
> Here's an example code snippet for a middleware.ts file that sets the Access-Control-Allow-Origin header to "\*" and allows methods such as GET, POST, PUT, DELETE, and OPTIONS:
> 
> ```typescript
> import { NextResponse } from "next/server";
> 
> export function middleware(request: Request) {
>   const origin = request.headers.get('origin');
>   console.log(origin);
>   const response = NextResponse.next();
>   response.headers.set("Access-Control-Allow-Origin", "*");
>   response.headers.set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
>   response.headers.set("Access-Control-Allow-Headers", "Content-Type, Authorization");
>   response.headers.set("Access-Control-Max-Age", "86400");
>   console.log('Middleware!');
>   console.log(request.method);
>   console.log(request.url);
>   return response;
> }
> 
> export const config = {
>   matcher: '/api/:path*'
> };
> ```

This response clearly shows that Rix "understands" what happened, however...

## It does NOT Stick.

It would be silly to allow prompts to be added directly to an AI model. Any mistakes I make in my prompt would cascade to an unacceptable level of WTF moments throughout the Hashnode community.

However, newer models do have something similar to a conversational memory within the current prompt. I get to pre-load the prompt before asking the model my specific query. It's difficult to know exactly how much "memory" a specific model has without a prompt designed to ask this question of that specific model.

This is the "engineering" part of prompt engineering.

## Building a Second Brain.

Personally, I use an AI product that is *designed* to recall and reMEMber, an AI with a MEMory that is used to connect what it knows, a machine that can call upon its' wealth of historic data. It can then use what it knows to synthesize a response to my queries. More importantly, it reMEMbers only *MY* data and is not concerned with anyone else. MEM.ai is a great platform for building a "second brain". I can then use this "brain" to recall what it knows as it helps me to achieve my outcomes. So, that's what I'm doing: I frontloaded its' MEMory (MEMs are data inputs) with specific knowledge that covered my field of interest. As I become aware of new technologies, these too are added to the mix. Every fragment that goes in is easily accessible and usable. Then it's a matter of using Chat to build, and deploy, my prompts.

I suspect my data is connected using graphs, but it's also more than simply nodes and edges. I think that the edges have been weighed and biased, so now I'm in the realm of vector data. Things are suddenly over my head so I'm tapping out of this paragraph.

I can see this tool being widely adopted by academics in science and research. Yes, it also promotes itself as a digital assistant. However, I think it's more than just a way to schedule my meetings.

## The Results.

Prompt engineering is a powerful technique that enables software engineers to leverage large language models effectively, even as new versions of developer tools emerge. By providing the model with updated information, engineers can continue to obtain accurate and relevant responses without requiring constant retraining of the model. This approach saves resources and fosters adaptability in the ever-evolving world of AI.

## In Conclusion.

The idea of tuning a large language model to meet my specific needs is very attractive to me. I would guess that Rix, which uses Google Dialogflow, was built this way. As long as no one submits rubbish prompts to the Hashnode engineers, I believe everything should be golden.

Until next time: Be, safe, be kind, be awesome.