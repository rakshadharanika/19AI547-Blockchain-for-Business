# Experiment 4: DeFi Lending and Borrowing Protocol
### Name : V Raksha Dharanika
### Reg No : 212223230167
# Aim:
To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi.

# Algorithm:
1.Deploy the contract and initialize required parameters like interest rate and liquidation threshold.

2.Users deposit ETH into the contract, which adds to the liquidity pool.

3.Users can borrow ETH by providing collateral greater than or equal to 150% of the borrowed amount.

4.Interest on borrowed funds is calculated dynamically based on the pool’s utilization rate.

5.If a borrower’s collateral drops below the required threshold (150% of the borrowed amount), they become eligible for liquidation.

6.Any user (a liquidator) can repay an undercollateralized borrower's debt and claim their collateral at a discounted rate.



# Program:
```py
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



![image](https://github.com/user-attachments/assets/63e1994e-9ca7-4bee-b657-b3f733076c07)



Users can borrow ETH by providing collateral.



![image](https://github.com/user-attachments/assets/aaf84ac1-8b0f-4e58-b448-b5e98bd417f9)



If Collateral ≥ 150% borrowed amount,liquidation not allowed.



![image](https://github.com/user-attachments/assets/3eecb5db-5ddc-4e49-8125-bd98388068c2)



# High-Level Overview:
1.Teaches key DeFi concepts: lending, borrowing, collateral, liquidation.


2.Introduces risk management: overcollateralization and liquidation.


3.Directly related to DeFi protocols like Aave and Compound.

# RESULT : 
Thus,To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi.


