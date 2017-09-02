# Getting started

This app is based on the [food-lookup-demo](https://www.fullstackreact.com/articles/using-create-react-app-with-a-server/) from fullstackreact.com.

Our sample app will be a simple food nutrition lookup table. The data driving the app is supplied by the USDA's [National Nutrient Database](https://www.ars.usda.gov/northeast-area/beltsville-md/beltsville-human-nutrition-research-center/nutrient-data-laboratory/docs/usda-national-nutrient-database-for-standard-reference/).

First, git clone this repository and cd into that directory.

This is where the server lives (server.js). Inside of the db folder is a sqlite database containing the nutrition data.


# Server Setup

We now use [Node.js](https://nodejs.org/en/) and the Node Package Manager to install all dependencies for our app. Make sure that you install the latest version of node first. Then use your Terminal, or [Git Bash](https://git-scm.com) under Windows, to run the following npm commands.

## Server Dependencies Installation

Use

```
npm install
```

to install all dependencies & dev-dependecies in a development environment (the default). Later you can use

```
npm install --production
```

or set the NODE_ENV environment variable to production to avoid installing dev-dependencies.

## Test the Server

Let's boot the server:

```
npm run server
```

This server provides a single API endpoint, /api/food. It expects a single parameter, q, the food we are searching for. You can test it with your browser or use the CURL command inside your console:

```
curl localhost:3001/api/food?q=mcflurry
```

Now that we understand how this endpoint works, let's build the front-end application. Kill the server with CTRL+C.


# Frontend Setup

Ensure that you have create-react-app installed globally:

```
npm install -g create-react-app
```

## create-react-app

At the top-level directory of the project we'll create our client app. We want the React app to be in a folder called client, so we'll just use that name in the create-react-app command:

```
create-react-app client
```

This creates a new directory with the following file structure:

```
ls client
README.md
node_modules/
package.json
public/
src/
```

Taking a look at client/package.json, we can see that we just installed react, react-dom, and react-scripts to the /client directory:

```
{
  "name": "client",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^15.6.1",
    "react-dom": "^15.6.1",
    "react-scripts": "1.0.12"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

Inside that directory, we can now run several commands:

> - npm start
>   - Starts the development server.
>
> - npm run build
>   - Bundles the app into static files for production.
>
> - npm test
>   - Starts the test runner.
>
> - npm run eject
>   - Removes this tool and copies build dependencies, configuration files and scripts into the app directory. If you do this, you can’t go back!


### react-scripts

react-scripts is an NPM package specifically for use with create-react-app. It's the "black box" which contains the essentials:

- Dependencies
  - Like Babel, ESLint, and Webpack.
- Configuration
  - Config files for Webpack, Babel and ESLint, both for development and production.
- Scripts
  - For instance, the command react-scripts start runs a script shipped with this package. It's responsible for ultimately booting the Webpack development server.

To see it in action, we can run npm start from inside of this folder:

```
cd client && npm start
```

This will launch a Webpack dev server and should also open localhost:3000 in your browser:

![](./boilerplate-page.png)

We have our API server in the top-level directory and we were able to boot that. And we have our client app down here in client and we're able to boot a server for this.

So the user will direct their browser to localhost:3000, hitting the Webpack dev server. But then how will the React app communicate with our API server?

create-react-app provides a mechanism for working with an API server in development. We can have the Webpack development server proxy requests intended for our API server, like this:

![](./flow-diagram.png)

In this flow, React makes an API request to localhost:3000, the Webpack development server. And then the development server simply proxies that request to the API server, negating any CORS issues.

we need to:
1. launch both the Webpack dev server and the API server in order to run the app locally.
1. we need to get the Webpack dev server to proxy requests intended for our API server.
