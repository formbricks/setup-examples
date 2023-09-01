# SvelteKit Integrttion with Formbricks

This folder is an example for integrating Formbricks with a SvelteKit application.

## Instructions

1. Create a new SvelteKit application:

   ```sh
   npm create svelte@latest
   ```

2. Navigate to the created application directory:

   ```sh
    cd <your app>
   ```

3. Install existing dependecies:

   ```sh
   npm install
   ```

4. Install the Formbricks JS library:

   ```sh
    npm install --save @formbricks/js
   ```

5. Create a Formbricks component to [lib/components/Formbricks.svelte](./lib/components/Formbricks.svelte) and add the below to it:

   ```svelte
   <script lang="ts">
       import { navigating } from '$app/stores';
       import { env } from '$env/dynamic/public';
       import type fbT from '@formbricks/js';
       import { onMount } from 'svelte';

       let formbricks: typeof fbT;

       onMount(() => {
           import('@formbricks/js').then((fb) => {
           formbricks = fb.default;
           formbricks.init({
               environmentId: env.PUBLIC_FORMBRICKS_ENVIRONMENT_ID || 'not set',
               apiHost: 'https://app.formbricks.com', // Cloud Hosted API
               debug: import.meta.env.DEV,
           });

           (window as any).formbricks = formbricks;
           });
       });

       $: if ($navigating) formbricks.registerRouteChange();
   </script>
   ```

6. Create a .env file at the root of your project and add the below to it:

   ```sh
   PUBLIC_FORMBRICKS_ENVIRONMENT_ID=<your environment id>
   ```

   By default it will use the Cloud Hosted instance. If you want to use a self-hosted instance, you need to modify the code a little bit in the formbricks component.

7. Use the component in +layout.svelte:

   ```svelte
   <script lang="ts">
       import Formbricks from '$lib/components/Formbricks.svelte';
   </script>

   <Formbricks />
   ```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
