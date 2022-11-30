## client

- modify code of **client/src/contexts/EthContext/EthProvider.jsx**

  - add condition checking for testing, `if (window.ethereum)`, for **useEffect** (the one using `window.ethereum`)

    ```javascript
    useEffect(() => {
      // run only when in the browser environment
      if (window.ethereum) {
        ...
      }
    }, [init, state.artifact]);

  - call to an external service for the **contracts** address

    ```javascript
    async artifact => {
      if (artifact) {
        ...
        try {
          const deployedNetwork = artifact.networks[networkID];
    
          address = deployedNetwork && deployedNetwork.address;
          // If the network can't be found in the contract JSON call the
          // backend API for the address.
          if (!address) {
            console.log("Address not found in contract JSON. Calling backup api");
            const text = await (await fetch(`/api/GetContractAddress/?networkId=${networkID}`)).text();
            console.log(`API result: ${text}`);
            address = text;
          }
    
          contract = new web3.eth.Contract(abi, address);
        } 
        ...
    ```

- add package **jest-junit** for saving testing result which is showed on the GitHub Action summary page

## truffle

- add package **mocha-xunit-reporter** for saving test results and add reporter to **truffle-config.js**

  ```javascript
  mocha: {
    reporter: "xunit",
    reporterOptions: {
      output: "TEST-results.xml"
    }
  }
  ```

- add an environment variable **DEV_NETWORK**

  ```javascript
  ...
  var devNetworkHost = process.env["DEV_NETWORK"];
  
  config = {
    ...
    networks: {
      ...
      // development: {
      //  host: "127.0.0.1",     // Localhost (default: none)
      //  port: 8545,            // Standard Ethereum port (default: none)
      //  network_id: "*",       // Any network (default: none)
      // },
      ...
    },
    ...
  };
  
  // Using this code can default to using the built in test
  // network but define a dev 
  // Network in CI system without breaking a developer inner loop.
  if (devNetworkHost) {
    config.networks["development"] = {
      host: devNetworkHost,
      port: 8545,
      network_id: '*'
    };
  }
  
  module.exports = config;
  ```

- Add configuration for **Sepolia**
  ```javascript
  var apiKey = process.env["API_KEY"];
  var mnemonic = process.env["MNEMONIC"];
  var HDWalletProvider = require('@truffle/hdwallet-provider');

  config = {
    networks: {
      sepolia: {
        provider: () => new HDWalletProvider(mnemonic, `https://sepolia.infura.io/v3/${apiKey}`),
        network_id: 11155111,       // sepolia's network id
        chain_id: 11155111,         // sepolia's chain id
        gas: 5500000,        // Gas limit used for deploys.
        confirmations: 2,    // # of confirmations to wait between deployments. (default: 0)
        timeoutBlocks: 200,  // # of blocks before a deployment times out  (minimum/default: 50)
        skipDryRun: true     // Skip dry run before migrations? (default: false for public nets)
      },
    },
  };
  ```

## api

_added_

**Azure Function** to provide the address to the frontend.

## iac

## github/workflows

_added_

perform **CI** **CD** for the **React** box

## package.json

- add **Truffle** to make pipeline easier to create

## truffle-box.json

