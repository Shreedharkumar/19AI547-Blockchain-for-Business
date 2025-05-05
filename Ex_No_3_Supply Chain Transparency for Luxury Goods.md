# Aim:
## Name : SHREEDAHR KUMAR K.J
## Reg No: 212224230265
## Date : 05-05-2025
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
The manufacturer records product creation details on-chain.


The product moves through different supply chain checkpoints.


The ownership of the product can be transferred securely.


Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
A luxury good (e.g., a Rolex watch) is registered on-chain.


Ownership is transferred at every checkpoint.


Buyers can check the authenticity before purchasing.


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.
# OUTPUT:
##Register
![Screenshot 2025-05-05 135045](https://github.com/user-attachments/assets/ca927f95-04ef-4f14-aae8-42c97511e280)
## Transaction
![Screenshot 2025-05-05 135350](https://github.com/user-attachments/assets/fc5ce4bf-d3a6-4b82-8d83-bd9be1f41bd0)

## Verification
![image](https://github.com/user-attachments/assets/77d03e80-824a-4625-ba03-ec554b8119c4)

# RESULT : 

A smart contract that tracks the supply chain of luxury goods and ensuring authenticity is successfully executed.
