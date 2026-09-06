# Pete's Pet Shop

A decentralized pet adoption dApp built with [Truffle](https://trufflesuite.com/), Solidity, and Web3. Browse 16 pets, adopt one from your Ethereum account, and see the adoption recorded on-chain.

This project follows the [Truffle Pet Shop tutorial](https://trufflesuite.com/guides/pet-shop/).

## Features

- Solidity `Adoption` contract that stores up to 16 adopters
- Web UI that lists pets from `src/pets.json`
- MetaMask / injected Web3 support, with a Ganache fallback
- Adopted pets are marked **Success** and cannot be adopted again
- JavaScript tests for the adoption flow

## Prerequisites

- [Node.js](https://nodejs.org/) (LTS)
- [Ganache](https://trufflesuite.com/ganache/) running locally (default UI port `7545`)
- [MetaMask](https://metamask.io/) (to adopt from the browser)

Truffle is listed as a project dependency, so you can run it via `npx truffle` after installing packages.

## Getting started

```bash
npm install
```

Start Ganache and keep it running. Then compile and deploy the contracts to the local network:

```bash
npx truffle compile
npx truffle migrate --network development
```

Run the front end (serves `src/` and the compiled contract artifacts):

```bash
npm run dev
```

Open the app in your browser, connect MetaMask to the Ganache network, and click **Adopt** on a pet.

## Tests

```bash
npx truffle test
```

## How it works

The `Adoption` contract keeps an array of 16 addresses. Calling `adopt(petId)` stores `msg.sender` as that pet's owner. `getAdopters()` returns the full list so the UI can disable pets that are already taken.

```solidity
function adopt(uint petId) public returns (uint) {
    require(petId >= 0 && petId <= 15);
    adopters[petId] = msg.sender;
    return petId;
}
```

## Project structure

```
contracts/          # Solidity contracts (Adoption, Migrations)
migrations/         # Truffle deployment scripts
src/                # Front end (HTML, CSS, JS, pet data and images)
test/               # Contract tests
truffle-config.js   # Networks (Ganache on 127.0.0.1:7545)
```

## License

MIT
