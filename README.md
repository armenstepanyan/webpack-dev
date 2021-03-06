# webpack-dev
### Initialize `package.json` with default params
```
npm i -y
```

### Install
 - `npm i -D webpack webpack-cli`
 - `npm i -D html-webpack-plugin html-loader` 
 - `npm i -D @babel/core babel-loader @babel/preset-env`
 - `npm i -D file-loader` for assets
 - `npm i -D node-sass style-loader css-loader sass-loader mini-css-extract-plugin`


### Create 
- `src/index.js` - main js file
- `hello.js` - custom js file with simple function
- `src/index.html`
- `images/cat.jpg` - assets files
- `src/style.main.scss` - sass file
- `webpack.config.js`

### Add scripts
```
  "scripts": {
    "build": "webpack",
    "start": "webpack-dev-server"
  },
```

### hello.js file

```
const sayHi = name => {
    return `Hello ${name}`
}

export { sayHi }

```

###  src/style/main.scss file
```
$bg: blue;

body {
    background-color: $bg;
}
```

###  index.js file

```
import { sayHi } from './hello';
import './style/main.scss';

console.log( sayHi('Bro') ) 

```


### webpack.config.js

```
const HtmlWebPackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            },
            {
                test: /\.html$/,
                use: [
                    {
                        loader: "html-loader",
                        options: { minimize: true }
                    }
                ]
            },
            {
                test: /\.(png|jpg|jpeg|gif)$/,
                use: [
                    'file-loader'
                ]
            },
            {
                test: /\.scss$/,
                use: [
                    'style-loader',
                    'css-loader',
                    'sass-loader'
                ]
            }
        ]
    },
    plugins: [
        new HtmlWebPackPlugin({
            template: './src/index.html',
            filename: './index.html'
        }),
        new MiniCssExtractPlugin({
            filename: '[name].css',
            chunkFilename: '[id].css'
        })
    ]
}
```
### npm run start - start dev server

### npm run build

- `cd dist`
- `http-server -o`
- navigate to `http://127.0.0.1:8080/`
