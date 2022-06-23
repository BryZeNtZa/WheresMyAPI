#Requirements#

- Node.js version ≥ v12.x installed in your local development environment
- Access to a package manager like npm or Yarn
- Basic knowledge of Node.js and Express

#Project init: package.json#

- mkdir xdev.bdm-fmw
- cd xdev.bdm-fmw
- npm init --yes

Rmq: --yes flag uses de default settings you have set up from your npm config

# Create a minimal server with Express#

- npm install express dotenv
Rmq: the dotenv package is useful for reading .env files

- Create the .env file with the following content
    PORT=8000

- create the application entry point index.js

    const express = require('express');
    const dotnev = require('dotenv');

    dotenv.config();

    const app = express();
    const port = process.env.PORT;

    app.get('/', (req, res) => {
    res.send('Express + TypeScript Server');
    });

    app.listen(port, () => {
    console.log(`[server]: Server is running at https://localhost:${port}`);
    });

# Installing TypeScript
- npm i -D typescript @types/express @types/node

Rmq: -D means we are installing TypeScript as a dev dependecy

#Generating tsconfig.json
- npx tsc --init

#Convert the index.js to index.ts
Now, you can easily convert the minimal server code in index.js to an index.ts file.

# Watching file changes and build directory

nodemon is a development-related utility library for tracking file changes when coding and automatically restart the NodeJS server.
So we first install Concurrently library, which allows us to run multiple commands.

- npm install -D concurrently nodemon

After installing these dev dependencies, update the scripts in the package.json file:

{
  "scripts": {
    "build": "npx tsc",
    "start": "node dist/index.js",
    "dev": "concurrently \"npx tsc --watch\" \"nodemon -q dist/index.js\""
  }
}

The build command will compile the code in JavaScript inside a dist directory.
The dev command is used to run the Node.js server in development mode.

Now, go back to the terminal window and run npm run dev to trigger the development server:


#Install eslint and prettier and configure them to avoid conflicts
-------------------------------------------------------------------

ESLint and Prettier are code writting assisting tools that help write better code and catch error while coding.

- npm i -D eslint prettier
- install VScode extension of EsLint and Prettier
- configure ESlint: we are going to use coding recommandations from AirBnB
See the AirBnB coding standards here: https://github.com/airbnb/javascript
- Initialize Eslint by typing the following command line: 
  > npx eslint --init ( You can also run this command directly using '> npm init @eslint/config')
  Answer all the configs questions and choose airbnb as you coding style guide and JSON as the configs format
  After this step you must be able to see a new file created: .eslintrc.json

  In case npx eslint --init command does not prompt you to choose a coding standard (so that you can choose airbnb),
  then install it manually this way:
  > npx install-peerdeps --dev eslint-config-airbnb

- you can now do:
    > npx eslint ./src/*
    to analyze the code under the ./src directory

Dive deep into ESlint configuration: https://eslint.org/docs/user-guide/configuring/

# Configure Prettier
We are going to configure Prettier to have upper hand on ESlint
- create the Prettier config file: .prettierrc
- install Eslint configurator for prettier, and prettier plugin for EsLint :
  > npm install --save-dev eslint-config-prettier eslint-plugin-prettier
  In the .eslintrc.json : 
   add prettier in the extends entry and in the plugin entry
   also add prettier into the rules entry

  {
    ...
    "extends": [
        "airbnb-base", 
        "prettier"
    ]
    ...
     "plugins": [
        "@typescript-eslint",
        "prettier"
    ],
    "rules": {
        "pretier/prettier": "error"
    }
  }


https://blog.logrocket.com/how-to-set-up-node-typescript-express/
https://www.typescriptlang.org/docs/handbook/modules.html


# DATABASE Access
-----------------

# Install TypeORM, reflect-metadata, and MysQL2
> npm install typeorm --save
> npm install reflect-metadata --save
> npm install mysql2 --save