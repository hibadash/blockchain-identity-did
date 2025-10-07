# Time-Locked Wallet (Solidity)

A simple Ethereum smart contract that locks Ether until a specified unlock time. Only the owner can withdraw the funds once the unlock time is reached.

## Features

- Lock ETH for a specific duration.
- Only the owner can withdraw.
- Emits an event on withdrawal.

## Contract Details

- **Contract Name:** `Lock`
- **Solidity Version:** ^0.8.28
- **Functions:**
  - `constructor(uint _unlockTime) payable`: Deploy the contract and set the unlock time.
  - `withdraw()`: Withdraw the locked funds after the unlock time.

## Events

- `Withdrawal(uint amount, uint when)`: Emitted when the funds are withdrawn.

## Usage

1. Deploy the contract with a future `_unlockTime` and optionally send ETH.
2. Wait until `block.timestamp >= unlockTime`.
3. Call `withdraw()` as the owner to retrieve your funds.

## Example

```js
// Deploying in Hardhat
const Lock = await ethers.getContractFactory("Lock");
const lock = await Lock.deploy(unlockTime, { value: ethers.utils.parseEther("1.0") });
await lock.deployed();

// Withdraw after unlock time
await lock.withdraw();
