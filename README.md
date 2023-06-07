# webpack-5-crash-course-traversy-media
```bash
npm init -y
npm i -D webpack webpack-cli
```

Add script to package.json:
```json
"scripts": {
  "build": "webpack --mode production"
}
```


```bash
npm run build
```

## Using npm modules:
```bash
npm i uuid
npm remove uuid #(optionally can remove this)
```

##






```bash
touch webpack.config.js
```
## Single Entry Point
```js
// webpack.config.js;

const path = require('path');

module.exports = {
  mode: 'development',

  // ENTRY PointerEvent(s)
  entry: path.resolve(__dirname, 'src/index.js'),

  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
};

```

## Multiple Entry Points:
```js
// webpack.config.js;
// USING COMMON JS SYNTAX

const path = require('path');

module.exports = {
  mode: 'development',

  // ENTRY PointerEvent(s)
  entry: {
    bundle: path.resolve(__dirname, 'src/index.js'),
  },

  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js',
  },
};

```

## Adding Loaders
```bash
npm i -D sass style-loader css-loader sass-loader

mkdir styles && touch styles/main.scss
```

```js
// webpack.config.js;
const path = require('path');

module.exports = {
  ...

  // LOADERS
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
    ],
  },

};

```


## Adding Plugins
```bash
npm i -D html-webpack-plugin
touch template.html
```

```js
// webpack.config.js;
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  ...

  // PLUGINS
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Webpack App',
      filename: 'index.html',
      template: 'src/template.html',
    }),
  ],
};

```

```html
<!-- src/template.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <div class="container">
      <h3>Don't Laugh Challenge</h3>
      <div id="joke" class="joke"></div>
      <button id="jokeBtn" class="btn">Get Another Joke</button>
    </div>
  </body>
</html>

```



## Webpack Caching
```js
// webpack.config.js;

...

output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js', // <- add [contenthash] substitution
  },

...
```

## Add Webpack Dev Server
```json
// package.json

  "scripts": {
    "build": "webpack",
    "dev": "webpack serve" // <-Add dev script
  },
```

```bash
npm run dev # This will run on http://localhost:8080/
```

```js
// webpack.config.js;

  // DEV SERVER
  devServer: {
    static: {
      directory: path.resolve(__dirname, 'dist'),
    },
    port: 3000,
    open: true,   // automatically opens the app URL in web browser.
    hot: true,
    compress: true, // Enables gzip compression (a widely-used, server-side compression technique), for everything served.
    historyApiFallback: true,  // Ensures that all client-side routes work as expected by falling back to index.html for all unknown routes.
  },
```



```js
// webpack.config.js;

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  ...

  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js',
    clean: true   // <- will clean out old files in the dist folder
  },
```

## Adding Source Maps
```js
// webpack.config.js;

module.exports = {
  ...

  output: {
    ...
  },

  // SOURCE MAPPINGS:
  devtool: 'source-map', // <- Added this line

    // DEV SERVER
  devServer: {
    ...
  }
  ...
```


## Add Babel
```bash
npm i -D babel-loader @babel/core @babel/preset-env
```

Add the babel Loader
```js
// webpack.config.js;

module.exports = {
  ...

  // LOADERS
  module: {
    rules: [
      // CSS Loaders
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },

      // Babel Loader - enables backwards compatability
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
    ],
  },

```

## Asset Resource Loading
```bash
mkdir src/assets
```
```js
// webpack.config.js;

module.exports = {
  ...

  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js',
    clean: true,
    assetModuleFilename: '[name][ext]', // <-add this line to keep the asset name
  },


  // LOADERS
  module: {
    rules: [
      // ...other loaders

      // Resource Loader (included in webpack)
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },

```

## Add Bundle Analyzer Plugin
```bash
npm i -D webpack-bundle-analyzer
```

```bash
```

```bash
```

```bash
```

```bash
```
