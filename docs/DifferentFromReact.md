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

- add package **jest-junit** for saving testing result which is showed on the GitHub Action summary page

## truffle

## iac

## github/workflows