# VueJs Integration with Formbricks

This repository is an example of how to integrate Formbricks with a VueJs application.

For a comprehensive step-by-step guide to integrate Formbricks in your app, please refer to the official [Formbricks VueJs Guide](https://formbricks.com/docs/getting-started/framework-guides#vue-js).

## Setup Instructions we Followed

1. Created a new Vue application:

   ```sh
   npm create vue@latest
   ```

2. Navigated to the created application directory:

   ```sh
   cd vuejs
   ```

3. Installed existing dependecies:

   ```sh
   npm install
   ```

4. Installed the Formbricks JS library:

   ```sh
   npm install --save @formbricks/js
   ```

5. Created an [app/formbricks.tsx](./src/formbricks.js) file and added the below to it:

   ```js
   import formbricks from '@formbricks/js'

   if (typeof window !== 'undefined') {
     formbricks.init({
       environmentId: '<environment-id>',
       apiHost: '<api-host>'
     })
   }

   export default formbricks
   ```

6. Edited the Formbricks Enviornment ID and API Host

7. Imported Formbricks in the [src/main.ts](./src/main.ts) file:

   ```ts
   // other imports
   import formbricks from '@/formbricks'

   const app = createApp(App)

   app.use(router)

   app.mount('#app')

   router.afterEach((to, from) => {
     if (typeof formbricks !== 'undefined') {
       formbricks.registerRouteChange()
     }
   })
   ```

8. Started the Vue development server:

   ```sh
   npm run dev
   ```

With these steps, we had a running VueJs application with Formbricks integrated.
