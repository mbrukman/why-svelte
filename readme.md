# Why Svelte is our choice for a large web project in 2020

**tldr** — [Svelte](https://github.com/sveltejs/svelte)
is a JavaScript framework for building user interfaces.
Its compiler architecture enables amazing tradeoffs for UX and DX.
Svelte might be worth your attention,
especially if you pine for the web of yore and future.

## Contents

- [Introduction](#Introduction)
- [Advantages](#Advantages)
  - [easy to learn](#easy-to-learn)
  - [syntax and semantics](#syntax-and-semantics)
  - [write less code](#write-less-code)
  - [compilers enable output flexibility](#compilers-enable-output-flexibility)
  - [great performance](#great-performance)
  - [feels good](#feels-good)
  - [aligns with the web platform](#aligns-with-the-web-platform)
- [Disadvantages](#Disadvantages)
  - [compilers move complexity](#compilers-move-complexity)
  - [using Svelte means adopting a new language](#using-Svelte-means-adopting-a-new-language)
  - [reactive syntax is for components only](#reactive-syntax-is-for-components-only)
  - [rendering blocks the main thread](#rendering-blocks-the-main-thread)
  - [if it ain’t broke](#if-it-aint-broke)
- [Drawbacks today](#Drawbacks-today)
  - [immature tools](#immature-tools)
  - [best practices are still evolving](#best-practices-are-still-evolving)
  - [young library ecosystem](#young-library-ecosystem)
  - [the bundle size inflection point](#the-bundle-size-inflection-point)
  - [barrier to open source contributions](#barrier-to-open-source-contributions)
  - [fewer jobs today](#fewer-jobs-today)
  - [it’s a volunteer effort](#its-a-volunteer-effort)
- [Conclusion](#Conclusion)

## Introduction

It’s March 2020 and a friend and I are spinning up a big long-term web project.
We’re choosing technologies and I’m recommending a UI framework.
I love writing frontends and my friend is a backend developer
with a little frontend experience. Here’s what our project looks like:

- competes with community platforms like forums and chat apps
- heavy on content and extra heavy on interactivity and app-like behavior
- embraces the web platform and optimizes for both desktop and mobile
- it’s big and [we plan to work on it](https://felt.dev/about) for many years

So — which frontend JavaScript UI framework should we choose?
For context, I’ve used React full-time since 2014 and Svelte for a year.
I’ve also made small things with Vue, Angular, and Ember, and before that,
I worked with Backbone and jQuery for three years.
I pledge no allegiance — all are good tools.

Our top priority is the end user experience.
Whatever tools we use should optimize for the quality of the experience
while balancing other concerns. This is no simple formula.
Many factors affect UX — performance, development speed,
even [developer happiness](https://rubyonrails.org/doctrine/#optimize-for-programmer-happiness).
Each of these is complex and interrelated.
This is a subjective choice, not a solvable equation,
and any recommendation is going to be context-dependent and biased.
My goal is to communicate why I believe Svelte is the better choice
for our project, lay out the pros and cons,
especially as they relate to its compiler paradigm,
and open doors for you to learn more.

Here’s the current opening pitch at [svelte.dev](https://svelte.dev):

> Svelte is a radical new approach to building user interfaces.
> Whereas traditional frameworks like React and Vue do the bulk of their work
> in the browser, Svelte shifts that work
> into a compile step that happens when you build your app.

> Instead of using techniques like virtual DOM diffing,
> Svelte writes code that surgically updates the DOM
> when the state of your app changes.

If you’re new to Svelte, now would be a good time to read
[its introductory blog post](https://svelte.dev/blog/svelte-3-rethinking-reactivity).
From here I’ll assume some familiarity.

Svelte is a compiler that turns declarative components
into imperative JavaScript that runs about as fast as hand-written code.
After using Svelte for a year and participating in the community,
I can say I love its design and I’m having a lot of fun.
It’s an enjoyable DX that doesn’t compromise on UX.
I think it’ll soon become common knowledge among UI developers that compilers
have an advantage over runtime-only frameworks for hitting this sweet spot.
Both Angular ([Ivy](https://angular.io/guide/ivy))
and Ember ([Octane](https://blog.emberjs.com/2019/12/20/octane-is-here.html))
have evolved towards compilation as Svelte helps popularize the idea.

[Rich Harris](https://github.com/rich-harris) created Svelte in 2016
for his work on interactives at the New York Times.
The work demanded web UIs that are fast, tiny in bundle size,
and quick to produce, with good support for SVG and animations.
His colleague [Mike Bostock](https://github.com/mbostock)
(of [d3](https://github.com/d3/d3)) had been promoting compilation
as a powerful pattern that was underutilized on the web.
Svelte grew out of these needs and inspiration.
In early 2019
[version 3 was released](https://svelte.dev/blog/svelte-3-rethinking-reactivity),
bringing major innovations like
[reactive assignments](https://svelte.dev/examples#reactive-assignments),
[reactive declarations](https://svelte.dev/examples#reactive-declarations),
and [composable lifecycle functions](https://svelte.dev/examples#ondestroy),
attracting significant attention in the web community.
([1](https://twitter.com/sveltejs/status/1120666410332688386),
[2](https://twitter.com/Rich_Harris/status/1120633203927203840),
[3](https://twitter.com/HenrikJoreteg/status/1120926295565553665),
[4](https://twitter.com/sarah_edo/status/1120846189274918912))
I was loosely following Svelte because it kept smoking benchmarks,
and version 3’s ergonomics and reactivity convinced me of its potential —
I began using it for risk-tolerant projects.

In the [State of JS 2019 survey](https://2019.stateofjs.com/front-end-frameworks/svelte/),
75% of respondents have heard of Svelte,
45% are interested in learning it,
and 7% have used it.
(all public survey data is going to have biases, but roughly speaking,
these are great numbers for a smalltime framework)
It’s no exaggeration when author Rich Harris calls the community
[small but mighty](https://twitter.com/rich_harris/status/1207505891693600769).
Compared to modern mainstream frameworks like React and Vue and their
communities, Svelte is smaller and less mature,
but its community is active and established.
Svelte is now commonly mentioned in the same breath
as React, Vue, Angular, Preact, and Ember.

Like all technologies Svelte has its tradeoffs.
We’ll explore both the pros and cons ahead.
The costs and benefits to your projects are situational.
Some downsides are unavoidable, but many are temporary
if growth and development continue.
First let’s talk about the good stuff.

## Advantages

Our goal is to create amazing user interfaces that exceed expectations,
and Svelte is a tool that delivers.
By default, Svelte websites are fast and lightweight.
As a tool, it’s powerful, flexible, and beautifully designed.
Its compiler architecture unlocks broad powers
ripe for further exploration.
Making things with Svelte feels fun and streamlined.
Let’s walk through the details.

### easy to learn

Svelte is easy to learn.
Its design philosophy shares much with
[The Zen of Python](https://www.python.org/dev/peps/pep-0020/#the-zen-of-python).
The team values beginner friendliness and
the [official tutorial](https://svelte.dev/tutorial/basics)
is excellent and approachable.
The official blog post
[“Svelte for new developers”](https://svelte.dev/blog/svelte-for-new-developers)
helps those new to Node and the command line.

Its `.svelte` files pack together all three of the web’s languages
with holistically-designed extensions.
Like Vue, Svelte templates are a superset of HTML.
If you know HTML and CSS, you can write Svelte immediately
and learn more as you go, layering useful concepts on top of the web platform.
People who already know JavaScript and a modern frontend framework
regularly mention how easy it is to learn Svelte.
([1](https://twitter.com/sveltejs/status/1167081592420012032),
[2](https://twitter.com/hexrcs/status/1185186492982943744),
[3](https://twitter.com/Wattenberger/status/1221799311144603651))

Like most frameworks that abstract the DOM, Svelte has incompatibilities
like the inability to name a prop `class` because it’s a reserved keyword in JS,
and you’ll use `on:click` not `onclick`,
but these quirks are few in number and reflect carefully chosen tradeoffs.
Svelte does its best to harmonize with the web platform,
welcoming both experienced developers and newcomers
with whatever web knowledge they have.

### syntax and semantics

The Svelte language’s extensions to HTML, CSS, and JS
are designed to improve the development experience,
and they set the framework clearly apart from its peers.
Svelte initially received a lot of attention
for its performance and small bundles,
but since v3 the dev team has emphasized Svelte’s DX advantages.
Here are some of the official examples, which hopefully speak for themselves:

- [reactive assignments](https://svelte.dev/examples#reactive-assignments)
- [reactive declarations](https://svelte.dev/examples#reactive-declarations)
- [reactive statements](https://svelte.dev/examples#reactive-statements)
- [declaring props](https://svelte.dev/examples#declaring-props)
- [store auto subscriptions](https://svelte.dev/examples#auto-subscriptions)
- [transitions](https://svelte.dev/examples#transition)
- [event forwarding](https://svelte.dev/examples#event-forwarding)
- [optional two-way binding](https://svelte.dev/examples#text-inputs)

### write less code

Svelte code is terse, and not in a cryptic way —
component definitions feel distilled to their essence,
with hardly any wasted characters.
See the official blog post
[“Write less code”](https://svelte.dev/blog/write-less-code)
for the full picture.
Rich also gave a related talk,
[“The Return of ‘Write Less, Do More’”](https://www.youtube.com/watch?v=BzX4aTRPzno).

### compilers enable output flexibility

As a compiler, Svelte can tailor its output code for context-specific needs.
For example, it can write to targets like
[custom elements](https://svelte.dev/docs#Custom_element_API)
a.k.a. web components — and component libraries
can export both Svelte components and vanilla JS scripts.
This makes it a good candidate for incremental adoption,
like [using Svelte components with React and Vue](https://github.com/pngwn/svelte-adapter).
Svelte outputs small bundles that
include only the framework code used by your components.

Svelte’s server-side rendering mode compiles components
to simple string concatenation for big performance gains.
A [charting library from Rich named Pancake](https://dev.to/richharris/a-new-technique-for-making-responsive-javascript-free-charts-gmp)
shows how Svelte can be used to create UIs that require no runtime JavaScript.
An [experiment with WebGL](https://github.com/sveltejs/gl)
and the NativeScript integration
[svelte-native](https://github.com/halfnelson/svelte-native)
demonstrate compile targets beyond the DOM
that bypass the costs of runtime abstractions like virtual DOM.

Within the constraints of Svelte’s syntax and semantics,
its output flexibility positions it well for the future.
It can change its runtime strategy without any changes to components,
holistically transforming both the runtime and the user’s code.
Modern webdev commonly pairs a runtime-only framework
with a non-UI compiler like Babel.
Svelte has a higher degree of freedom and unlocks power
by integrating the two as a UI component compiler.

Simply put, compilers have access to flexibility and power
that runtime-only frameworks lack —
this point is deep and there’s a wide frontier to explore.

### great performance

Svelte has excellent performance characteristics.
It deserves its reputation for speed but that’s not its top priority —
instead Svelte wants to provide an awesome development experience
and output code that performs well by default.
Svelte can optimize user code at compile-time,
like resolving the dependency graph of computed properties
to propagate changes with minimal runtime overhead,
and [there’s low-hanging performance fruit](https://twitter.com/Rich_Harris/status/1201565469406384128)
to be picked.

Runtime frameworks like React and Vue pay some costs
that compilers can minimize or avoid.
Virtual DOM implementations have downsides —
see the official Svelte blog post
[“Virtual DOM is pure overhead”](https://svelte.dev/blog/virtual-dom-is-pure-overhead).
While Vue is implementing strategies to
[optimize its runtime templating](https://twitter.com/youyuxi/status/1184824857663594499),
React is betting long-term on
[concurrent mode](https://reactjs.org/docs/concurrent-mode-intro.html)
and functional purity to improve performance,
leveraging its virtual DOM architecture to unlock benefits
unavailable to other frameworks, like rendering that never drops a frame. (!!)
Concurrent mode applies
[additional restrictions](https://reactjs.org/docs/concurrent-mode-adoption.html)
that [developers are learning to work with](https://twitter.com/AdamRackis/status/1236460463199850496),
which the React team confidently trades for the benefits.
The tradeoffs are complex, context-dependent, and nuanced.

React may provide amazing UX in some circumstances
once concurrent mode is ready,
but I’m skeptical that their solution is the best one for our problems.
My instincts lead me to prefer less abstraction,
lean on automated tools like compilers,
and avoid runtime costs without clear benefit.
[See this comparison](https://twitter.com/Rich_Harris/status/1200807516529147904)
Rich made between Svelte and a popular React concurrent mode demo.
Svelte can write code that performs similarly to hand-written JS
and sometimes do everything in a single animation frame,
where React sometimes spreads equivalent work over multiple frames.

Sometimes is the key word here.
There is no objectively right answer for every situation.
With Svelte we may end up jealous of React’s sweet non-blocking rendering
one day [as this tweet portends](https://twitter.com/acdlite/status/1228720823814344705),
but today Svelte is fast for typical usage, it should continue improving,
and it’s possible that Svelte will discover its own solutions
to the problem of blocking rendering.

### feels good

Making UIs with Svelte is a pleasure.
Svelte’s aesthetics feel like a warm cozy blanket on the stormy web.
This impacts everything — features, documentation, syntax, semantics,
performance, framework internals, npm install size,
the welcoming and helpful community attitude,
and its collegial open development and
[RFCs](https://github.com/sveltejs/rfcs) —
it all oozes good taste.
Its API is tight, powerful, and good looking —
I’d point to [actions](https://svelte.dev/docs#use_action) and
[stores](https://svelte.dev/docs#svelte_store) to support this praise,
but really, the whole is what feels so good.

The aesthetics of underlying technologies have a way of leaking
into the end user experience.
Our team is building open source community tools and Svelte
fits our identity as an independent labor of love with an organic community.
With some frameworks, you may find your needs at odds with
the enterprise-level goals of a megacorp owner,
and you may both benefit and sometimes suffer from their web-scale engineering.
Svelte’s future does not depend on the continued delivery of business value
to one company, and its direction is shaped in public by volunteers.
Regardless of measurable impact,
Svelte resonates with our emotions and it makes for a good story.

### aligns with the web platform

Svelte components are a thin layer over the DOM
and naturally expose the web platform.
Coding in Svelte feels like I’m moving with the grain of the web.
React abstracts the DOM with
[functionally pure declarative rendering](https://twitter.com/dan_abramov/status/1236643811998171136)
and provides escape hatches back to mutable imperative DOM land.
This is a profound philosophical difference that Rich gave a talk about.
(unfortunately not recorded —
[slides here](https://docs.google.com/presentation/d/1PUvpXMBEDS45rd0wHu6tF3j_8wmGC6cOLtOw2hzU-mw/edit))

The difference is salient with animation —
Svelte ships with builtin support for high performance transitions
and animations, using
[optimal CSS when possible and JS when not](https://svelte.dev/tutorial/custom-css-transitions).
In comparison, React’s functional declarative model has developers declare
what the UI looks like at individual snapshots in time.
Both the code we write and performance are impacted —
it can be difficult or verbose to accomplish some things like animations
in React, especially without libraries,
and high-performance React animation libraries often
[bail out of its rendering cycle](https://www.framer.com/api/motion/component#performance)
to manipulate the DOM directly.

Concurrent mode is a further departure from the DOM
and points toward the endgame of React’s functional purity.
It’ll be interesting to follow how this philosophical difference plays out
as each side of the spectrum moves closer to the theoretical endpoints.
Future web standards may or may not follow React’s lead.
For our project, we’re comfortable aligning
with the web platform for the long run —
maybe it’ll bring us full circle back towards React — who knows!

## Disadvantages

Svelte’s upsides are compelling to our team,
but we also need to understand its downsides.
First we’ll discuss the negatives that are unlikely to change.

### compilers move complexity

Compilers may appear to magically eliminate complexity,
but that’s an illusion — they shift it.
The compiler architecture moves complexity
from the runtime and source code to buildtime and tools.
Behind Svelte’s simple APIs sits a beefy compiler.
Frontend web development has become very tool heavy in the webapp era,
so in practice this adds little cost beyond what developers like myself
already pay, but increased build complexity is important to acknowledge.

For example Vue’s [Evan You](https://twitter.com/youyuxi) has stated
that Vue should always be droppable into any webpage for immediate development.
Many people like and rely on this ability.
It keeps things simple.

Svelte can do this but only by including its compiler in the browser,
which currently weighs 870k. This is super useful in some circumstances,
like [Svelte’s REPL](https://svelte.dev/repl/hello-world),
but it’s not a viable option for normal application code.
Svelte requires a build step that’s heavier
than React’s JSX and Vue’s `.vue` files.

### using Svelte means adopting a new language

[Svelte is its own language](https://gist.github.com/Rich-Harris/0f910048478c2a6505d1c32185b61934),
not plain HTML+CSS+JS — increasing the risks of adoption —
but it adheres closely to web standards
outside of its own targeted enhancements.
Svelte changes some of JavaScript’s semantics to support useful features
by extending/reusing/reinterpreting valid syntax.
(e.g. [reactivity](https://svelte.dev/tutorial/reactive-assignments),
[auto-subscriptions](https://svelte.dev/tutorial/auto-subscriptions),
and [declaring props](https://svelte.dev/tutorial/declaring-props))

As as result, you’ll need more specialized tools
and a little more framework-specific knowledge.
For those rare unfortunate times you find yourself migrating
Svelte components to another framework,
its language extensions add friction.

Rich is proposing to standardize its templating language as
[HTMLx](https://github.com/htmlx-org/HTMLx),
which may or may not gain adoption.

Svelte CSS is scoped to components, which is a nice default,
and it provides the [`:global` escape hatch](https://svelte.dev/docs#style)
to opt out.

[Many, many languages compile to JavaScript](https://github.com/jashkenas/coffeescript/wiki/List-of-languages-that-compile-to-JS)
to target the web platform.
Some languages are a natural fit with certain frameworks —
for example ClojureScript and ReasonML have great React integrations.
The Svelte compiler
[requires script tags to be JavaScript](https://twitter.com/Rich_Harris/status/1237864318164553729),
so any language you want to use through
[preprocessors](https://svelte.dev/docs#svelte_preprocess)
must satisfy that constraint,
and integrating an unofficial language
with Svelte’s markup (for e.g. typechecking)
requires more specialized tooling.
Svelte is written in TypeScript and work
[integrating it for users is in progress](https://github.com/sveltejs/svelte/issues/4518).

[Svelte isn’t alone in its approach](https://twitter.com/Rich_Harris/status/1120737306774843392)
of extending languages, but it goes further than Angular and Vue,
which extend HTML but not JS,
though their JS is subject to framework-specific rules and behaviors
not unlike Svelte.
React introduced both JSX and hooks,
the latter of which change some semantic expectations of JS function calls,
and it’s arguable whether React or Svelte
is the more radical departure from the norm.
(sounds like a boring argument tbh)

Treating the web as a compile target has a lot of implications, many negative.
For example “view source” is a beautiful feature of the web
that’s especially useful for learning and it’s an important part of its history.
Source maps, which Svelte uses to map its web language outputs
back to its source language, have limitations.
Kyle Simpson makes a thorough case against treating JavaScript as a machine
in his talk [“Keep Betting on JS”](https://www.youtube.com/watch?v=ft5bYnt0W48).
I currently see Svelte as an acceptably webby choice for our long-term project,
but this point is worth serious consideration.

After using Svelte for a year, I can comfortably claim
it extends the web’s languages with taste and restraint,
and for our team it’s worth the costs and risk.
By extending the web’s languages instead of replacing them
like [Elm](https://elm-lang.org/) and [Dart](https://dart.dev/),
Svelte will work with future versions of the standards — ES2042 here we come.
(design conflicts are possible — that’s where restraint is important)

### reactive syntax is for components only

Svelte’s reactive language extensions are limited to components.
In Vue and libraries like the React-friendly MobX,
you use the same syntax for reactive primitives in every module,
because they are plain JavaScript.

Although this is a restriction in Svelte, it comes with benefits as well —
its reactive syntax is part of why people like it so much, and its
[simple store contract](https://svelte.dev/docs#svelte_store)
interoperates with libraries like RxJS,
so you can choose among many state management options or stick with
Svelte’s simple builtin stores, depending on the needs of a project.
Our large project is going to need highly structured
and predictable state management, and Svelte’s flexibility
scales from trivial projects up to our big one.
We’re looking at
statecharts and [XState](https://github.com/davidkpiano/xstate)
to wrangle this problem.

### rendering blocks the main thread

Svelte may never be able to implement a full equivalent of React’s
[concurrent mode](https://reactjs.org/docs/concurrent-mode-intro.html),
which combines the virtual DOM and interruptible renders
to achieve rendering that drops no frames.
This could be significant and it’s the weakest part
of my recommendation to my team.
That said, Svelte may surprise us or find other angles to approach this problem.
For more about how concurrent mode relates to Svelte,
see [these tweets from Rich](https://twitter.com/Rich_Harris/status/1200805237948325888),
this section of
[his talk “Rethinking reactivity”](https://www.youtube.com/watch?v=AdNJ3fydeao&feature=youtu.be&t=1130),
and [the discussion above](#great-performance).
Svelte has a history of surprising innovations
but we shouldn’t choose Svelte today expecting an ideal answer.

Rich [intends to implement an equivalent to React’s suspense](https://twitter.com/Rich_Harris/status/1148263929497477120),
so it appears React’s advantage there is temporary.

### if it ain’t broke

React and other mainstream frameworks work great.
Is Svelte worth the time and risk?

## Drawbacks today

Many of Svelte’s negative tradeoffs reflect its relative youth
and not-yet-mainstream popularity.
Today these are issues, but I expect them to be resolved
as Svelte’s development and adoption continue.

### immature tools

Peripheral tooling is a work in progress.
With React and TypeScript we can write fairly well-typed frontends
with good buildtime error detection, featureful editor plugins,
and mature devtool browser extensions.
Svelte is its own language, not plain JS, so it needs specialized tooling.
Svelte has decent editor support today
but the plugins I’ve used have rough edges and missing features.

Svelte’s TypeScript support is
[a work in progress being helped by a TypeScript team member](https://github.com/sveltejs/svelte/issues/4518).

The [community](https://github.com/sveltejs/community)
has been actively improving tools for the year I’ve been using Svelte
(shoutout to [@UnwrittenFun](https://github.com/UnwrittenFun))
but there’s much to do before the DX feels polished.

### best practices are still evolving

Svelte’s userland resources and cultural knowledge like
patterns, anti-patterns, best practices,
and consensus libraries are sparse and under-developed.
People who adopt it today will have to think through problems
where other communities have common knowledge solutions,
making the learning curve temporarily steeper.

Svelte’s beginner documentation is great
but people are still figuring out what mastery looks like.
Thoughtful feedback from experienced Svelte users is readily offered
on [Discord](https://svelte.dev/chat), and the community is active
on [Twitter](https://twitter.com/sveltejs),
[Reddit](https://www.reddit.com/r/sveltejs/),
and [Stack Overflow](https://stackoverflow.com/questions/tagged/svelte),
but not to the degree of React and Vue,
which have vast communities and educational resources.

Our development will be slowed as our team develops ideas
about the best ways to build a big Svelte app.
I have a lot of experience working on JS frontends
and I enjoy the pattern frontier, so I’m personally excited
about working in a fresh and chaotic ecosystem with my teammates.
For us the slowdown is an acceptable cost
and we see a meaningful opportunity to grow as developers.

### young library ecosystem

Libraries are fewer in number and generally less mature.
Depending on your project and team,
this could be irrelevant, inconvenient, or a blocker.
Even though Svelte has
[many quality choices](https://github.com/sveltejs/community) for the basics
like [component sets](https://svelte-community.netlify.com/code/?tag=ui+component+sets),
its library ecosystem is a fraction of the size of the major frameworks.

For our project this is not impactful —
we’ll be writing most components from scratch for UX and DX reasons.
We’re developing our own design language and we care a lot about
customizability, consistency, and performance,
and off-the-shelf components add friction,
especially in a less mature ecosystem.

For short-term results,
Svelte today may not have the libraries to meet one’s needs.
We’re investing for the long-term.
Implementing components oneself is one of the best ways
to gain valuable experience as a developer,
and we’re able and willing to spend the time
to own our UI and level up along the way.

### the bundle size inflection point

Svelte is known for its tantalizingly small JavaScript bundles,
and [compiler improvements sometimes shrink the output](https://github.com/sveltejs/svelte/pull/3945#issuecomment-557840183)
even more for free, but there’s a problem here.
With its current compiler, as more components are added to a single bundle,
Svelte’s JS size advantage shrinks and eventually reverses,
because Svelte templates are compiled to a form
that is more verbose than the source.

Rich addresses this in the issue
[“Yes, but does it scale?”](https://github.com/sveltejs/svelte/issues/2546),
saying that code splitting usually retains Svelte’s bundle size advantage,
and notes that in the future,
Svelte could optionally send a template bytecode
instead of compiled JS to clients,
substantially lowering bundle sizes after paying the cost of the interpreter —
however today there is no such Svelte template interpreter.

A large majority of websites will not have this problem,
but our project is going to have a heavy UI metasystem similar to an IDE,
with components that are more difficult to code split and lazy load.
Our base JS cost may be larger than the equivalent
in other frameworks if we don’t pull off some wizardry.
That said, our primary use case is a long-lived app with chat,
so we care less about bundle size and more about
the performance of change propagation in the UI.

### barrier to open source contributions

Our project is an open source community platform that seeks
to build a community around its source code,
and Svelte is going to be a barrier to some would-be contributors —
not because it’s difficult to learn
([as mentioned earlier](#easy-to-learn), I think quite the opposite) —
but because many people develop an understanding of a single framework,
structure their thinking around its patterns, and remain in its garden,
often for employment reasons.

Some people who would jump into a React or Vue project
won’t look twice at a Svelte codebase — this can be mitigated but not ignored.
On the bright side, Svelte may attract some people
who have the time and motivation to learn a new framework,
and it’s approachable for web developers of any experience level.

### fewer jobs today

There are few jobs for Svelte right now.
Our team members are developing skills
that might not directly translate to future employment.
In my experience, learning multiple frameworks was tremendously helpful
for rounding out my frontend skills.

### it’s a volunteer effort

There’s no full-time team supporting Svelte —
its developers are part-time volunteers.
Bugs get fixed, features get added,
and many professionals rely on it in production,
but unlike other major frameworks,
nobody is being paid to work on it full-time.

Rich likes his dayjob, but it seems likely that funding
will be available to the dev team in the future, if they want it.

## Conclusion

Is using bleeding edge tech risky and foolish?
How much blood are we talking about?
My experience tells me Svelte is a safe choice,
more leading edge than bleeding.
However I’m more risk tolerant than most people,
I have a lot of experience with JS frameworks,
and our team is motivated, so we can deal with rough edges.

We’re happy to pay the costs of early adoption
when a technology provides significant advantages,
and that’s our bet for Svelte.

Evidence of growth, buyin, mindshare, etc:

- there’s a lot of logos and faces at [svelte.dev](https://svelte.dev/)
- the [InfoQ Trends Report 2020](https://www.infoq.com/articles/javascript-web-development-trends-2020/)
  puts Svelte in the “early majority” section of the adoption curve
- Svelte is one of the 6 JS frameworks in the
  [State of JS 2019 survey](https://2019.stateofjs.com/front-end-frameworks/svelte/) —
  75% have heard of it, 7% have used it,
  and 45% are interested in learning more
- GitHub stars in March 2020 (the best metric obv) —
  React has 145k, Vue 159k, Angular 59k, Svelte 31k, Preact 26k, and Ember 21k
- lots of [local meetup groups](https://svelte-community.netlify.com/events/)
  have formed in the last year
- IBM recently implemented their
  [Carbon design system in Svelte](https://github.com/IBM/carbon-components-svelte)
  and Apple is [hiring for Svelte](https://twitter.com/mansur_ashraf/status/1204542852581273600)
- [npm trends shows consistent growth](https://www.npmtrends.com/svelte)
  since v3 was released in early 2019
- active community —
  tweet [@sveltejs](https://twitter.com/sveltejs) —
  chat on [Discord](https://svelte.dev/chat) —
  unofficial subreddit [/r/sveltejs](https://reddit.com/r/sveltejs)

With the caveat that hero worship can be
gross, distorting, and unhelpful to everyone involved,
Svelte author [Rich Harris](https://github.com/rich-harris)
([@rich_harris on Twitter](https://twitter.com/Rich_Harris))
is one of my favorite open source developers.
In the JS community he’s well-known among tool authors
for [spreading interesting ideas](https://twitter.com/Rich_Harris/status/803713274596511747).
He’s the creator of many open source projects including
[Rollup](https://github.com/rollup/rollup),
the bundler of choice for many libraries including React and Vue.
Here are some of his inspiring talks about Svelte:

- [“The Return of ‘Write Less, Do More’”](https://www.youtube.com/watch?v=BzX4aTRPzno)
- [“Rethinking reactivity”](https://www.youtube.com/watch?v=AdNJ3fydeao)
- [“Computer, build me an app”](https://www.youtube.com/watch?v=qqt6YxAZoOc)

Alright! Was that a fairly thorough and clarifying overview?
I hope you’ll consider Svelte
next time you want to play around with some new technologies
and see it as a worthwhile option for making awesome software for people.

Want to learn more?
[The interactive Svelte tutorial](https://svelte.dev/tutorial/basics)
is a good place to start.
[The examples](https://svelte.dev/examples) are a good followup,
and [the API docs](https://svelte.dev/docs)
and [Discord community](https://svelte.dev/chat) can help you from there.
[The basic template](https://github.com/sveltejs/template) is a good way
to begin making stuff, or jump in with
[Sapper](https://sapper.svelte.dev/),
the officially supported app framework equivalent of
React’s Next.js and Vue’s Nuxt.js.
And finally,
[the Svelte community repo](https://github.com/sveltejs/community)
is a nice door into the ecosystem.

Discuss this post on the web:

- [/r/javascript](https://www.reddit.com/r/javascript/comments/fgcmxo/why_svelte_is_our_choice_for_a_large_web_project/) —
  [/r/sveltejs](https://www.reddit.com/r/sveltejs/comments/fgcn4l/why_svelte_is_our_choice_for_a_large_web_project/)
- [lobste.rs](https://lobste.rs/s/ver9ln/why_svelte_is_our_choice_for_large_web)
- [Hacker News](https://news.ycombinator.com/item?id=22534639)
- [Tildes](https://tildes.net/~comp/mjh/why_svelte_is_our_choice_for_a_large_web_project_in_2020)
- tweet me [@ryanatkn](https://twitter.com/ryanatkn)
  and see [the tweet for this post](https://twitter.com/ryanatkn/status/1237347309488349184)
- please feel free to
  [open an issue](https://github.com/feltcoop/why-svelte/issues)
  here on GitHub with questions/comments/improvements/etc

It’s worth mentioning that Svelte limits its scope
to being only a UI component framework.
Like React, it provides the view layer,
but it has more batteries included with its
[component-scoped CSS](https://svelte.dev/docs#style) and extensible
[stores for state management](https://svelte.dev/docs#svelte_store).
Others like Angular and Vue provide a more all-in-one solution
with official routers, opinionated state management, CLIs, and more.
[Sapper](https://sapper.svelte.dev/) is Svelte’s official app framework
that adds routing, server-side rendering, code splitting,
and some other essential app features,
but it has no opinions about state management and beyond.
Some devs prefer Svelte’s minimal approach that defers problems to userland,
encouraging more innovation, choice, and fragmentation,
and other devs prefer a more fully integrated toolkit
with a well-supported happy path.

The project that prompted this post is
[Felt](https://github.com/feltcoop/felt),
a super customizable community platform.
We’re in the planning phase right now —
[felt.dev](https://felt.dev) has an early mockup,
[felt.social](https://felt.social) has a mailing list signup,
and we’re @feltcoop
on [GitHub](https://github.com/feltcoop)
and [Twitter](https://twitter.com/feltcoop).
Felt is open source, easily self-hosted, and owned by a worker co-op
with the future goal of becoming a [platform co-op](https://platform.coop).
The name was inspired by Svelte so our bias goes deep. :]

Written by Ryan Atkinson ([@ryanatkn](https://github.com/ryanatkn))
with special thanks to
Hamilton Reed ([@greatbacon](https://github.com/greatbacon)),
Robert Hall ([@arxpoetica](https://github.com/arxpoetica)),
and [@pngwn](https://github.com/pngwn)
([![!!!](pngwn.jpg)](https://github.com/pngwn)),
and extra special thanks to the Svelte team and community
for the wonderful experience. 💚

[![Creative Commons License](cc-by-nc-sa.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)
[license](license)
