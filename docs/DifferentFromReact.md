## client

- modify code of **client/src/contexts/EthContext/EthProvider.jsx**

  - add condition checking, `if (window.ethereum)`, for **useEffect** (the one using `window.ethereum`)

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

## iac

## github/workflows