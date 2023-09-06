# Remix Integration with Formbricks

This repository is an example of how to integrate Formbricks with a Remix application.


## Setup Instructions we Followed

1. Created a new Remix application:

   ```sh
   npx create-remix@latest
   ```

2. Navigated to the created application directory:

   ```sh
   cd remix
   ```

3. Installed existing dependecies:

   ```sh
   npm install
   ```

4. Installed the Formbricks JS library:

   ```sh
   npm install --save @formbricks/js
   ```

5. Added the below in my [app/root.tsx](./app/root.tsx) file:

   ```js
   import formbricks from "@formbricks/js";

   if (typeof window !== "undefined") {
      formbricks.init({
         environmentId: "<environment-id>",
         apiHost: "<api-host>",
         debug: true, // remove when in production
      });
   }
   ```

6. Edited the Formbricks Enviornment ID and API Host

7. Start the React development server:

   ```sh
   npm dev
   ```

With these steps, we had a running Remix application with Formbricks integrated.
