# Build your own CRA

## Notes 
This is mostly for my own reference and is heavily based on https://reactjs.org/docs/create-a-new-react-app.html
But updated for newer webpack syntaxes and functional components

* `yarn init` 
* `yarn add @babel/core @babel/cli @babel/preset-env @babel/preset-react --dev`

### Babel 
* `touch .babelrc`
 ```json
    {
  "presets": ["@babel/env", "@babel/preset-react"]
}

``` 
### Webpack
* `yarn add webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader --dev`
* `touch webpack.config.js` 
```js
const path = require('path');

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
        static: {
            directory: path.join(__dirname, "public/"),
        },
        port: 3000, 
        hot: true
    }
}
```
### React
* `yarn add react react-dom`
* `touch ./src/index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.js';
ReactDOM.render(<App />, document.getElementById("root"));

```

* `touch ./src/App.js`
```js
import React from 'react';
import './src/App.css';
const App = (props) => {
    return(
    <div className="App">
        <h1>Hello from React!!!</h1>
    </div>
    )

}
export default App;
```
* `touch ./src/App.css`
```css
.App {
    margin: 1rem;
    font-family: Arial, Helvetica, sans-serif;
}
```

### Scripts
* Update `package.json`
```json
  "scripts": {
    "start": "webpack serve --mode development", 
    "build": "webpack --mode production"
  },
  ```
