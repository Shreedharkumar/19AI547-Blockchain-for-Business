# Experiment 4: DeFi Lending and Borrowing Protocol
# Aim:
To build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi.

# Algorithm:
Step 1: Users deposit ETH into the smart contract to earn interest over time.

Step 2: Users can borrow ETH by providing enough collateral (at least 150% of the borrowed amount).

Step 3: The contract checks that collateral is sufficient before allowing the loan.

Step 4: Interest is calculated dynamically based on how much ETH is borrowed compared to total deposits.

Step 5: If a borrower’s collateral value drops below the safe level (liquidation threshold), they can be liquidated.

Step 6: Liquidators can repay a borrower's debt and claim their collateral to maintain system stability.

# Program:
```
Developed by: SHREEDHAR KUMAR K.J
Register number: 212224230265
Date: 05-05-2025
```
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
# Output :

### Borrow

![Screenshot 2025-05-05 140214](https://github.com/user-attachments/assets/83b5c1ae-8191-4ea1-b931-c821fb0bd82c)

### Liquidate

![Screenshot 2025-05-05 140348](https://github.com/user-attachments/assets/5216e52b-89eb-43be-9afb-d654c4dd7b26)

### ReduceCollateral

![image](https://github.com/user-attachments/assets/1e5a8d9e-c1f9-4764-89e7-101df6d44917)

### Borrowed

![image](https://github.com/user-attachments/assets/293f676d-3e35-4bc6-a53b-23f3e41743f1)

### Collateral

![image](https://github.com/user-attachments/assets/c5eb6f0a-631e-49d9-aee3-852a2734250f)

### Deposits

 ![image](https://github.com/user-attachments/assets/5668fe74-8e2b-4583-bdbb-6da5d59c252e)

### Interest rate

![image](https://github.com/user-attachments/assets/959f1312-a3ca-4f05-a663-fc64d138a626)

### Liquidation threshold call

![image](https://github.com/user-attachments/assets/bf0a3e0a-707c-4ca6-be76-a478a5dc0b65)

### Owner

![image](https://github.com/user-attachments/assets/c8952803-f291-48ac-a593-745246ee93c4)

# RESULT : 
Thus, to build a decentralized lending protocol where users can deposit assets to earn interest and borrow assets by providing collateral. This experiment introduces concepts like overcollateralization, liquidity pools, and interest accrual in DeFi is executed successfully.
