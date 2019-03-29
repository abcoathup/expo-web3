# Expo (React Native) and Web3.js

Boiler plate

Based on https://gist.github.com/dougbacelar/29e60920d8fa1982535247563eb63766

1. Create expo app
```
expo init
```

2. Install node-libs-browser
```
npm install --save node-libs-browser
```

3. Create a file called rn-cli.config.js on the root of the project and add the following code into it:
```
const nodeLibs = require('node-libs-browser');

module.exports = {
  resolver: {
    extraNodeModules: nodeLibs
  }
};
```

4. Create a file called global.js on the root of the project and add the following code into it:
```
// Inject node globals into React Native global scope.
global.Buffer = require('buffer').Buffer;
global.process = require('process');

if (typeof btoa === 'undefined') {
  global.btoa = function (str) {
    return new Buffer(str, 'binary').toString('base64');
  };
}

if (typeof atob === 'undefined') {
  global.atob = function (b64Encoded) {
    return new Buffer(b64Encoded, 'base64').toString('binary');
  };
}
```

5. Import the global.js file into your App.js file
```
import './global';
```

Now we can install the web3.js api
```
npm install --save web3
```

Require the API in your App.js file
```
const Web3 = require('web3');
```

6. Add the following code inside your React component in App.js to get started with consuming the API. The code will print information of the latest block on the console.
```
componentWillMount() {
  const web3 = new Web3(
    new Web3.providers.HttpProvider('https://mainnet.infura.io/')
  );

  web3.eth.getBlock('latest').then(console.log)
}
```

7. Start expo
```
npm start
```