# Ex_No_3_Supply Chain Transparency for Luxury Good
### Name   : V Raksha Dharanika
### Reg No : 212223230167
# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:

1.The manufacturer records product creation details on-chain.


2.The product moves through different supply chain checkpoints.


3.The ownership of the product can be transferred securely.


4.Buyers can verify the product’s authenticity.


# Program:
```py
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
1.A luxury good (e.g., a Rolex watch) is registered on-chain.
![image](https://github.com/user-attachments/assets/a60288eb-e4e9-4d7c-996f-4cc71f0850e3)


2.Ownership is transferred at every checkpoint.
![image](https://github.com/user-attachments/assets/06c33e65-7f38-4ed4-88c6-888876b809e3)


3.Buyers can check the authenticity before purchasing.

![image](https://github.com/user-attachments/assets/939834da-c835-4ffa-8334-39cf81620083)

# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 

Successfully developed a smart contract to track and verify the supply chain of luxury goods, ensuring secure ownership transfer and product authenticity.
