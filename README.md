# MyToken Smart Contract

This repository contains the source code for the `MyToken` smart contract, a simple implementation of an ERC20-like token on the Ethereum blockchain.

## Contract Details

The `MyToken` smart contract allows for the minting and burning of tokens. It includes public variables to store the token name, symbol, and total supply. Additionally, it maintains a mapping of addresses to balances.

### Features

- **Token Details**: Public variables for the token name (`name`), symbol (`symbol`), and total supply (`totalSupply`).
- **Balance Mapping**: A mapping that associates each address with its token balance.
- **Minting**: A `mint` function to create new tokens and assign them to a specified address.
- **Burning**: A `burn` function to destroy tokens from the sender's balance, ensuring the sender has enough tokens before burning.

## Requirements

1. The contract has public variables that store the details about the token (Token Name, Token Abbreviation, Total Supply).
2. The contract has a mapping of addresses to balances.
3. The contract includes a `mint` function that takes an address and a value, increasing the total supply by that number and the balance of the specified address by that amount.
4. The contract includes a `burn` function that takes a value and decreases the total supply by that number and the balance of the sender by that amount.
5. The `burn` function ensures the sender's balance is greater than or equal to the amount to be burned.

## Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

contract MyToken {

    // Public variables
    string public name = "Token";
    string public symbol = "KRM";
    uint public totalSupply;

    // Mapping of addresses to balances
    mapping(address => uint) public balances;

    // Mint function to create new tokens
    function mint(address _add, uint amount) public {
        totalSupply += amount;
        balances[_add] += amount;
    }

    // Burn function to destroy tokens
    function burn(uint amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance to burn");
        totalSupply -= amount;
        balances[msg.sender] -= amount;
    }
}
