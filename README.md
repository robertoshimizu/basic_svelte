# Svelte + TS + Vite

This template should help get you started developing with Svelte and TypeScript in Vite.

## Pnpm Dev to start

```bash
pnpm dev
```

## How Svelte works?

The `main.ts` file configures the `App.svelte` component to be inserted in the body of the `index.html` file. Whenever the server is running and we save a file, there is a quick process of compiling Svelte's files into a pure javascript file, which in turn is imported by `index.html`.

```html
<!-- index.html -->
<body>
  <div id="app"></div>
  <script type="module" src="/src/main.ts"></script>
</body>
```

```typescript
// main.ts
import './app.css'
import App from './App.svelte'

const app = new App({
  target: document.getElementById('app')
})

export default app
```

## Reactivity

Insert javascript variables into HTML content and tag attributes.

We use the same braces `{}` syntax for both cases. Notice the case for `{href}`, used both for attibute and content.

```typescript
<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  const vite_href = 'https://vitejs.dev'
  const git_href = "https://github.com/sveltejs/kit#readme"
  const href='https://svelte.dev'
</script>

<main>
  <div>
    <a href={vite_href} target="_blank" rel="noreferrer">
      <img src="/vite.svg" class="logo" alt="Vite Logo" />
    </a>
    <a {href} target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href={git_href} target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>
```

## Bind Values

```typescript
<script lang="ts">
  let value = 'antonio';
</script>

<input type="text" bind:value={value}>
```

Short version

```typescript
<input type="text" bind:value>
```

## Technical considerations

**Why use this over SvelteKit?**

- It brings its own routing solution which might not be preferable for some users.
- It is first and foremost a framework that just happens to use Vite under the hood, not a Vite app.

This template contains as little as possible to get started with Vite + TypeScript + Svelte, while taking into account the developer experience with regards to HMR and intellisense. It demonstrates capabilities on par with the other `create-vite` templates and is a good starting point for beginners dipping their toes into a Vite + Svelte project.

Should you later need the extended capabilities and extensibility provided by SvelteKit, the template has been structured similarly to SvelteKit so that it is easy to migrate.

**Why `global.d.ts` instead of `compilerOptions.types` inside `jsconfig.json` or `tsconfig.json`?**

Setting `compilerOptions.types` shuts out all other types not explicitly listed in the configuration. Using triple-slash references keeps the default TypeScript setting of accepting type information from the entire workspace, while also adding `svelte` and `vite/client` type information.

**Why include `.vscode/extensions.json`?**

Other templates indirectly recommend extensions via the README, but this file allows VS Code to prompt the user to install the recommended extension upon opening the project.

**Why enable `allowJs` in the TS template?**

While `allowJs: false` would indeed prevent the use of `.js` files in the project, it does not prevent the use of JavaScript syntax in `.svelte` files. In addition, it would force `checkJs: false`, bringing the worst of both worlds: not being able to guarantee the entire codebase is TypeScript, and also having worse typechecking for the existing JavaScript. In addition, there are valid use cases in which a mixed codebase may be relevant.

**Why is HMR not preserving my local component state?**

HMR stands for Hot Module Replacement. It is a tool that is used during development to replace only the parts that have changed in a running application, without the need to reload the whole browser page.

HMR state preservation comes with a number of gotchas! It has been disabled by default in both `svelte-hmr` and `@sveltejs/vite-plugin-svelte` due to its often surprising behavior. You can read the details [here](https://github.com/rixo/svelte-hmr#svelte-hmr).

If you have state that's important to retain within a component, consider creating an external store which would not be replaced by HMR.

```ts
// store.ts
// An extremely simple external store
import { writable } from 'svelte/store'
export default writable(0)
```
