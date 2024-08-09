# Learning Svelte and SvelteKit

## [Part 1: Basic Svelte](https://learn.svelte.dev/tutorial/welcome-to-svelte)

### Introduction

- [Refer to variables](https://learn.svelte.dev/tutorial/your-first-component) - `<h1>Hello {name}</h1>`
- [Dynamic attributes](https://learn.svelte.dev/tutorial/dynamic-attributes) - `<img src={src} />` or `<img {src} />`
  - accessibility - `<img {src} alt='accessible description.' />`
- [Styling](https://learn.svelte.dev/tutorial/styling) - `<style> CSS... </style>`
- [Nested components](https://learn.svelte.dev/tutorial/nested-components) - `<Nested />`
  - Component names are always capitalized, to distinguish them from HTML elements.
- [HTML tags](https://learn.svelte.dev/tutorial/html-tags) - `<p>{@html string}</p>`

### Reactivity

- [Assignments](https://learn.svelte.dev/tutorial/reactive-assignments) - `<button on:click={increment}> </button>`
- [Declarations](https://learn.svelte.dev/tutorial/reactive-declarations) - `$: doubled = count * 2`
- [Statements](https://learn.svelte.dev/tutorial/reactive-statements):
  - `$: console.log()`
  - `$: { console.log() }`
  - `$: if (count >= 10) { }`
- [Update arrays and objects](https://learn.svelte.dev/tutorial/updating-arrays-and-objects):

  - `() => numbers = [...numbers, numbers.length + 1];`
  - `() => numbers[numbers.length] = numbers.length + 1;`
  - Name of updated variable must appear on the left hand side of the assignment.

    ```ts
    const obj = { foo: { bar: 1 } };
    const foo = obj.foo;
    foo.bar = 2;

    // instead
    const obj = { foo: { bar: 1 } };
    obj.foo.bar = 2;
    ```

### Props

- [Declaring props](https://learn.svelte.dev/tutorial/declaring-props) - `<script> export let answer; </script>`
- [Default values](https://learn.svelte.dev/tutorial/default-values) - `<script> export let answer = 'secret'; </script>`
- [Spread props](https://learn.svelte.dev/tutorial/spread-props) - `<PackageInfo {...pkg} />`

### Logic

- [If blocks](https://learn.svelte.dev/tutorial/if-blocks) - `{#if count > 10} .. {/if}`
- [Else blocks](https://learn.svelte.dev/tutorial/else-blocks) - `{#if count > 10} .. {:else} .. {/if}`
- [Else-if blocks](https://learn.svelte.dev/tutorial/else-if-blocks) - `{#if count > 10} .. {:else if count < 5} .. {:else} .. {/if}`
- [Each blocks](https://learn.svelte.dev/tutorial/each-blocks):
  - `{#each colors as color} .. {/each}`
  - `{#each colors as color, i} .. {/each}`
- [Keyed each blocks](https://learn.svelte.dev/tutorial/keyed-each-blocks) - `{#each things as thing (thing.id)} .. {/each}`
- [Await blocks](https://learn.svelte.dev/tutorial/await-blocks):
  - `{#await promise} .. {:then value} .. {:catch error} .. {/await}`
  - `{#await promise then number} .. {/await}`

### Events

- [DOM events](https://learn.svelte.dev/tutorial/dom-events) - `<div on:pointermove={handleMove}> .. </div>`
- [Inline handlers](https://learn.svelte.dev/tutorial/inline-handlers) - `<div on:pointermove={(e) => .. }> .. </div>`
- [Event modifiers](https://learn.svelte.dev/tutorial/event-modifiers) - `<button on:click|once={() => alert(clicked)}>`
  - List of modifiers:
    - `preventDefault`
    - `stopPropagation`
    - `passive`
    - `nonpassive`
    - `capture`
    - `once`
    - `self`
    - `trusted`
  - Chaining modifiers - `on:click|once|capture={ .. }`
- [Component events](https://learn.svelte.dev/tutorial/component-events):
  - Create event dispatcher
    ```html
    <script>
      import { createEventDispatcher } from "svelte";
      const dispatch = createEventDispatcher();
    </script>
    ```
  - `<Inner on:message={handleMessage}} />`
- [Event forwarding](https://learn.svelte.dev/tutorial/event-forwarding) - `<Inner on:message />`
- [DOM event forwarding](https://learn.svelte.dev/tutorial/dom-event-forwarding) - `<button on:click> Push </button>`

### Bindings

- Data flow in Svelte is _top down_.
- [Text inputs](https://learn.svelte.dev/tutorial/text-inputs) - `<input bind:value={name}>`
- [Numeric inputs](https://learn.svelte.dev/tutorial/numeric-inputs):
  - `<input type="number" bind:value={a} min="0" max="10" />`
  - `<input type="range" bind:value={a} min="0" max="10" />`
- [Checkbox inputs](https://learn.svelte.dev/tutorial/checkbox-inputs) - `<input type="checkbox" bind:checked={yes}>`
- [Select bindings](https://learn.svelte.dev/tutorial/select-bindings) - `<select bind:value={selected}>`
- [Group inputs](https://learn.svelte.dev/tutorial/group-inputs):
  - `<input type="radio" name="scoops" value={number} bind:group={scoops} />`
  - `<input type="checkbox" name="colors" value={color} bind:group={colors} />`
- [Select multiple](https://learn.svelte.dev/tutorial/multiple-select-bindings) - `<select multiple bind:value={flavors}> .. </select>`
- [Textarea inputs](https://learn.svelte.dev/tutorial/textarea-inputs):
  - `<textarea bind:value={value}> </textarea>`
  - `<textarea bind:value></textarea>`

### Lifecycle

- [onMount](https://learn.svelte.dev/tutorial/onmount)- runs after component is first rendered to the DOM.
- [beforeUpdate and afterUpdate](https://learn.svelte.dev/tutorial/update):
  - before and after DOM is updated.
  - `beforeUpdate` runs before `onMount`.
- [tick](https://learn.svelte.dev/tutorial/tick) - returns and resolves a promise:
  - after state changes have been applied to the DOM.
  - immediately, if there are no pending state changes.

### Stores

- [Writable stores](https://learn.svelte.dev/tutorial/writable-stores) - `const count = writable(0);`
  - `count.update((n) => n + 1);`
  - `count.set(0);`
- [Auto-subscriptions](https://learn.svelte.dev/tutorial/auto-subscriptions):
  - `onDestroy(unsubscribe);`
  - reference a store with `$`. Example,`{$count}`
- [Readable stores](https://learn.svelte.dev/tutorial/readable-stores) - `readable(initialValue, function)`
- [Derived stores](https://learn.svelte.dev/tutorial/derived-stores) - `derived(store, function)`
- [Custom stores](https://learn.svelte.dev/tutorial/custom-stores):
  - a store only needs to correctly implement the `subscribe` method.
  - can add custom methods to the store.
- [Store bindings](https://learn.svelte.dev/tutorial/store-bindings) - you can bind writable stores (has a `set` method).
  - `<input bind:value={$name}>`
  - `<button on:click={() => $name += '!'}> </button>`

## [Part 2: Advanced Svelte](https://learn.svelte.dev/tutorial/tweens)

### Motion

- [Tweens](https://learn.svelte.dev/tutorial/tweens) - gradual changes (progress bar).
  - Options:
    - `delay`
    - `duration`
    - `easing` - `p => t` function
    - `interpolate`
- [Springs](https://learn.svelte.dev/tutorial/springs) - frequent changes

### Transitions

- [Fade](https://learn.svelte.dev/tutorial/transition) - `transition:fade`
- [Fly](https://learn.svelte.dev/tutorial/adding-parameters-to-transitions) - `transition:fly`
- [In and out](https://learn.svelte.dev/tutorial/in-and-out) - `in:fade`, `out:fly`, and so on.
- [Custom CSS](https://learn.svelte.dev/tutorial/custom-css-transitions)
- [Custom JS](https://learn.svelte.dev/tutorial/custom-js-transitions) - typewriter effect, and so on.
- [Transition events](https://learn.svelte.dev/tutorial/transition-events):
  - `on:introstart`
  - `on:introend`
  - `on:outrostart`
  - `on:outroend`
- [Global transitions](https://learn.svelte.dev/tutorial/global-transitions) - `transition:slide|global`
- [Key Blocks](https://learn.svelte.dev/tutorial/key-blocks) - play transition when value changes, `{#key i} {/key}`.
- [Deferred transitions](https://learn.svelte.dev/tutorial/deferred-transitions) - `in:receive`, `out:send`

### Animations

- [Flip](https://learn.svelte.dev/tutorial/animate) - "First, Last, Invert, Play", `animate:flip`.

### Actions

- [Use](https://learn.svelte.dev/tutorial/actions) - element-level lifecycle functions, `<div class="menu" use:trapFocus>`.
- [Adding parameters](https://learn.svelte.dev/tutorial/adding-parameters-to-actions) - `<button use:tooltip={{ content }}> </button>`

### Advanced bindings

- [Contenteditable bindings](https://learn.svelte.dev/tutorial/contenteditable-bindings) - `<div bind:innerHTML={html} contenteditable />`
  - `contenteditable` attribute support:
    - `textContent`
    - `innerHTML`
- [Each block bindings](https://learn.svelte.dev/tutorial/each-block-bindings) - bind properties inside an `each` block.
- [Media elements](https://learn.svelte.dev/tutorial/media-elements) - bind properties of `<audio>` and `<video>` elements.
  - `readonly` bindings:
    - `duration` - total duration of video in seconds
    - `buffered` - array of `{start, end}` objects
    - `seekable` - ditto
    - `played` - ditto
    - `seeking` - boolean
    - `ended` - boolean
    - `readyState` - number between 0 and 4
    - `videoWidth` - for video only
    - `videoHeght` - for video only
  - `two-way` bindings:
    - `currentTime` - current point in the video, in seconds
    - `playbackRate` - how fast to play the video, `1` is normal
    - `paused`
    - `volume` - value between 0 and 1
    - `muted` - boolean
- [Dimensions](https://learn.svelte.dev/tutorial/dimensions) - bind block-level element:
  - `clientWidth`
  - `clientHeight`
  - `offsetWidth`
  - `offsetHeight`
- [This](https://learn.svelte.dev/tutorial/bind-this) - `bind:this`
- [Component bindings](https://learn.svelte.dev/tutorial/component-bindings) - bind to component props.
- [Binding to component instances](https://learn.svelte.dev/tutorial/component-this) - bind to component instances with `bind:this`.

### Classes and styles

- [Classes](https://learn.svelte.dev/tutorial/classes):
  - `<button class="card {flipped ? 'flipped' : ''}>`
  - `<button class="card" class:flipped={flipped}>`
- [Shorthand Class](https://learn.svelte.dev/tutorial/class-shorthand) - `<button class="card" class:flipped>`
- [Styles](https://learn.svelte.dev/tutorial/styles) - inline `style` attributes.
  - `<button class="card" style:--bg-1="palegoldenrod">`
- [Component styles](https://learn.svelte.dev/tutorial/component-styles) - influence styles inside a child component.
  - `:global` should be used as a last resort.
  - `<style> .box { background-color: var(--color, #ddd); } </style>`
  - `<Box --color="red" />`

### Component composition

- [Slots](https://learn.svelte.dev/tutorial/slots) - components can have children.
  - `<div class="card"> <slot /> </div>`
  - `<Card> <span>Patrick BATEMAN</span> </Card>`
- [Named slots](https://learn.svelte.dev/tutorial/named-slots) - `<div class="card"> <slot name="company" /> </div>`
- [Slot fallbacks](https://learn.svelte.dev/tutorial/slot-fallbacks) - `<slot name="telephone"> telephone </slot>`
- [Slot props](https://learn.svelte.dev/tutorial/slot-props) - `<slot {item} />`
- [Checking for slot content](https://learn.svelte.dev/tutorial/optional-slots) - `{#if $$slots.header} .. {/if}`

### Context API

- [setContext and getContext](https://learn.svelte.dev/tutorial/context-api):
  - Called during component initialization.
  - Context object can include anything, including stores.

### Special elements

- [<svelte:self>](https://learn.svelte.dev/tutorial/svelte-self) - allows a component to contain itself recursively.
- [<svelte:component>](https://learn.svelte.dev/tutorial/svelte-component) - instead of if blocks, create a single dynamic component.
- [<svelte:element>](https://learn.svelte.dev/tutorial/svelte-element) - instead of if blocks, create a single dynamic element.
- [<svelte:window>](https://learn.svelte.dev/tutorial/svelte-window) - add event listeners to the `window` object.
  - Can also add [event modifiers](https://learn.svelte.dev/tutorial/event-modifiers) like `preventDetault`.
- [<svelte:window> bindings](https://learn.svelte.dev/tutorial/svelte-window-bindings) - `<svelte:window bind:scrollY={y} />`
  - List of properties you can bind:
    - `innerWidth`
    - `innerHeight`
    - `outerWidth`
    - `outerHieght`
    - `scrollX`
    - `scrollY`
    - `online` - an alias for `window.navigator.onLine`
  - All properties are `readonly` except `scrollX` and `scrollY`.
- [<svelte:body>](https://learn.svelte.dev/tutorial/svelte-body) - add event listeners to `document.body`.
- [<svelte:document>](https://learn.svelte.dev/tutorial/svelte-document) - add event listeners to `document`.
  - Avoid `mouseenter` and `mouseleave` handlers here.
  - Use `<svelte:body>` instead.
- [<svelte:head>](https://learn.svelte.dev/tutorial/svelte-head) - insert elements inside `<head>` of your document.
  - Useful for thins like `<title>` and `<meta>` tags for good SEO.
  - In SSR mode, contents of `<svelte:head>` are returned separately from your HTML.
- [<svelte:options>](https://learn.svelte.dev/tutorial/svelte-options) - specify compiler options.
  - `<svelte:options immutable/>`.
  - Available options:
    - `immutable={true}`
    - `immutable={false}` - default.
    - `accessors={true}`
    - `accessors={false}` - default.
    - `namespace="..."`
    - `customElement="...`
- [<svelte:fragment>](https://learn.svelte.dev/tutorial/svelte-fragment) - place content in a named slot without wrapping it in a container DOM element.

### Module Context

- [Sharing code](https://learn.svelte.dev/tutorial/sharing-code) - `<script context="module> </script>`
  - Code will run once when the module first evaluates.
  - Components talk to each other without any state management.
- [Exports](https://learn.svelte.dev/tutorial/module-exports) - you can't have a default export, because the component is the default export.

### Miscellaneous

- [Debug](https://learn.svelte.dev/tutorial/debug):
  - Inspect logs - `console.log(...)`
  - Pause execution - `(@debug ...}`

## [Part 3: Basic SvelteKit](https://learn.svelte.dev/tutorial/introducing-sveltekit)

SvelteKit's main job boils down to three things:

1. **Routing** - figure out which route matches an incoming request
2. **Loading** - get the data needed by the route
3. **Rendering** - generate HTML (on the server) or update the DOM (in the browser)

### Routing

- [Pages](https://learn.svelte.dev/tutorial/pages) - filesystem-based routing, meaning routes are defined by folders.
  - Every `+page.svelte` file inside `src/routes` creates a page.
  - Navigation is like a single-page app.
- [Layouts](https://learn.svelte.dev/tutorial/layouts) - share UI between pages with `+layout.svelte`.
  - `+layout.svelte` files apply to `child` and `sibling` routes.
- [Route parameters](https://learn.svelte.dev/tutorial/params) - use square brackets around a valid variable name,
  - `src/routes/blog/[slug]/+page.svelte`
  - For multiple route parameters in one segment: `foo/[bar]x[baz]`

### Loading data

- [Page data](https://learn.svelte.dev/tutorial/page-data) - declare `load` function with `+page.server.js`.
- [Layout data](https://learn.svelte.dev/tutorial/layout-data) - `+layout.server.js` loads data for every child route.

### Headers and cookies

- [Setting headers](https://learn.svelte.dev/tutorial/headers) - set response headers with `setHeaders`.
  - Commonly used for customizing caching behavior with `Cache-Control`.
- [Reading and writing cookies](https://learn.svelte.dev/tutorial/cookies):
  - read cookies with `cookies.get(name, options);`.
  - write cookies with `cookies.set(name, value, options);`.
    - explicitly configure path since browsers set it on the parent of current path.
  - SvelteKit sets the following defaults:
    - httpOnly: true
    - secure: true
    - sameSite: lax

### Shared modules

- [The $lib alias](https://learn.svelte.dev/tutorial/lib) - anything inside `src/lib` can be accessed using `$lib`.
  - You can use `$lib` as long as the module is in the `src` folder.
  - "Put code close to where it's used".

### Forms

- [The form element](https://learn.svelte.dev/tutorial/the-form-element) - `<form method="POST"> </form>`
- [Named form actions](https://learn.svelte.dev/tutorial/named-form-actions) - `<form method="POST" action"?/create"> </form>`
  - Most pages need multiple actions.
  - Default actions cannot coexist with named actions.
- [Validation](https://learn.svelte.dev/tutorial/form-validation):
  - HTML form validation like `required`, and so on.
  - Server-side validation.
- [Progressive enhancement](https://learn.svelte.dev/tutorial/progressive-enhancement) - enhance experience with JavaScript, `use:enhance`.
  - App should still be usable when JavaScript is disabled in browsers.
- [Customize use:enhance](https://learn.svelte.dev/tutorial/customizing-use-enhance) - customize by providing callback, `use:enhance={() => {}}`.
  - Useful for adding `pending states` and `optimistic UI`.

### API Routes

- General info:
  - Uses `+server.js` for API route handlers.
  - Request handlers must return a `Response` object.
  - Generating responses with SvelteKit, use `json(data)`.
- [GET handlers](https://learn.svelte.dev/tutorial/get-handlers)
- [POST handlers](https://learn.svelte.dev/tutorial/post-handlers):
  - Use [form actions](https://learn.svelte.dev/tutorial/the-form-element) for most cases, less code and works without JavaScript.
  - Only mutate `data` in a way that you'd get the same result by reloading the page.
- [Other handlers](https://learn.svelte.dev/tutorial/other-handlers): `PUT`, `DELETE`, and so on.

### Stores

- SvelteKit makes three readonly stores available via `$app/stores` module:
  - `page`
  - `navigating`
  - `updated`
- [Page](https://learn.svelte.dev/tutorial/page-store):
  - `url` - the URL of current page
  - `params` - the current page's parameters
  - `route` - object with `id` representing the current route
  - `status` - the HTTP status code of the current page
  - `error` - the error object of the current page
  - `data` - the data of the current page with return values of all `load` functions
  - `form` - the data returned from a `form action`.
- [Navigating](https://learn.svelte.dev/tutorial/navigating-store) - represents the current navigation.
  - `from` and `to` objects with the following properties:
    - `params`
    - `route`
    - `url`
  - `type` - the type of navigation:
    - `link`
    - `popstate`
    - `goto`
- [Updated](https://learn.svelte.dev/tutorial/updated-store) - `true/false`, if a new app version has been deployed since opening the page.
  - Manually check for new versions, `updated.check()`.

### Errors and redirects

- [Basics](https://learn.svelte.dev/tutorial/error-basics) - two types of errors; `expected` and `unexpected` errors.
  - Expected errors:
    - Created with `@sveltejs/kit` error helper.
    - Displays expected error message.
  - Unexpected errors:
    - Any other error like `throw new Error()`.
    - Displays generic `Internal Error`.
    - Can contain sensitive data.
- [Error pages](https://learn.svelte.dev/tutorial/error-pages) - customize error page by using `+error.svelte`.
  - SvelteKit renders an error page on `load` function errors.
- [Fallback errors](https://learn.svelte.dev/tutorial/fallback-errors) - customize fallback error page in `src/error.html` file.
  - Can include:
    - `%sveltekit.status%` - the HTTP status code
    - `%sveltekit.error.message%` - the error message
- [Redirects](https://learn.svelte.dev/tutorial/redirects) - use `throw redirect(...)` to redirect from one page to another.
  - You can use `throw redirect(...)` inside:
    - `load` functions
    - form actions,
    - API routes
    - `handle` hook.
  - Common status codes:
    - `303` - for form actions after successful submission
    - `307` - for temporary redirects
    - `308` - for permanent redirects

## [Part 4: Advanced SvelteKit](https://learn.svelte.dev/tutorial/handle)

### Hooks

- [handle](https://learn.svelte.dev/tutorial/handle) - receives an `event` object and a `resolve` function, returns a`Response` object.
  - in `src/hooks.server.js` file.
- [RequestEvent](https://learn.svelte.dev/tutorial/event) - `event` object passed into `handle`.
  - Passed into API routes, form actions, and `load` functions.
  - Properties and methods:
    - `cookies`
    - `fetch`
    - `getClientAddress()`
    - `isDataRequest`
    - `locals`
    - `params`
    - `request`
    - `route`
    - `setHeaders(...)`
    - `url`
- [handleFetch](https://learn.svelte.dev/tutorial/handlefetch) - `event` object's `fetch` method.
  - Inherits the `cookie` and `authorization` headers from the incoming request.
  - Can make relative requests on the server.
  - Internal requests go directly to the handler function when running on the server.
- [handleError](https://learn.svelte.dev/tutorial/handleerror) - intercept `unexpected` errors.

### Page options

- [Basics](https://learn.svelte.dev/tutorial/page-options):
  - export `page options` from the following:
    - `+page.js`
    - `+page.server.js`
    - `+layout.js`
    - `+layout.server.js`
  - Available options:
    - `ssr` - whether or not pages should be server-rendered
    - `csr` - whether to load the SvelteKit client
    - `prerender` - whether to prerender pages at build time, instead of per-request
    - `trailingSlash` - whether to strip, add, or ignore trailing slashes in URLs
  - Options apply to individual pages if exported from `+page.js` or `+page.server.js`.
  - Options apply to group of pages if exported from `+layout.js` or `+layout.server.js`.
  - Export from root layout to define an option for the whole app.
  - Child layouts and pages override values from parent.
- [ssr](https://learn.svelte.dev/tutorial/ssr) - generates HTML on the server.
  - SvelteKit does SSR by default.
  - Improves performance, resilience, and SEO.
  - Setting `ssr` to `false` in the root `+layout.server.js` turns the app into a SPA.
- [csr](https://learn.svelte.dev/tutorial/csr) - makes pages interactive and update on navigation without a full-page reload.
- [prerender](https://learn.svelte.dev/tutorial/prerender) - generate HTML for a page once, at build time.
  - Serving static data is cheap and performant.
  - Serve large number of users without worrying about `cache-control` headers.
  - Prerendered pages:
    - must not contain `form actions`.
    - must get the same content from the server.
  - Setting `prerenter` to `true` in the root `+layout.server.js` turns SvelteKit to SSG.
- [trailingSlash](https://learn.svelte.dev/tutorial/trailingslash):
  - trailing URL slashes might harm SEO.
  - default value is `never`.
  - add trailing slash with `always`.
  - support both cases with `ignore`.

### Link Options

- [Preloading](https://learn.svelte.dev/tutorial/preload) - preload data or JavaScript to speed up page loads.
  - `data-sveltekit-preload-data`
    - `hover` - default, falls back to `tap` on mobile
    - `tap` - begin preloading on tap
    - `off` - disable preloading
  - `data-sveltekit-preload-code`
    - `eager` - preload everything on the page
    - `viewport` - preload everything as it appears in the viewport
    - `hover` - default
    - `tap`
    - `off`
  - preloading programmatically, import from `$app/navigation`:
    - `preloadData('/foo')`
    - `preloadCode('/bar')`
- [Reloading the page](https://learn.svelte.dev/tutorial/reload) - `data-sveltekit-reload`, to reload when navigating between pages.

### Advanced routing

- [Optional parameters](https://learn.svelte.dev/tutorial/optional-params) - use double brackets for optional parameters, `[[foo]]`.
- [Rest parameters](https://learn.svelte.dev/tutorial/rest-params) - for matching an unknown number of path segments, use `[...rest]`.
  - More specific routes will be tested first, making rest parameters as `catch-all` routes.
- [Param matchers](https://learn.svelte.dev/tutorial/param-matchers) - validate route params with matchers, `/colors/[color=matcher].
  - Matchers run both on the server and in the browser.
- [Route groups](https://learn.svelte.dev/tutorial/route-groups) - group routes using parenthesis, `(authed)/app/+page.svelte`.
  - Useful for grouping routes that need authentication.
  - Use `(authed)/+layout.server.js` to control grouped routes behavior.
  - Use `(authed)/+layout.svelte` to customize grouped routes UI.
- [Breaking out of layouts](https://learn.svelte.dev/tutorial/breaking-out-of-layouts) - break from layout hierarchy by adding `@`, `+page@.svelte`.
  - `src/routes/a/b/c/+page.svelte` inherits every layout above it:
    - `src/routes/+layout.svelte`
    - `src/routes/a/+layout.svelte`
    - `src/routes/a/b/+layout.svelte`
    - `src/routes/a/b/c/+layout.svelte`
  - The root layout applies to every page of your app. You cannot break out of it.

### Advanced loading

- [Universal load functions](https://learn.svelte.dev/tutorial/universal-load-functions) - turn server `load` functions into universal `load` functions.
  - Rename `+page.server.js` file to `+page.js`.
  - Functions run on the server during SSR, but also run in the browser when app hydrates.
  - [Universal vs server docs](https://kit.svelte.dev/docs/load#universal-vs-server).
  - Use cases for universal `load` functions:
    - loading data from external API
    - use in-memory data
    - delay navigation until image has been preloaded
    - return from `load` that can't be serialized
- [Using both load functions](https://learn.svelte.dev/tutorial/using-both-load-functions) - access server data via the `data` property, `data.message`.
  - Data isn't merged, need to explicitly return `message` from universal load function.
- [Using parent data](https://learn.svelte.dev/tutorial/await-parent) - access parent data from `load` functions with `await parent()`.
  - `Universal load` functions can get data from a `parent server load` function.
  - A `server load` function can only get parent data from another `server load` function.
  - Fetch other data that is not dependent on parent data first.
- [Invalidation](https://learn.svelte.dev/tutorial/invalidation) - invalidate specific or pattern URLs in load function with `invalidate(...)`.
- [Custom dependencies](https://learn.svelte.dev/tutorial/custom-dependencies) - specify dependencies with `depends(...)`.
  - Useful when not using `fetch(url)`.
- [invalidateAll](https://learn.svelte.dev/tutorial/invalidate-all) - re-run all `load` functions with `invalidateAll()`.
  - `invalidateAll()` re-runs `load` functions without `url` dependencies.
  - `invalidate(() => true)` does not re-run `load` functions without `url` dependencies.

### Environment Variables

- General info:
  - `static` variables are known at build time.
    - `import { API_KEY } from '$env/static/private`, use variable: `API_KEY.
  - `dynamic` variables read values when the app runs.
    - `import { env } from '$env/dynamic/private`, use variable: `env.API_KEY`.
  - `private` variables Cannot import env variables into `client-side code`.
    - Can only import env variables into server modules:
      - `+page.server.js`
      - `+layout.server.js`
      - `+server.js`
      - any modules ending with `.server.js`
      - any modules inside `src/lib/server`
    - Server modules can only be imported by other server modules.
  - `public` variables can be safely exposed to the browser.
- [$env/static/private](https://learn.svelte.dev/tutorial/env-static-private)
- [$env/dynamic/private](https://learn.svelte.dev/tutorial/env-dynamic-private)
- [$env/static/public](https://learn.svelte.dev/tutorial/env-static-public)
- [$env/dynamic/public](https://learn.svelte.dev/tutorial/env-dynamic-public)