## GETTING STARTED

### Creating a project

The easiest way to start building a SvelteKit app is to run `npm create` :

```bash
npm create svelte@latest first-app
cd first-app
npm install
npm run dev
```

The first command will scaffold a new project in the first-app directory asking you if you'd like to set up some basic tooling such as TypeScript. See [integrations](https://kit.svelte.dev/docs/integrations) for pointers on setting up additional tooling. The subsequent commands will then install its dependencies and start a server on [localhost:5173](localhost:5173).

- There are two basic concepts:

    - Each page of your app is a [Svelte](https://svelte.dev/) component
    - You create pages by adding files to the `src/routes` directory of your project. These will be server-rendered so that a user's first visit to your app is as fast as possible, then a client-side app takes over


### Editor setup 

- Use [Visual Studio Code (aka VSCode)](https://code.visualstudio.com/download) with [the Svelte extension](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)


### Project structure

- A typical SvelteKit project looks like this:

```tree
my-project/
├ src/
│ ├ lib/
│ │ ├ server/
│ │ │ └ [your server-only lib files]
│ │ └ [your lib files]
│ ├ params/
│ │ └ [your param matchers]
│ ├ routes/
│ │ └ [your routes]
│ ├ app.html
│ ├ error.html
│ ├ hooks.client.js
│ ├ hooks.server.js
│ └ service-worker.js
├ static/
│ └ [your static assets]
├ tests/
│ └ [your tests]
├ package.json
├ svelte.config.js
├ tsconfig.json
└ vite.config.js
```

> You'll also find common files like `.gitignore` and `.npmrc` (and `.prettierrc` and `eslint.config.js` and so on, if you chose those options when running `npm create svelte@latest` ).


### Project files 

#### src 

The `src` directory contains the meat of your project. Everything except `src/routes` and `src/app.html` is optional.

- `lib` contains your library code (utilities and components), which can be imported via the `$lib` alias, or packaged up for distribution using [svelte-package](https://kit.svelte.dev/docs/packaging)
    - `server` contains your server-only library code. It can be imported by using the [`$lib/server`](https://kit.svelte.dev/docs/server-only-modules) alias. SvelteKit will prevent you from importing these in client code.

- `params` contains any [`param matchers`](https://kit.svelte.dev/docs/advanced-routing#matching) your app needs

- `routes` contains the [`routes`](https://kit.svelte.dev/docs/routing) of your application. You can also colocate other components that are only used within a single route here

- `app.html` is your page template — an HTML document containing the following placeholders:

    - `%sveltekit.head%` — `<link>` and `<script>` elements needed by the app, plus any `<svelte:head>` content

    - `%sveltekit.body%` — the markup for a rendered page. This should live inside a `<div>` or other element, rather than directly inside `<body>`, to prevent bugs caused by browser extensions injecting elements that are then destroyed by the hydration process. SvelteKit will warn you in development if this is not the case

    - `%sveltekit.assets%` — either [`paths.assets`](https://kit.svelte.dev/docs/configuration#paths), if specified, or a relative path to [`paths.base`](https://kit.svelte.dev/docs/configuration#paths)

    - `%sveltekit.nonce%` — a [CSP](https://kit.svelte.dev/docs/configuration#csp) nonce for manually included links and scripts, if used

    - `%sveltekit.env.[NAME]%` - this will be replaced at render time with the `[NAME]` environment variable, which must begin with the [publicPrefix](https://kit.svelte.dev/docs/configuration#env) (usually `PUBLIC_`). It will fallback to `''` if not matched.

- `error.html` is the page that is rendered when everything else fails. It can contain the following placeholders:
    - `%sveltekit.status%` — the HTTP status

    - `%sveltekit.error.message%` — the error message

- `hooks.client.js` contains your client [hooks](https://kit.svelte.dev/docs/hooks)

- `hooks.server.js` contains your server [hooks](https://kit.svelte.dev/docs/hooks)

- `service-worker.js` contains your [service worker](https://kit.svelte.dev/docs/service-workers)



#### static

Any static assets that should be served as-is, like `robots.txt` or `favicon.png`, go in here.

#### tests

If you added [Playwright](https://playwright.dev/docs/intro) for browser testing when you set up your project, the tests will live in this directory.

#### package.json 

Your `package.json` file must include `@sveltejs/kit`, `svelte` and `vite` as `devDependencies`.

When you create a project with `npm create svelte@latest`, you'll also notice that `package.json` includes `"type": "module"`. This means that `.js` files are interpreted as native JavaScript modules with `import` and `export` keywords. Legacy CommonJS files need a `.cjs` file extension.

#### svelte.config.js

This file contains your Svelte and SvelteKit [configuration](https://kit.svelte.dev/docs/configuration).

#### tsconfig.json

This file (or `jsconfig.json`, if you prefer type-checked `.js` files over `.ts` files) configures TypeScript, if you added typechecking during `npm create svelte@latest`. Since SvelteKit relies on certain configuration being set a specific way, it generates its own `.svelte-kit/tsconfig.json` file which your own config `extends`.

#### vite.config.js

A SvelteKit project is really just a [Vite](https://vitejs.dev/guide/) project that uses the [`@sveltejs/kit/vite`](https://kit.svelte.dev/docs/modules#sveltejs-kit-vite) plugin, along with any other [Vite configuration](https://vitejs.dev/config/).

### Other files

#### .svelte-kit

As you develop and build your project, SvelteKit will generate files in a `.svelte-kit` directory (configurable as [outDir](https://kit.svelte.dev/docs/configuration#outdir)). You can ignore its contents, and delete them at any time (they will be regenerated when you next `dev` or `build`).


### Web standards

- standard [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) that SvelteKit builds on top of.

- During development, and in [adapters](https://kit.svelte.dev/docs/adapters) for Node-based environments (including AWS Lambda), they're made available via polyfills where necessary (for now, that is — Node is rapidly adding support for more web standards).

In particular, you'll get comfortable with the following:

#### Fetch APIs 

SvelteKit uses [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Window/fetch) for getting data from the network. It's available in [hooks](https://kit.svelte.dev/docs/hooks) and [server routes](https://kit.svelte.dev/docs/routing#server) as well as in the browser.

> A special version of `fetch` is available in [load](https://kit.svelte.dev/docs/load) functions, [server hooks](https://kit.svelte.dev/docs/hooks#server-hooks) and [API routes](https://kit.svelte.dev/docs/routing#server) for invoking endpoints directly during server-side rendering, without making an HTTP call, while preserving credentials. (To make credentialled fetches in server-side code outside load, you must explicitly pass `cookie` and/or `authorization` headers.) It also allows you to make relative requests, whereas server-side `fetch` normally requires a fully qualified URL.

Besides fetch itself, the [Fetch API](
https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) includes the following interfaces:
- Request :

    - An instance of [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) is accessible in [hooks](https://kit.svelte.dev/docs/hooks) and [server routes](https://kit.svelte.dev/docs/routing#server) as `event.request`. It contains useful methods like `request.json()` and `request.formData()` for getting data that was posted to an endpoint.


- Response

    - An instance of [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) is returned from `await fetch(...)` and handlers in `+server.js` files. Fundamentally, a SvelteKit app is a machine for turning a `Request` into a `Response`.


- Headers 

    - The [Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers) interface allows you to read incoming `request.headers` and set outgoing `response.headers`. For example, you can get the `request.headers` as shown below, and use the [json convenience function](https://kit.svelte.dev/docs/modules#sveltejs-kit-json) to send modified `response.headers`:

    ```js
    src/routes/what-is-my-user-agent/+server.js

    import { json } from '@sveltejs/kit';
    /** @type {import('./$types').RequestHandler} */
    export function GET({ request }) {	
        // log all headers	
        console.log(...request.headers);
        
        // create a JSON Response using a header we received	
        return json({		
            // retrieve a specific header		
            userAgent: request.headers.get('user-agent')	
        }, {		
            // set a header on the response		
            headers: { 'x-custom-header': 'potato' }	
    });}

    ```

#### FormData 

When dealing with HTML native form submissions you'll be working with [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) objects.

```js
src/routes/hello/+server.js
import { json } from '@sveltejs/kit';
/** @type {import('./$types').RequestHandler} */
export async function POST(event) {	
    const body = await event.request.formData();
	// log all fields	
    console.log([...body]);
	return json({		
        // get a specific field's value		
        name: body.get('name') ?? 'world'	
    });
}
```

#### Stream APIs 

Most of the time, your endpoints will return complete data, as in the userAgent example above. Sometimes, you may need to return a response that's too large to fit in memory in one go, or is delivered in chunks, and for this the platform provides [streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) — [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream), [WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream) and [TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream).


#### URL APIs 

URLs are represented by the [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL) interface, which includes useful properties like `origin` and `pathname` (and, in the browser, hash). This interface shows up in various places — `event.url` in [hooks](https://kit.svelte.dev/docs/hooks) and [server routes](https://kit.svelte.dev/docs/routing#server), [$page.url](https://kit.svelte.dev/docs/modules#$app-stores) in [pages](https://kit.svelte.dev/docs/routing#page), from and to in [beforeNavigate](https://kit.svelte.dev/docs/modules#$app-navigation-beforenavigate) and [afterNavigate](https://kit.svelte.dev/docs/modules#$app-navigation-afternavigate) and so on.


#### URLSearchParams

Wherever you encounter a URL, you can access query parameters via `url.searchParams`, which is an instance of [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams):

```js
const foo = url.searchParams.get('foo');

```

#### Web Crypto 

The [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API) is made available via the `crypto` global. It's used internally for [Content Security Policy](https://kit.svelte.dev/docs/configuration#csp) headers, but you can also use it for things like generating UU

```js
const uuid = crypto.randomUUID();

```






