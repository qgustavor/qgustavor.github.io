---
title: Some thoughts on the current state of JavaScript runtimes
date: 2026-11-09T13:48:00
description: Gustavo rants on the state of JavaScript runtimes
---

Since the beginning of 2026 I have been trying to work on [adorai](https://adorai.neocities.org). That said, it's a mess: it's core logic lives on a huge .js file, so I need to modularize it so I can continue developing in a sane way. Thus, I made a new folder for this project named "vite-project" and went to [vite.dev](https://vite.dev/) to check what's the current-year way to start a Vite project. Then, I was caught with a dilemma: *which runtime to use?*

Well, which runtimes I often use for my projects? Node.js, Deno and Bun. Then, what should I use? Node.js is old, so maybe consider something else? Bun works, but it's slop coded (their maintainer pushed a huge PR changing lots and lots of files recently, rewriting almost everything). Deno will stop being maintained after October 2027, but maybe there are forks...

So I checked Deno's GitHub and found [this discussion](https://github.com/denoland/deno/issues/37030) and found a weird (but interesting) complaint about Deno: *was a mistake making it be Node.js compatible?* One of the comments even commented about [their fork of Deno](https://ende.sh/) without Node.js compatibility (which, I will comment later).

This question annoys me. Sure, maybe the great issue with Deno was trying to make it compatible with Node.js. On one side, if Deno's compatible with Node.js, people can replace Node.js with Deno and gain the features which Node.js doesn't have, it's a good thing, no? Well, it helps bringing users, but then why would people develop tooling and libraries for Deno? *Just develop for Node.js and Deno will be compatible.*

So the major issue of this is that it hurts the FOSS development culture around JavaScript: if Node.js provides anything easier to implement than a web standard, then library developers would only care about supporting standards if they want it because their own beliefs. Example: MEGAJS has a version specifically for Node.js because it's crypto implementation supports streaming with Web Crypto doesn't (as of writing), so the non-Node versions need to implement crypto in user-land, pure-JS, which, to be fair, I don't like (it's too risky).

Also, when Deno 2 was released, the version that introduced most Node.js compatibility changes, it actually broke Deno 1 projects that assumed a package.json near scripts would be ignored. I had to add `--no-config` to lots and lots of scripts of mine due to that. On Deno 1 you could import npm libraries using the `npm:` specifier, but migrate to Deno 2 and it tries to use a nearby package.json to resolve npm packages. Sudden breaking change!

Then, sure, Ende removes that, no `npm:` specifier, no `node:` built-ins, but, why? As I mentioned before, library developers don't have too much incentives for migrating their code to use web standards instead of Node.js built-ins, isn't like people would write JSR libraries suddenly just because a single runtime decided to return to the original Deno objective to supporting open web standards. Not to mention that the development of this runtime was so fast one can only assume it was AI-driven (which looks to be true, from the `agents.md` file in the documentation repository) without proper human supervision, which is dangerous as hell.

---

Well, before this "Cloudflare bought Deno" event I would classify those three runtimes as following:

- Node.js: use when you want to feel safe, want something battle tested along the years.
- Deno: use if you want to share self-contained scripts. No, the permission system is not worth your attention.
- Bun: if you want to distribute your code as self-contained executable files, or just want a faster runtime, and you are not afraid of slop code.

But now I would not recommend Deno -- nor Deno forks -- for that. And it's a shame! It's a shame because it remembers me of another big issue of the current platforms: platform lock-in around Microsoft.

See, Microsoft bought GitHub and NPM, and recently then were been pushing updates disguised as "security updates" that made NPM harder to use without GitHub and/or other approved tools. They announced they will make importing modules from HTTPS CDNs (which is how SheetJS CE recommends installing) harder (claiming they are less safe). All of this only leads to one platform lock-in. It hurts the community.

If you can't use HTTPS as an alternative to NPM and host your packages yourself, what's an alternative? JSR? Maybe, but JSR rules are way more restrictive than NPM. I can't publish megajs on JSR due to its requirements, mainly, "You cannot publish CommonJS modules." JSR isn't a package registry for JavaScript, it's a package registry for server-side JavaScript runtimes which support ESM. Requiring ESM means for me that I no longer could support two legacy releases of megajs (or I would have to host them elsewhere). Sure, the next version of megajs will be ESM-only, but isn't an easy choice for library developers to stop supporting things just because their registry doesn't allow them. See, people prefer rehosting SheetJS CE on NPM over abiding to their "use our CDN, please" rule, it breaks people's workflow, as annoying as it is.

---

So, in conclusion, I'm annoyed and I don't have high hopes on JS. I will probably use Bun over Node.js for adorai, because if things go south for Bun I can just switch to Node.js and it's faster. I'm sure late on having to learn a better server-side language for my projects, maybe Rust, or Go, I don't know.
