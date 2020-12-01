<h1 align="center">🌐 Adam's Opinionated Sapper Template</h1>

Forked from babichjacob [@babichjacob](https://github.com/babichjacob)'s [`Opinionated Sapper`](https://github.com/babichjacob/sapper-firebase-typescript-graphql-tailwindcss-actions-template)

- [Sapper for Svelte](https://sapper.svelte.dev/)
  - [Official VS Code Extension](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)
- [Firebase](https://firebase.google.com/)
  - [Functions](https://firebase.google.com/docs/functions/) for Server Side Rendering (SSR)
  - [Hosting](https://firebase.google.com/docs/hosting) for static assets
  - Thanks to [@Eckhardt-D](https://github.com/Eckhardt-D)'s [`sapper-firebase-starter`](https://github.com/Eckhardt-D/sapper-firebase-starter)
  - Thanks to [@nhristov](https://github.com/nhristov)'s [`sapper-template-firebase`](https://github.com/nhristov/sapper-template-firebase)
- [TypeScript](https://www.typescriptlang.org/)
  - [TypeGraphQL](https://typegraphql.com/)
  - Inside Svelte components, thanks to [`svelte-preprocess`](https://github.com/kaisermann/svelte-preprocess)
- [SCSS](https://github.com/sveltejs/svelte-preprocess)
- [Materialify](https://svelte-materialify.vercel.app/)
- [DND](https://github.com/isaacHagoel/svelte-dnd-action)
- [PostCSS](https://postcss.org/)
  - [Tailwind CSS](https://tailwindcss.com/)
    - [Official VS Code Extension](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
  - [postcss-import](https://github.com/postcss/postcss-import)
  - [PurgeCSS](https://www.purgecss.com/)
  - [CSSNano](https://cssnano.co/)
  - Inside Svelte components, thanks to [`svelte-preprocess`](https://github.com/kaisermann/svelte-preprocess)
- [GitHub Actions](https://github.com/features/actions)
  - Automatic building and deployment to Firebase, triggered on commits to `main` or `master`
- [Progressive Web App (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) best practices set up
  - [`manifest.json`](https://developer.mozilla.org/en-US/docs/Web/Manifest)'s most important fields filled out
  - High [Lighthouse](https://developers.google.com/web/tools/lighthouse) audit score
- [ESLint](https://eslint.org/)
  - [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
  - `eslint:fix` package script

This template comes from combining two of my smaller ones: [one for Tailwind CSS (PostCSS)](https://github.com/babichjacob/sapper-postcss-template), and [another for TypeScript and GraphQL](https://github.com/babichjacob/sapper-typescript-graphql-template). If this is too much for you, check out one of those!

### ⬇️ Install Dependencies

You need to be using version 12 or higher of Node; the `package.json` `engines` field only specifies `10` for Cloud Functions for Firebase.

```sh
yarn  # pnpm also works
```

## 🛠 Usage

### 🧪 Development

```sh
yarn dev
```

### 🔥 Deployment to Firebase

This will create a production build for you before deploying.

```sh
yarn deploy
```

### 🔨 Testing Production Builds Locally

This probably pairs well with [Firebase Emulators](https://firebase.google.com/docs/rules/emulator-setup).

```sh
yarn prod
yarn start
```

### 📦 Deploying a Static Site to Firebase Hosting

Cloud Functions for Firebase [requires billing set up with the Blaze Plan](https://firebase.google.com/support/faq#expandable-15), but you can stay on the Spark Plan for a free and fast (no cold starts!) static site:

```sh
yarn deploy:export
```

This will create an exported build for you before deploying.

If your project is transitioning from SSR to a static site, be sure to delete the residual `ssr` Cloud Function:

```sh
yarn firebase functions:delete ssr
```

You will also need to remove `rewrites` from `firebase.json`.

## ⚙ Configuration

### 🔥 Firebase and 🐙 GitHub Actions

The least you should need to do to get started is to edit `.firebaserc`, changing the project ID to _your_ project (initialized in the [Firebase console](https://console.firebase.google.com/)) ID.

For automatic building and deployment to work, you need to generate [a CI login token from Firebase](https://firebase.google.com/docs/cli#cli-ci-systems):

```sh
yarn firebase login:ci
```

Then, go to your repository's Settings > Secrets. Copy the result of the command above and save it as a Secret named `FIREBASE_TOKEN`.

You can test if it's working by making a commit to `main` or `master` and checking the Actions tab of your repository to see if your project successfully builds and deploys to Firebase.

### ⚡ Web app

Many of the fields in `static/manifest.json` (`short_name`, `name`, `description`, `categories`, `theme_color`, and `background_color`) are filled with demonstrative values that won't match your site. Similarly, you've got to take new screenshots to replace the included `static/screenshot-1.png` and `static/screenshot-2.png` files. If you want, you can add [app shortcut definitions for "add to home screen" on Android](https://web.dev/app-shortcuts/#define-app-shortcuts-in-the-web-app-manifest). Once you change `theme_color`, update the `meta name="theme-color"` tag in `src/template.html` to match.

The [Apple touch icon](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html), favicon, and `logo-` files (also all in the `static` directory) are created by placing the logo within a "safe area" centered circle that takes up 80% of the canvas's dimension. For instance, the constraining circle in `logo-512.png` is 512 × 0.80 = 409.6 ≈ 410 pixels wide and tall.

### 🗺 Source maps

This project base comes with [source maps](https://blog.teamtreehouse.com/introduction-source-maps) enabled during development and disabled during production for the best compromise between performance and developer experience. You can change this behavior through the `sourcemap` variable in `rollup.config.js`.

### 💨 Optionally removing Tailwind CSS (and PurgeCSS)

1. Remove all Tailwind imports in the `src/global.pcss` file
2. Remove these lines in `postcss.config.js`:
   1. ```js
      const tailwindcss = require("tailwindcss");
      ```
   2. ```js
      const tailwindcssConfig = require("./tailwind.config");
      ```
   3. ```js
      tailwindcss(tailwindcssConfig),
      ```
3. Delete the `tailwind.config.js` file
4. Uninstall the `tailwindcss` package

### 🕸 Optionally removing the GraphQL server

1. Remove these lines in `src/server.ts`:

   1. ```ts
      import { createApolloServer } from "./graphql";
      ```
   2. ```ts
      const apolloServer = await createApolloServer();
      ```
   3. ```ts
      apolloServer.applyMiddleware({ app, path: graphqlPath });
      ```

2. Remove the now-useless `graphqlPath` parameter to `createSapperAndApolloServer` in `src/server.ts`. This is also a good opportunity to rename the function since there is no longer an Apollo Server; if you do rename it, then also update the reference in `/index.js` or your Cloud Functions will still be referring to the old (now non-existent) function

3. Delete the `src/graphql` folder

4. Uninstall the `apollo-server-express`, `bufferutil`, `class-validator`, `graphql`, `reflect-metadata`, `type-graphql`, and `utf-8-validate` packages

5. Remove the now-error-causing
   ```yaml
   - name: "Delete the Unexportable GraphQL Page"
     run: "rm __sapper__/export/graphql"
   ```
   task in `.github/workflows/build-and-deploy.yml`
