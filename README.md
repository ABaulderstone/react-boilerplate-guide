# Build your own CRA
* `yarn init` 
* `yarn add @babel/core @babel/cli @babel/preset-env @babel/preset-react --dev`

## Babel 
* `touch .babelrc`
 ```json
    {
  "presets": ["@babel/env", "@babel/preset-react"]
}

``` 
## Webpack
* `yarn add webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader --dev`
* `touch webpack.config.js` 
```js
const path = require('path');
const webpack = require('webpack');

module.exports = {
    entry: "./src/index.js", 
    mode: "development", 
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /(node_modules|bower_components)/,
                loader: "babel-loader",
                options: { presets: ["@babel/env"]}
            },
            {
                test: /\.css$/,
                use: ["style-loader", "css-loader"]
            }
        ]
    },
    resolve: {extensions: ["*", ".js", ".jsx"]},
    output: {
        path: path.resolve(__dirname, "dist"), 
        publicPath: "/dist/",
        filename: "bundle.js"
    }, 
    devServer: {
        contentBase: path.join(__dirname, "public/"),
        port: 3000, 
        publicPath: "http://localhost:3000/dist/",
        hotOnly: true
    },
    plugins: [new webpack.HotModuleReplacementPlugin()]
};
```
## React
* `yarn add react react-dom`
