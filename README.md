# SimpleWallet-
its a simple wallet of deposit withdraw and many other functions
# SimpleWallet Smart Contract

This project is a simple wallet smart contract implemented in Solidity. It demonstrates the usage of `require()`, `assert()`, and `revert()` statements. The contract allows users to deposit Ether, and the owner can withdraw Ether. It includes functions to check the balance and to manually trigger `revert()` and `assert()` statements for demonstration purposes.

## Functionality

- **`require()` Statement**: Used to ensure that only the contract owner can perform certain actions.
- **`assert()` Statement**: Used to verify internal state invariants.
- **`revert()` Statement**: Used to manually revert transactions with a custom error message.

## Contract Code

The smart contract is implemented in `SimpleWallet.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleWallet {
    address public owner;
    uint public balance;

    // Constructor to set the owner of the contract
    constructor() {
        owner = msg.sender;
        balance = 0;
    }

    // Modifier to check if the caller is the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Caller is not the owner");
        _;
    }

    // Function to deposit Ether into the wallet
    function deposit() public payable {
        balance += msg.value;
    }

    // Function to withdraw Ether from the wallet
    function withdraw(uint amount) public onlyOwner {
        require(amount <= balance, "Insufficient balance");
        balance -= amount;
        payable(msg.sender).transfer(amount);
    }

    // Function to check the balance
    function checkBalance() public view returns (uint) {
        return balance;
    }

    // Function to trigger a manual revert
    function triggerRevert() public {
        revert("Manual revert triggered");
    }

    // Function to trigger an assert failure
    function triggerAssert() public {
        assert(balance == 0); // This will fail if balance is not zero
    }
}
