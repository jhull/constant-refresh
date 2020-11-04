---
title: 'NuxtJS, SSG, and Authorization'
tldr: "A simple trick to alleviate headaches. "
published: '2020-11-03T18:36:00'
id: 'a4b91b87-9df8-4bbd-8b57-f98f3eaca737'
---

Authorization and protected content is a pain. Add in a statically generated site, and you've got a recepie for hours and hours of **banging your head** against the keyboard trying to figure out how to make it all work.

The problem?

Hydration. A static site by definition is unaware of the user’s logged in status. And when it comes to *hydrating*, or populating individual pages with protected content, the page needs to know that you want to run an authorization check. 

## The Static Solution

With [Nuxt](https://nuxtjs.org), the greatest most funnest app development platform in the world, static site generation (SSG) is super simple. You add this:

```
static: true
```

to your `nuxt.config.js` and Nuxt crawls your entire app, generating individual HTML pages for delivery to the web. 

And while Nuxt offers [a great first-class Auth module](https://auth.nuxtjs.org), it fails to make that check on first page load—

—unless you wrap the protected content with this:

```
<client-only>
 <ProtectedComponent/>
</client-only>
```

That `client-only` wrapper is the key to all your problems. And it’s not for brevity that the protected component sits in a separate module. You need to put that code in another file if you don’t want the app to ignore it on initial page load 

[Subtext](https://narrativefirst.com/subtext/), my story development app written with Nuxt, contains several special features for subscribers—many of which sit on unprotected pages alongside other content. 

When I tried to cordon off parts of the page with the `client-only` tag, they refused to load. As soon as I separated them out, everything worked as expected. 

(And my subscribers are super happy for it 😀)