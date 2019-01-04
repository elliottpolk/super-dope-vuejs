# super-dope

## Environment setup - **Assumes nodejs and npm installed**

Ensure that the **vue cli** and CLI dependencies are installed:

```bash

$ npm install -g @vue/cli @vue/cli-init

```

---

## New project setup

It is a good indea to use **webpack** from here. If this is being run / setup 
from behind a proxy (i.e. warnings about a cert may prevent the setup), it might 
need to be run in offline mode

```bash

# replace <project-name> with the actual project name
$ vue init webpack <project-name>

# if working from behind a proxy, need to download the templates first
$ git clone https://github.com/vuejs-templates/webpack ${HOME}/.vue-templates/webpack

# and init via --offline mode, replacing <project-name> with the actual project name
$ vue init webpack <project-name> --offline

```

This will go through a setup wizard for configuring the project. The below
tools / settings are a personal preference.

* Vue build **standalone**
  * this will be the selectable **Runtime + Compiler** option
* Install vue-router? **Yes**
* Use ESLint to lint your code? **Yes**
* Pick an ESLint preset **Standard**
* Set up unit tests **Yes**
* Pick a test runner **jest**
  * this will be the selectable **Jest** - recommended to reduce the amount of
      vulnerabilities
* Setup e2e tests with Nightwatch? **No**
* Should we run \`npm install\` for you after the project has been created?
    (recommeneded) **npm**

## WARNING: 
Some of the default libs use vulnerable versions / dependencies. It's a good idea 
to go through and run the audit process and clean these up (if possible). At the 
time of this writing, the current packages are at issue:

* url-loader@0.5.9
* webpack-dev-server@2.11.3 - updating will cause a breaking change

The builtin `audit fix` tool doesn't work for some of these, so a manual 
intervention is required. Switch to the project directory and perform a little 
cleanup:

```bash

# replace <project-name> with the actual name of the project
$ cd <project-name>

# url-loader
$ npm install --save-dev url-loader@1.1.2

```

---

### SCSS / SASS

Add the SCSS/SASS loader and update the **webconfig.base.conf.js** in `build/webconfig.base.conf.js` 
to allow for the pre-processing ([see](https://vue-loader.vuejs.org/guide/pre-processors.html#sass)...)

```bash

# navigate to the project dir
$ cd <project-name>

$ npm install --save-dev sass-loader node-sass

```

```json

module.exports = {
  module: {
    rules: [
      // ... other rules omitted

      // this will apply to both plain `.scss` files
      // AND `<style lang="scss">` blocks in `.vue` files
      {
        test: /\.scss$/,
        use: [
          'vue-style-loader',
          'css-loader',
          'sass-loader'
        ]
      }
    ]
  },
  // plugin omitted
}

```

## Once the _new_ project is setup, it's ready to run:

```bash

$ npm run dev

```

---

## Run this repo after checkout

```bash

# install dependencies
$ npm install

# run the dev environment
$ npm run dev

```

