This is a summary of [Fireship's youtube video](https://www.youtube.com/watch?v=Dkx5ydvtpCA) explaining 10 rendering patterns to choose from while building a web app, all credits for the following content goes to the linked source, i only did a recap for study purposes.

## What is a rendering Pattern? 

Rendering is the process of turning data and code into HTML that can be seen by the end user. This can be done on the server or in the browser, all at once or partially and these methods all have trade-offs in terms of user experience, developer experience and performance.

### Static Rendering

The original and most basic rendering Paradigm is a **static website**: in this rendering Paradigm you put together all of your web pages in advance then upload them as static files to a storage bucket somewhere in the cloud, and point a domain name to them. 
This works great even in today's world and there are Frameworks like **Hugo**, **11ty**, and **Jekyll** that can help you build them programmatically.
The drawback is that they're not great for websites where the the data changes often so it's only suitable for very basic websites that **don't require a ton of interactivity or dynamic data**.

### Multi-page websites

Eventually websites needed to be more Dynamic and that brought us multi-page applications where the HTML and data is put together dynamically on a server whenever a request comes in from a browser.
This means that **the appearance of the website can change whenever the underlying data changes** many of the biggest web apps like amazon.comstill use this approach today.
There are many popular Frameworks to build multi-page apps like **Ruby on Rails**, **Django**, and **Laravel** as well as content Management Systems like **WordPress**.
This approach worked great until the iPhone came out then people started to realize that having this full page reload on every URL feels kind of clunky compared to the super smooth iPhone apps, that's why approximately in 2010 we saw the rise of the **single page application**.

### Single-page application

Single-page application can be built with popular frameworks like **Angularjs** and **React**  .
In the **SPA** Paradigm all the UI rendering happens in the browser: you start with one HTML page as a shell, then execute JavaScript to render the UI and fetch any required data with an additional HTTP request.
Even though it's just a single page it can still have multiple routes that don't point to a server, they're just updated by JavaScript in the browser.
This has the huge advantage of feeling instantaneous to the end user unlike a multi-page application that might take at least a few hundred milliseconds or more to render the page.
There are some big disadvantages:
- It requires a large JavaScript bundle which can make the initial page load pretty slow.
- Because it only renders a shell, search engines even today have a hard time understanding any of the content on the dynamic routes and that's a no-go if you need good SEO or want people to share your content on social media.

### Server-side Rendering
A few years later it was time for a new type of framework, something that could render HTML and data or the initial page on the server, then hydrate to client-side JavaScript afterwards.
We call this **SSR** today, but the general idea is that the initial request goes to a server that renders everything dynamically, then after that initial page load JavaScript takes over to give you the app like single page application experience.
This Best of both Worlds approach is used by Frameworks like **Next JS**, **Nuxt**, **Svelte Kit** and so on, which are often referred to as **meta Frameworks**.
This is likely the **most popular rendering strategy** as of today but there are still some drawbacks: you need an actual server and servers cost money.

### Static site generation

A slight variation on SSR is **SSG** or **static site generation**.
In this paradigm, you render all of your HTML in advance and then upload it to a static host like a storage bucket.  Like SSR it will hydrate to JavaScript after the initial page load.
Websites like this are often called **Jam stack sites** and they're typically built by the same meta fameworks like  **Next JS** and **Svelte Kit** .
You get the simplicity and low-cost hosting of a static site with the app-like experience of a SPA.
The only bad thing is you have to redeploy your site whenever the data changes and that's why they invented ISR or incremental static regeneration.

###  Incremental static regeneration

This Paradigm started in **Next JS** and the idea is that you deploy a static site but you rebuild individual pages on the fly on your server when the cache is invalidated.
Normally with a static site you can just cache everything permanently on a CDN making it extremely fast with ISR: the Cache can be invalidated based on certain rules like a specific amount of time and when that happens the pages will be rebuilt. 
This allows you to handle Dynamic data without the need for an actual server deployment like you would with SSR. you get the best of both worlds between SSG and SSR but the drawback is that it's more complex to set up on your own which means you'll likely need to find a host like **Vercel** that supports it out of the box .

### Partial Hydration
Now another problem we haven't talked about with any framework that uses hydration is that on the initial page load the app might feel like it's frozen while the JavaScript is still executing to take over the rendering process, to solve this problem we have **partial hydration**. 
On a large website JavaScript may have a lot to do for things that aren't even visible to the end user like rendering an interactive footer.
With partial hydration you might render the components at the top of the page first and then wait until the user scrolls down before making that component interactive.
Many tools today support code splitting to break your apps into smaller chunks to facilitate lazy loading patterns like this, but it may be possible to render even more efficiently with the **islands architecture**.

### Islands
Normally when hydrating JavaScript takes over the entire page, but that's not very efficient because many components are just static and non-interactive.
With **Islands** you start with static HTML, then only use JavaScript to hydrate interactive components. This gives you **islands of interactivity**: frameworks like **Astro** facilitate this pattern-
What's cool about it is that you may have a page that's not interactive at all in which case no JavaScript is ever shipped to the client even though you built the UI with a JavaScript framework like React.

### Streaming server-side rendering
Another way to address inefficient hydration is a paradigm called **streaming SSR** which is supported in Frameworks like **Next JS 13** with the app directory, thanks to building blocks like **React server components**.
Basically it allows you to render server-side content concurrently in multiple chunks instead of all at once.
Ultimately this means the UI becomes interactive faster and feels more performant to the end user, but what if there is a way we could get rid of hydration altogether?

### Resumability
This is a new rendering Paradigm being pioneered by the **qwik** framework.
It takes an interesting approach where a website and all of its data (even things like JavaScript event listeners) are serialized into HTML, then the actual JavaScript code is broken into tons of tiny chunks.
That means the initial page load is always static HTML: no hydration is needed.
Any JavaScript required for interactivity is **lazy loaded in the background**.


