## Overview 

<details><summary>What is Svelte?</summary>

Svelte is a tool for building web applications. Like other user interface frameworks, it allows you to build your app declaratively out of components that combine markup, styles and behaviours.

These components are compiled into small, efficient JavaScript modules that eliminate overhead traditionally associated with UI frameworks.

You can build your entire app with Svelte (for example, using an application framework like [SvelteKit](https://kit.svelte.dev/docs/introduction), which this tutorial will cover), or you can add it incrementally to an existing codebase. You can also ship components as standalone packages that work anywhere.
</details>
<details><summary>Will Cover in 4 main parts :</summary>

1. Basic Svelte 

2. Advanced Svelte

3. Basic SvelteKit

4. Advanced SvelteKit

</details>

### 1. Basic Svelte

<details><summary>Introduction</summary>

- Dynamic attributes 
- Styling 
- Nested components 
- HTML Tags 
</details>

<details><summary>Reactivity</summary>

- Assignments 
- Declarations 
- Statements
- Updating arrays and objects 

</details>

<details><summary>Props</summary>

- Declaring props 
- Default values
- Spread props 

</details>

<details><summary>Logic</summary>

- If blocks
- Else blocks 
- Else-if blocks 
- Each blocks 
- Keyed each blocks
- Await blocks 

</details>

<details><summary>Events</summary>

- DOM events
- Inline handlers
- Event modifiers
- Component events
- Event Forwarding
- DOM event forwarding

</details>

<details><summary>Bindings</summary>

- Text inputs
- Numeric inputs
- Checkbox inputs
- Select bindings 
- Group inputs
- Select multiple 
- Textarea inputs 

</details>

<details><summary>Lifecycle</summary>

- onMount 
- beforeUpdate and afterUpdate
- tick

</details>

<details><summary>Stores</summary>

- Writable stores 
- Auto-subscriptions
- Readable stores
- Derived stores
- Custom stores 
- Store bindings 

</details>

### 2. Advanced Svelte

<details><summary>Motion</summary>
 
- Tweens
- Springs

</details>

<details><summary>Transitions</summary>

- The transition directive
- Adding parameters
- In and out
- Custom CSS transitions
- Custom JS transitions
- Transition events
- Global transition
- Key blocks
- Deferred transitions 

</details>

<details><summary>Animations</summary>

- The animate directive

</details>

<details><summary>Actions</summary>

- The use directive
- Adding parameters

</details>

<details><summary>Advanced bindings</summary>

- Contenteditable bindings
- Each block bindings
- Media elements
- Dimensions
- This 
- Component bindings
- Binding to component instances

</details>

<details><summary>Classes and Styles</summary>

- The class directive
- Shorthand class directive
- The style directive
- Component styles

</details>

<details><summary>Component composition</summary>

- Slots
- Named slots
- Slot fallbacks
- Slot props
- Checking for slot content 

</details>

<details><summary>Context API</summary>

- setContext and getContext

</details>

<details><summary>Special elements</summary>

- `<svelte:self>`
- `<svelte:component>`
- `<svelte:element>`
- `<svelte:window>`
- `<svelte:window>` bindings
- `<svelte:body>`
- `<svelte:document>`
- `<svelte:head>`
- `<svelte:options>`
- `<svelte:fragment>`

</details>

<details><summary>Module context</summary>

- Sharing code
- Exports

</details>

<details><summary>Miscellaneous</summary>

- The @debug tag

</details>


### 3. Basic SvelteKit

<details><summary>Introduction</summary>

- Whereas Svelte is a component framework, SvelteKit is an app framework (or 'metaframework', depending on who you ask) that solves the tricky problems of building something production-ready:

    - Routing
    - Server-side rendering
    - Data fetching
    - Service workers
    - TypeScript integration
    - Prerendering
    - Single-page apps
    - Library packaging
    - Optimised production builds
    - Deploying to different hosting providers
    - ...and so on

- SvelteKit apps are server-rendered by default (like traditional 'multi-page apps' or MPAs) for excellent first load performance and SEO characteristics, but can then transition to client-side navigation (like modern 'single-page apps' or SPAs) to avoid jankily reloading everything (including things like third-party analytics code) when the user navigates. They can run anywhere JavaScript runs, though — as we'll see — your users may not need to run any JavaScript at all.

</details>

<details><summary>Routing</summary>

- Pages
- Layouts
- Route Parameters

</details>

<details><summary>Loading data</summary>

- Page data 
- Layout data

</details>

<details><summary>Headers and cookies</summary>

- Setting headers
- Reading and writing cookies

</details>


<details><summary>Shared modules</summary>

- The `$lib`  alias 

</details>
<details><summary>Forms</summary>

- The `<form>` element
- Named form actions
- Validation
- Progressive enhancement
- Customizing use:enhance

</details>

<details><summary>API routes</summary>

- GET handlers
- POST handlers
- Other handlers

</details>
<details><summary>Stores</summary>

- Page
- Navigating
- updated

</details>
<details><summary>Errors and redirects</summary>

- Basics 
- Error pages
- Fallback errors
- Redirects

</details>

### 4. Advanced SvelteKit 

<details><summary>Hooks</summary>

- handle
- The RequestEvent object
- handleFetch
- handleError

</details>
<details><summary>Page options</summary>

- Basics 
- ssr
- csr
- prerender
- trailingSlash

</details>
<details><summary>Link options</summary>

- Preloading
- Reloading the page

</details>
<details><summary>Advanced routing</summary>

- Optional parameters
- Rest parameters
- Param matchers
- Route groups 
- Breaking out of layouts

</details>
<details><summary>Advanced loading</summary>

- Universal load functions
- Using both load functions 
- Using parent data 
- Invalidation
- Custom dependencies
- InvalidateAll

</details>
<details><summary>Environment variables</summary>

- `$env/static/private`
- `$env/dynamic/private`
- `$env/static/public`
- `$env/dynamic/public`

</details>


> _This doc only contains to be covered Key points_















