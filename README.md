# Example Svelte app with Solid Authentication

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template-webpack.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template-webpack svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*

## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
npm install buffer @inrupt/solid-client-authn-browser @inrupt/solid-client dotenv-webpack
```

In the `webpack.config.js` add a fallback for the Buffer library:

```
resolve: {
	fallback: {
			"Buffer": require.resolve('buffer/'),
	}
```

Add the `dotenv-webpack` also:

```
const Dotenv = require('dotenv-webpack');

plugins: [
    ...
    ...
    new Dotenv(),
]
```

Add an `env` file with content:

```
REDIRECT_URL=http://localhost:8080/
```

...then start webpack:

```bash
npm run dev
```

Navigate to [localhost:8080](http://localhost:8080). You should see your app running. Edit a component file in `src`, save it, and the page should reload with your changes.


## Deploying to the web

```bash
npm run build
```

And copy these files on your webserver.
