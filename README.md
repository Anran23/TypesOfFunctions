# MyToken (ERC20 Token)

MyToken is an ERC20 token implemented in Solidity, based on OpenZeppelin's contracts.

## Features

- **ERC20 Compliance:** Implements standard ERC20 token functions.
- **ERC20Burnable:** Extends ERC20 with burning capabilities.
- **Ownable:** Provides exclusive access control functionalities.

## Overview

MyToken contract allows for:
- Initial minting of tokens to the deployer's address.
- Minting of additional tokens by the owner.
- Burning of tokens by the owner or authorized addresses.

## Installation

To use MyToken in your project, follow these steps:

1. Install necessary dependencies:

npm install @openzeppelin/contracts@4.9.0


2. Import the contract into your Solidity project:

```solidity
import "@openzeppelin/contracts@4.9.0/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts@4.9.0/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts@4.9.0/access/Ownable.sol";

contract MyToken is ERC20, ERC20Burnable, Ownable {
    constructor(string memory name, string memory symbol, uint256 initialSupply) ERC20(name, symbol) {
        _mint(msg.sender, initialSupply);
    }

    function mint(address account, uint256 amount) public onlyOwner {
        _mint(account, amount);
    }

    function burnFrom(address account, uint256 amount) public override  {
        _burn(account, amount); // Using _burn directly
    }

    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        return true;
    }
}

## Usage

Deploy the contract specifying the token name, symbol, and initial supply.
Use mint function to mint more tokens (onlyOwner).
Use burnFrom function to burn tokens from an account (onlyOwner).
Transfer tokens using standard ERC20 transfer function.

##License

This project is licensed under the MIT License - see the LICENSE file for details.

For more information on ERC20 tokens and OpenZeppelin, refer to their respective documentations:

ERC20 Token Standard
OpenZeppelin Contracts
