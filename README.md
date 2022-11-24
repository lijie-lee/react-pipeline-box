# React-Pipeline Truffle Box

This box comes by extending [react-box](https://github.com/truffle-box/react-box)

## Pipeline
The pipeline contains six jobs
- build
    - compiles, tests, and packages artifacts
- dev
    - deploys infrastructure, contracts and frontend
        - create an **Azure Container App** resource for hosting **Ganache** which provide the blockchain for development stage
        - create an **Azure Static Web Application(SWA)** resource for hosting frontend and providing API for retrieving smart contract address by using the built-in **Azure Function** within **SWA**
- dev_validation
    - waits for manual validation of dev and deletes dev environment
- qa
    - deploys infrastructure, contracts and frontend
        - create an **Azure Static Web Application(SWA)** resource for hosting frontend and providing API for retrieving smart contract address by using the built-in **Azure Function** within **SWA**
- qa_validation
  - waits for manual validation of qa and deletes qa environment
- prod
  - need to be implemented by yourself cause deploy contracts to mainnet, like Ethereum, is a sensitive job.

## How to setup project

Refer to [tutorial](https://github.com/lijie-lee/react-pipeline-box/blob/main/docs/Tutorial.md)

> If just develop locally, directly run command `truffle unbox lijie-lee/react-pipeline-box`, and then start coding.

## Difference from React-Box

[Difference](https://github.com/lijie-lee/react-pipeline-box/blob/main/docs/DifferenceFromReact.md)

## Q&A
[QA](https://github.com/lijie-lee/react-pipeline-box/blob/main/docs/QA.md)
