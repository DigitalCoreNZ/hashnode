---
title: "aiChat: The VocalCue Project."
datePublished: Mon Dec 04 2023 09:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clpqokvha00030alc9hiq880v
slug: aichat-the-vocalcue-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710541472104/a50fe04e-cbef-45d3-883c-4a499f678d52.png
tags: ai, machine-learning, chatbot, deep-learning, chatgpt

---

## TL;DR.

This is a chat with MEM.ai.

VocalCue will be a voice-enabled teleprompter that enhances video content creation by using dynamic content delivery and keyword voice commands.

> **Attributions:**
> 
> [https://mem.ai/](https://mem.ai/).

## An Introduction.

VocalCue is an innovative cutting-edge project that will harness the power of Mojo, DeepSpeech, and WASM to create a hands-free teleprompter.

The teleprompter will dynamically present its' content and respond to keyword voice commands. My marketing strategies will include content creation and influencer marketing that directly targets video content creators.

> The purpose of this post is to use Mem.ai to create a first-pass outline of the VocalCue project.

## The Big Picture.

I accidentally found that the Mem.ai chatbot is very good at drilling down into project details. I thought to myself "I could probably use this feature to create outlines for my projects."

The following is an unedited example of using a chatbot to generate the first pass of a project outline. The resulting "conversation" needs editing (i.e. adding some missing details) but this process allows me to consider further questions while providing extra details about my 12S projects.

## Prerequisites.

* None.
    

## The Chat.

What are the advantages of using Mojo for AI development?

> Hmm, I'm afraid I don't have any specific information on the advantages of using Mojo for AI development in your knowledge base. However, based on general knowledge, Mojo is a framework that can be used for developing and deploying production-grade machine learning models. It's known for its scalability, ease of use, and ability to handle large datasets.
> 
> But, as with any tool, its effectiveness can depend on the specific use case and the expertise of the team using it. Are you considering using Mojo for a particular project? If so, I could help you think through the potential benefits and drawbacks given your specific circumstances.

Yes, I am thinking of adopting Mojo.

> That's great to hear, Brian! Adopting a new framework like Mojo can be a game-changer. It's known for its scalability and ability to handle large datasets, which can be a significant advantage for AI development.
> 
> However, it's also important to consider the learning curve and the compatibility with your existing tech stack. You might want to think about:
> 
> * How well does Mojo integrate with your current tools and systems?
>     
> * What kind of support and community does Mojo have? Can you easily find solutions or advice when you encounter issues?
>     
> * How much time and resources are you willing to invest in learning and implementing Mojo?
>     
> 
> Remember, the best tool is the one that fits your needs and context the best. So, what's driving your interest in Mojo? Are there specific features or capabilities that caught your eye?

My interest in the Mojo programming language revolves around using it with the Modular AI Engine.

> Ah, I see. Using Mojo with the Modular AI Engine could indeed offer some compelling benefits. The Modular AI Engine is designed to allow for the integration of various AI models and algorithms, and Mojo could potentially provide a robust and scalable framework for developing these models.
> 
> Here are a few potential advantages:
> 
> 1. **Scalability**: Mojo is known for its ability to handle large datasets, which could be crucial when working with complex AI models that require substantial amounts of data.
>     
> 2. **Flexibility**: The Modular AI Engine's design could allow you to easily integrate Mojo-developed models with other components of your system.
>     
> 3. **Efficiency**: Using Mojo could potentially streamline the process of developing, testing, and deploying AI models within the Modular AI Engine.
>     
> 
> However, as with any technology decision, it's important to consider the potential challenges as well. For instance, you'll want to consider the learning curve associated with Mojo, the compatibility with your existing tech stack, and the availability of support and resources.
> 
> Given your role in IT & Engineering, I'm sure you're well-equipped to make this assessment. Is there a specific project or problem you're hoping to tackle with Mojo and the Modular AI Engine?

I want to develop a voice-enabled teleprompter.

> Ah, a voice-enabled teleprompter, that's an exciting project! Using Mojo with the Modular AI Engine could be a great fit for this. Here's why:
> 
> 1. **Real-time processing**: Mojo's ability to handle large datasets could be beneficial for processing and transcribing speech in real time.
>     
> 2. **Integration**: The Modular AI Engine's flexibility could allow you to integrate various components needed for a voice-enabled teleprompter, such as speech recognition, natural language processing, and real-time text display.
>     
> 3. **Customization**: Using Mojo could potentially allow you to customize the teleprompter's behavior to better fit your users' needs.
>     
> 
> However, developing a voice-enabled teleprompter can be a complex task. You'll need to consider factors like accuracy of speech recognition, latency, and user interface design.
> 
> Have you thought about how you'll handle these challenges? For example, what strategies do you have in mind for improving speech recognition accuracy and reducing latency?

Yes, I have.

> Great! It would be helpful to know more about the strategies you're considering. For instance, are you thinking about using any specific speech recognition APIs or libraries? Or perhaps you're considering a custom solution?
> 
> Also, how are you planning to handle latency issues? Are you considering any specific techniques or technologies to ensure real-time performance?
> 
> The more details you can provide, the better I can assist you in refining your approach.

I plan to use an open-source embedded Speech-to-Text engine called DeepSpeech. Latency issues will be solved by training a user's voice online, and then generating a custom WASM package that contains the AI agent for the user's account.

> That sounds like a solid plan, Brian. DeepSpeech is a great choice for an open-source Speech-to-Text engine, and training a user's voice online should help improve the accuracy of the transcription.
> 
> Generating a custom WASM package for each user's account is a clever way to handle latency issues. By running the AI agent directly in the user's browser, you can reduce the need for round-trip communication with a server, which should help keep latency to a minimum.
> 
> Just a thought, have you considered how you'll handle potential challenges with this approach? For example, how will you ensure the privacy and security of the user's voice data during the online training process? And how will you manage the potentially large size of the WASM packages, especially for users with limited bandwidth or storage capacity?

Privacy and security of the user's voice data can be maintained by using the same WASM package to generate the unique voice profile. The WASM package will be small because it only does two things: It creates a voice profile and it scrolls the teleprompter as the script is spoken.

> That's a smart approach, Brian. Using the WASM package to generate the unique voice profile can indeed help maintain the privacy and security of the user's voice data. And keeping the WASM package focused on just creating a voice profile and scrolling the teleprompter should help keep its size manageable.
> 
> Given your approach, it seems like you've got a good handle on the technical aspects of this project. I'm curious, though, have you thought about the user experience side of things? For instance, how will users train the system with their voice? And how will they interact with the teleprompter as they're speaking?

The user will require a smartphone to act as the teleprompting device, which can be mounted to a teleprompt holder with beam-split glass, like the Feelworld TP10. They can load their script on the phone and use a command phrase (similar to "Hey Google") to issue control instructions, for instance: "Teleprompter, go back two lines", or "Teleprompter, go forward one line."

> That's a neat setup, Brian! Using a smartphone as a teleprompting device is a practical choice, and the command phrase approach for controlling the teleprompter is user-friendly.
> 
> The Feelworld TP10 is a good choice for a teleprompt holder with beam-split glass. It's portable, easy to set up, and compatible with most smartphones and mini tablets.
> 
> As for the command phrases, it's important to ensure they're intuitive and easy to remember. The examples you provided ("Teleprompter, go back two lines", "Teleprompter, go forward one line") are straightforward and should be easy for users to pick up.
> 
> One thing to consider is how the system will handle potential speech recognition errors. For instance, what happens if the system misinterprets a command? Have you thought about implementing a system for error correction or feedback?

To reduce the chances of speech recognition errors, there will be a limit of five voice commands: Teleprompter Start, Teleprompter Stop, Teleprompter go back (number) lines, Teleprompter go forward (number) lines, Teleprompter reset. If the Teleprompter command phrase is garbled or unknown, the phone will ask for the command again, with examples.

> That's a solid strategy, Brian. Limiting the number of voice commands can indeed help reduce the chances of speech recognition errors. And having the phone ask for the command again, with examples, is a good way to handle situations where the command phrase is garbled or unknown.
> 
> This approach should make the system more robust and user-friendly. It also provides users with immediate feedback, which can help them learn how to interact with the system more effectively.
> 
> Just a thought, but have you considered how you might handle situations where the system repeatedly fails to understand a command? For example, you might want to consider implementing a fallback option, such as manual control, for these cases.

Manual override occurs through a simple touch of the screen. Looking through the beam-split glass to the reflected phone screen will show the five commands as buttons, and a number pad. The user can also remove the phone from the teleprompter holder and exit the prompter mode to access more detailed features, like the script editor, font size, font colour, background colour, etc.

> That's a well-rounded plan, Brian. Having a manual override through a simple touch of the screen is a great fallback option. It ensures that users can still control the teleprompter even if voice commands aren't working for some reason.
> 
> The on-screen buttons and number pad will provide a visual guide for users, making it easier for them to issue commands. And the ability to access more detailed features like the script editor, font size, font colour, and background colour by removing the phone from the teleprompter holder adds another layer of flexibility and customization to the user experience.
> 
> Given this setup, it seems like you've covered all the bases. Is there anything else you're considering or any other aspect you're unsure about?

No, but thank you for helping me clarify how I should begin to approach this project.

> You're welcome, Brian! It sounds like you're off to a great start. Remember, the key to a successful project is a well-thought-out plan and clear objectives. As you move forward, don't hesitate to revisit and revise your plan as needed. It's all part of the process.
> 
> So, what's the next step for you in this project? Are you going to start with the design or jump straight into coding?

I have yet to begin the first draft of my design documents. That's where I'll start.

> Great choice, Brian! Starting with a design document is a solid approach. It will help you clarify your thoughts, define the project scope, and set a clear direction for your team.
> 
> Remember, a good design document should include the needs and requirements of the system's stakeholders, a high-level system architecture, and detailed designs for each component. Also, don't forget to consider factors like scalability, maintainability, and security.
> 
> Do you have a particular structure in mind for your design document, or are you looking for some guidance on how to structure it?

I have a technical design template and a product design template.

> That's fantastic, Brian! Having a set of templates at your disposal can really streamline the process. It ensures you're not starting from scratch each time and helps maintain consistency across your projects.
> 
> When you're working on your design document, remember to tailor the templates to the specific needs of your project. Each project is unique, so don't be afraid to modify the templates as needed.
> 
> Are there any specific areas in your templates that you're unsure about or think might need some tweaking for this project?

Both templates have grown over time and now include many questions that are found in business plan templates. This is appropriate because my projects can very easily become businesses.

> That's a smart approach, Brian! Incorporating elements of a business plan into your design templates can provide a more holistic view of the project. It not only addresses the technical aspects but also considers the business potential of your projects.
> 
> This approach can help you identify potential opportunities and challenges early on, and it can also make it easier to transition the project into a business if the opportunity arises.
> 
> Are there any specific business-related questions or sections in your templates that you find particularly useful or challenging?

I find web-based projects more difficult to market to potential users, unlike real-world projects which I can easily market to real-world businesses.

> Ah, the classic challenge of marketing web-based projects. It's a different ball game compared to marketing physical products or services, isn't it?
> 
> One of the key differences is that with web-based projects, your potential user base is often much larger and more diverse. This can be both a blessing and a curse. On one hand, you have the potential to reach a global audience. On the other hand, it can be harder to identify and target the right users.
> 
> One approach could be to start by clearly defining your target audience. Who are they? What problems are they facing that your project can solve? Once you have a clear picture of your target audience, you can tailor your marketing efforts to reach them effectively.
> 
> Also, consider leveraging online marketing channels like social media, content marketing, SEO, and email marketing. These can be highly effective for reaching and engaging with your target audience.
> 
> What strategies have you tried so far for marketing your web-based projects? And how have they worked out?

In the real world, I can look at a company and say "This is your issue, this is how you fix it, and I'm the software developer who can solve your problems." My web projects, on the other hand, are built to solve my problems. The teleprompter project is a tool that will help me to produce quality videos for the web. In this case, the people who may find a use for my project are other video content creators.

> That's a great starting point, Brian. You've identified a specific audience - video content creators - who could potentially benefit from your teleprompter project.
> 
> Now, the challenge is to reach out to this audience and convince them that your tool can solve their problems. Here are a few strategies you might consider:
> 
> 1. **Content Marketing**: Create content that your target audience will find valuable. This could be blog posts, videos, or social media posts about video production tips, for example. You can subtly promote your teleprompter tool in this content.
>     
> 2. **Influencer Marketing**: Reach out to influencers in the video content creation space. If they try out your tool and like it, they might be willing to promote it to their followers.
>     
> 3. **Online Communities**: Participate in online communities where video content creators hang out. This could be forums, social media groups, or websites like Reddit. Share your knowledge and occasionally mention your tool.
>     
> 4. **Free Trials or Freemium Model**: Allow users to try your tool for free. If they find it useful, they might be willing to pay for additional features.
>     
> 5. **Partnerships**: Partner with other businesses that offer complementary products or services. They might be willing to promote your tool to their customers.
>     
> 
> Remember, marketing is a marathon, not a sprint. It might take some time to see results, but don't get discouraged. Keep experimenting with different strategies until you find what works best for you.
> 
> What do you think of these strategies? Do any of them resonate with you?

All of your suggestions are very good.

> Great to hear that, Brian! It's all about finding what resonates with you and your target audience. Remember, it's not just about getting your tool in front of people, but also about demonstrating its value. Show them how it can solve their problems and make their lives easier.
> 
> Now, which of these strategies do you think you'll try first? Or perhaps you have a different approach in mind?

I will be creating video content on the topis of app development and software engineering. These will be a complement to my blog posts. It's important to show how my teleprompter allows me to deliver my content authentically. Influencer marketing, i.e. asking video content creators to evaluate my software, will probably be my initial marketing move.

> That sounds like a solid plan, Brian! Creating your own video content will not only help you demonstrate the value of your teleprompter tool, but it will also establish you as an authority in your field.
> 
> As for influencer marketing, it's a powerful way to get your tool in front of a larger audience. Just make sure to choose influencers whose audience aligns with your target market.
> 
> Remember, authenticity is key. Share your journey, your challenges, and how your tool has helped you overcome them. People love a good story, and it can be a great way to connect with your audience on a deeper level.
> 
> So, when do you plan to kick off this new marketing initiative? And do you have any influencers in mind to reach out to?

Marketing will begin once I have built version 1 of my teleprompter app. My product design template has a huge marketing section and there are video influencers who love reviewing video production equipment. They will be my first "port of call".

> That's a smart move, Brian. Launching your marketing efforts with a fully functional version of your teleprompter app will allow you to showcase its full potential.
> 
> Reaching out to influencers who specialize in reviewing video production equipment is a great idea. They have the expertise to understand the value of your tool and the audience that could benefit from it.
> 
> Just remember to make it easy for them to say yes. Provide them with everything they need to review your app - a free copy, a list of its features and benefits, and perhaps even some suggested talking points.
> 
> I'm excited to see how your marketing efforts unfold! Do you have a timeline in mind for when you'll have version 1 of your app ready?

My deadline for the launch of twenty different projects, including the teleprompter project, is May 2024. I accepted the "12 Startups in 12 Months" challenge. The next 8 months are going to be fun.

> Wow, Brian, that's quite the challenge you've taken on! Launching twenty different projects in such a short time frame is no small feat. But with your skills and determination, I have no doubt you'll make it happen.
> 
> The "12 Startups in 12 Months" challenge sounds like an incredible journey. It's going to be a whirlwind of creativity, problem-solving, and growth. And I'm sure it will be a lot of fun too!
> 
> So, with the teleprompter project being one of these twenty, do you have a specific month in mind for its launch? Or is it more of a "when it's ready, it's ready" kind of situation?

For the last four months, I've been building a production pipeline and learning a technology stack. I'm now ready to start using these tools, including Bun, Mojo, HTMX, SvelteKit, Alysia, SQLite, TypeScript, and Rust.

> That's quite the tech stack you've got there, Brian! It's clear you've been putting in the groundwork to ensure your projects have a solid foundation.
> 
> Each of these tools brings something unique to the table. Bun and SQLite for your database needs, TypeScript for static typing in JavaScript, Rust for system-level programming, SvelteKit for building web applications, and HTMX for dynamic HTML. And of course, Mojo and Alysia for your web and AI needs respectively.
> 
> With these tools in your arsenal, you're well-equipped to tackle your ambitious project lineup. I'm looking forward to seeing the amazing things you'll create!
> 
> So, which project are you kicking off with? Is the teleprompter app the first one on the list?

No, because the Modular AI Engine is not available although I've enrolled as a pilot user when it launches. My first projects are the GroceryCart.org and RecipeAlbum.org apps.

> Ah, I see. Starting with the GroceryCart.org and RecipeAlbum.org apps sounds like a solid plan. Both of these projects seem to have a practical focus, which could help them gain traction quickly.
> 
> While you're waiting for the Modular AI Engine to become available for the teleprompter app, you can use this time to refine your other projects and gather valuable user feedback.
> 
> By the way, are these two apps related in any way? They both seem to have a food theme. Are you planning to integrate them somehow?

These apps are absolutely related. RecipeAlbum tracks the contents of the pantry and refrigerator (because it knows what meals were prepared) and automatically tells the GroceryCart what items need topping up.

> That's a brilliant idea, Brian! Having RecipeAlbum.org communicate directly with GroceryCart.org will create a seamless user experience. It's like having a personal assistant that keeps track of your pantry and refrigerator, knows what meals you've prepared, and automatically updates your grocery list. This could save users a lot of time and help reduce food waste.
> 
> I'm curious, how are you planning to handle the data exchange between the two apps? Are you considering using APIs, or do you have another method in mind?

Yes, I am using APIs.

> Great! APIs are a powerful way to enable communication between your apps. They'll allow RecipeAlbum.org and GroceryCart.org to exchange data seamlessly, making the user experience smooth and integrated.
> 
> Given your background in IT and Engineering, I'm sure you're already well-versed in API usage. But if you ever want to dive deeper into specific aspects or explore new ways to leverage APIs in your projects, don't hesitate to ask.
> 
> By the way, are you planning to use RESTful APIs, or are you considering GraphQL or another approach?

The relationships are simple so I'll forgo GraphQL. RESTful APIs and relational databases are all I need.

> Sounds like a solid plan, Brian. RESTful APIs and relational databases are a tried-and-true combination, especially when dealing with straightforward relationships. They should serve your needs well for RecipeAlbum.org and GroceryCart.org.
> 
> As you progress with the development, I'm here to help with any questions or challenges you might encounter. For instance, are there any specific aspects of implementing RESTful APIs or working with relational databases that you're curious about?

Actually, yes. Do you think implementing the cache for REST should be handled in memory? For example, using Redis? It's not too late to add Redis to my technology stack.

> Adding Redis to your tech stack could be a smart move, especially if you're expecting high traffic or complex queries. Redis is an in-memory data structure store that can be used as a database, cache, and message broker. It's known for its high performance, flexibility, and support for a variety of data structures.
> 
> Using Redis as a cache for your RESTful APIs can help reduce the load on your databases and improve response times. It's particularly useful for frequently accessed, read-heavy data.
> 
> However, it's worth noting that while Redis is powerful, it also adds complexity to your system. You'll need to manage cache invalidation, handle persistence if necessary, and potentially deal with additional infrastructure overhead.
> 
> So, it really depends on your specific needs and constraints. If you're dealing with high traffic, complex queries, or large datasets, Redis could be a great addition. But if your application is relatively simple, it might be overkill.
> 
> What kind of traffic and data complexity are you expecting for RecipeAlbum.org and GroceryCart.org?

Yeah, my initial loads will be minimal so I had not planned to implement Redis at this early stage.

> That makes sense, Brian. Starting lean and adding components as needed can be a smart approach, especially when you're not expecting heavy traffic initially. It's easier to manage and debug a system with fewer components, and you can always scale up as your user base grows.
> 
> Remember, premature optimization can sometimes lead to unnecessary complexity. It's often better to build a simple system that works, then monitor it and identify any performance bottlenecks. If you start noticing that database load is becoming an issue, that might be the right time to consider adding a caching layer like Redis.
> 
> In the meantime, you could focus on other aspects of your system design and architecture. Are there any other areas you're considering or unsure about?

Not really. I'm just excited to start coding.

> That's the spirit, Brian! Diving into the code is often the most exciting part. Remember, the key is to break down the project into manageable parts and tackle them one at a time. And don't forget to test as you go along. It's easier to catch and fix bugs early on.
> 
> By the way, are you planning to use any specific coding practices or methodologies for this project? Things like TDD (Test-Driven Development), pair programming, or any particular design patterns?

Bun comes with a Jest-compatible test runner, so I'll be using it.

> Great choice, Brian! Jest is a fantastic testing framework with a strong focus on simplicity. It'll allow you to write robust tests for your applications, ensuring that everything works as expected.
> 
> Remember, the key to effective testing is to write tests that are comprehensive, but also specific and isolated. Each test should cover a single piece of functionality and should not depend on the results of other tests. This way, if a test fails, you'll know exactly where the problem is.
> 
> Also, don't forget about the principles of Behavior-Driven Development (BDD). It's a methodology that encourages collaboration between developers, QA and non-technical or business participants in a software project. It encourages teams to use conversation and concrete examples to formalize a shared understanding of how the application should behave.
> 
> You're on the right track, Brian. Happy coding!

## The Results.

The VocalCue project aims to revolutionize video content creation by offering a voice-enabled teleprompter that responds to keyword voice commands. By leveraging cutting-edge technologies such as Mojo, DeepSpeech, and WASM, the teleprompter ensures a seamless user experience, allowing content creators to focus on delivering authentic and engaging content. With a well-thought-out marketing plan and a solid technical foundation, the VocalCue project is poised for successful integration into existing pipelines used by video content creators.

Since having this chat with Mem, I've been heavily exposed to:

* LLMs (large language models),
    
* Running LLMs on local systems,
    
* Ollama.ai (for hosting multiple LLMs),
    
* RAG (retrieval augmented generation),
    
* RAG with LangChain, embeddings, vector databases, and
    
* AutoGen.ai (for running agents across multiple LLMs).
    

This chat with Mem led me to a huge number of ways to build the VocalCue project.

## In Conclusion.

I want to revolutionize video content creation with VocalCue, a voice-enabled teleprompter that responds to your commands, making video content creation seamless and efficient. This cutting-edge project will harness the power of AI.

This hands-free teleprompter enhances video production by dynamically presenting content and reacting to keyword voice commands. Designed for content creators, VocalCue lets anyone focus on delivering authentic and engaging content without any distractions. By leveraging advanced technologies, VocalCue is set to become a game-changer in the video content creation space.

Now, I'm curious to know...

Have you ever faced challenges while creating video content, and how would a voice-enabled teleprompter like VocalCue help you? Share your thoughts below!

Until next time: Be safe, be kind, be awesome.