# Experiment 4: DeFi Lending and Borrowing Protocol
### Name : V Raksha dharanika
### Reg No: 212223230167
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
//SPDX-License-Identifier: MIT
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
        require(msg.value >= (amount * liquidationThreshold) / 100, "Nota enough collateral");
        borrowed[msg.sender] += amount;
        collateral[msg.sender] += msg.value;
        payable(msg.sender).transfer(amount);
        emit Borrowed(msg.sender, amount, msg.value);
    }
    function reduceCollateral(address user, uint256 amount) public {
    require(msg.sender == owner, "Only owner can reduce");
    require(collateral[user] >= amount, "Not enough collateral to reduce");
    collateral[user] -= amount;
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



![image](https://github.com/user-attachments/assets/4c359583-68e4-46e5-bceb-2446b5038802)



Users can borrow ETH by providing collateral.



![image](https://github.com/user-attachments/assets/75472f4e-bb85-428c-9423-87573e1bc5fb)





If Collateral ≥ 150% Borrowed amount, liquidation is not allowed.




![image](https://github.com/user-attachments/assets/61901f3e-9bba-434c-8157-c1ecc4168b87)




# High-Level Overview:


Teaches key DeFi concepts: lending, borrowing, collateral, liquidation.


Introduces risk management: overcollateralization and liquidation.


Directly related to DeFi protocols like Aave and Compound.

# RESULT : 
Thus,To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi.
