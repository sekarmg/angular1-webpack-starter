#introduction
[![Build Status](https://travis-ci.org/sekarmg/karmasoc-webui.svg?branch=master)](https://travis-ci.org/sekarmg/karmasoc-webui)
[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)

# Mock Startup project for karmasoc

This is karmasoc webui project that uses following stack.

Stack
-----

- NPM
- Webpack
- Angular 1.5
- Angular UI Router (with self-registering components)
- ES 6 / Babel (Module Loading)
- SASS
- Jade
- Tests
  - Karma (Test Runner, http://karma-runner.github.io/)
  - Mocha (Test Framework, http://mochajs.org/)
  - Chai (BDD/TSS assertion library, http://chaijs.com/)

Requirements
------------

- ES 6 with Angular 1.4
- Webpack Bundling
- SASS support
- Angular UI Router
- Self-registering components
- Jade support
- Typescript


## Usage

Development
-----------

Create a JS bundle with Webpack::

  $ npm run build

Start the Webpack development server on 'localhost:9000'::

  $ npm run start

Run tests::

  $ npm run test

Linting::

  $ npm run lint


HTML Webpack Plugin
-------------------

Installation::

  $ npm install html-webpack-plugin --save-dev

webpack.config.js::

  var HtmlWebpackPlugin = require('html-webpack-plugin')

  module.exports = {
    ...
    plugins: [
      new HtmlWebpackPlugin({
        title: 'Website Starter',
        template: 'src/index.html',
        minify: {
          collapseWhitespace: true,
          removeComments: true,
          removeRedundantAttributes: true,
          removeScriptTypeAttributes: true,
          removeStyleLinkTypeAttributes: true
        }
      })
    ],
  }


ES 6 Imports
------------

Default import::

  import localName from 'src/my_lib';

Namespace import: imports the module as an object (with one property per named export)::

  import * as my_lib from 'src/my_lib';

Named imports::

  import { name1, name2 } from 'src/my_lib';

Renaming named imports::

  // Renaming: import `name1` as `localName1`
  import { name1 as localName1, name2 } from 'src/my_lib';
Empty import: only loads the module, doesn’t import anything. The first such import in a program executes the body of the module.
  import 'src/my_lib';

Source: http://exploringjs.com/es6/ch_modules.html

Imports for broken modules::

  require('script!objectpath/lib/ObjectPath');

Source: https://webpack.github.io/docs/shimming-modules.html


SASS Loader
-----------

Installation::

  $ npm install sass-loader --save-dev

Webpack Configuration (webpack.config.js)::

  module.exports = {
    ...
    module: {
      loaders: [
        ...
        { test: /\.scss$/, loaders: ["style", "css?sourceMap", "sass?sourceMap"]},
      ]
    },
    devtool: 'source-map'
  }

Javascript::

  import Styles from './styles.scss';

SASS (styles.scss)::

  body {
      padding-top: 80px;
  }


Jade Loader
-----------

Installation::

  $ npm install jade-loader --save-dev

Webpack Configuration (webpack.config.js)::

  module.exports = {
    ...
    module: {
      loaders: [
        ...
        { test: /\.jade$/, loader: 'jade-loader' },
      ]
    }
  }

Javascript::

  import template from './hero.jade';

Jade (hero.jade)::

  div.jumbotron
    h1 Angular, ES6, Webpack Starter!
    h3 You can find my template inside {{ vm.name }}.html


Angular Schema Form
-------------------

Installation::

  $ npm install angular-schema-form --save
  $ npm install objectpath --save
  $ npm install tv4 --save
  $ npm install angular-sanitize --save

Javascript::

  import 'angular-sanitize';
  require('script!tv4/tv4.js');
  require('script!objectpath/lib/ObjectPath');
  require('script!angular-schema-form/dist/schema-form');
  require('script!angular-schema-form/dist/bootstrap-decorator');

  let formsModule = angular.module('forms', [
    uiRouter,
    'schemaForm'
  ])

  ...

Controller::

  class FormsController {
    constructor() {
      this.name = 'Contact Us';
      this.model = {};
      this.schema = {
        type: 'object',
        properties: {
          name: { type: 'string', minLength: 2, title: 'Name', description: 'Name or alias' },
          title: {
            type: 'string',
            enum: ['dr','jr','sir','mrs','mr','NaN','dj']
          }
        },
        'required': [
          'name'
        ]
      };
      this.form = [
        '*',
        {
          type: 'submit',
          title: 'Save'
        }
      ];
    }
  }

  export default FormsController;


Service
-------

...

Travis CI
---------

- Enable Travis for repository

.travis.yml::

  language: node_js
  node_js:
  - 4.2.1
  cache:
    directories:
      - node_modules
  before_install:
    - export CHROME_BIN=chromium-browser
    - export DISPLAY=:99.0
    - sh -e /etc/init.d/xvfb start
  install:
  - npm install -g babel
  - npm install -g webpack@1.13.1
  - npm install -g webpack-dev-server@1.14.0
  - npm install -g eslint
  - npm install
  script:
  - npm run test
  notifications:
    email:
    - sekharau@gmail.com

webpack.config.js::

ESLint
------

Installation::

  $ npm install eslint -g

## License

Copyright (C) 2012 Travis CI Development Team

Distributed under the MIT License, the same as Node.js.