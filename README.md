# Getting started

This app is based on the [food-lookup-demo](https://www.fullstackreact.com/articles/using-create-react-app-with-a-server/) from fullstackreact.com.

Our sample app will be a simple food nutrition lookup table. The data driving the app is supplied by the USDA's [National Nutrient Database](https://www.ars.usda.gov/northeast-area/beltsville-md/beltsville-human-nutrition-research-center/nutrient-data-laboratory/docs/usda-national-nutrient-database-for-standard-reference/).

First, git clone this repository and cd into that directory.

This is where the server lives (server.js). Inside of the db folder is a sqlite database containing the nutrition data.


# Server Setup

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
curl localhost:3001/api/food?q=hash+browns
```

Now that we understand how this endpoint works, let's build the front-end application. Kill the server with CTRL+C.
