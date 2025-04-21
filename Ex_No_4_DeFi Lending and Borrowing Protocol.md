# Experiment 4: DeFi Lending and Borrowing Protocol
# Aim:
To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi.

# Algorithm:
step 1 :Users send Ether to the contract via deposit(), which adds the amount to their balance and emits a Deposited event.

step 2 :Users call borrow(amount) and must provide at least 150% of the loan amount as collateral. The contract transfers the borrowed Ether to the user and records the debt.

step 3 :Anyone can call liquidate(borrower) if a user's collateral falls below 150% of their debt. The liquidator receives the borrower’s collateral.


step 4 :Every deposit, borrow, and liquidation emits an event to ensure transparency and traceability on the blockchain.



Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract DeFiLending {
    address public owner;
    uint256 public interestRate = 5; // 5% interest per cycle
    uint256 public liquidationThreshold = 150; // 150% collateralization
    mapping(address => uint256) public deposits;
    mapping(address => uint256) public borrowed;
    mapping(address => uint256) public collateral;

    event Deposited(address indexed user, uint256 amount);
    event Borrowed(address indexed user, uint256 amount, uint256 collateral);
    event Liquidated(address indexed user, uint256 debtRepaid, uint256 collateralSeized);

    constructor() {
        owner = msg.sender;
    }

    function deposit() public payable {
        require(msg.value > 0, "Deposit must be greater than zero");
        deposits[msg.sender] += msg.value;
        emit Deposited(msg.sender, msg.value);
    }

    function borrow(uint256 amount) public payable {
        require(msg.value >= (amount * liquidationThreshold) / 100, "Not enough collateral");
        borrowed[msg.sender] += amount;
        collateral[msg.sender] += msg.value;
        payable(msg.sender).transfer(amount);
        emit Borrowed(msg.sender, amount, msg.value);
    }

    function liquidate(address borrower) public {
        require(collateral[borrower] < (borrowed[borrower] * liquidationThreshold) / 100, "Not eligible for liquidation");
        uint256 debt = borrowed[borrower];
        uint256 seizedCollateral = collateral[borrower];

        borrowed[borrower] = 0;
        collateral[borrower] = 0;
        payable(msg.sender).transfer(seizedCollateral);
        emit Liquidated(borrower, debt, seizedCollateral);
    }
}

```
# Expected Output:
Users can deposit ETH and earn interest.
![Screenshot 2025-04-21 133946](https://github.com/user-attachments/assets/fc346029-f93c-4141-8e80-4b110f0f402a)


Users can borrow ETH by providing collateral.
![Screenshot 2025-04-21 134010](https://github.com/user-attachments/assets/698ea6f9-5708-4ff9-8b83-cb3e171e1a49)


If collateral < 150% of borrowed amount, liquidators can seize the collateral.
![Screenshot 2025-04-21 134058](https://github.com/user-attachments/assets/3d3f64ba-0384-4cd8-acd8-944792edd885)



# High-Level Overview:
Teaches key DeFi concepts: lending, borrowing, collateral, liquidation.


Introduces risk management: overcollateralization and liquidation.


Directly related to DeFi protocols like Aave and Compound.

# RESULT : 
To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi is completed successfully.

