# Ex No: 3 - Supply Chain Transparency for Luxury Goods
## Name : Abdul kalaam k m
## Reg No: 212223230003
## Date : 21-04-2025
# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
## step 1:
Manufacturer inputs productId and name, and registers the product if it's not already registered.
## step 2:
Contract stores the product with name, msg.sender as currentOwner, and sets verified = true.
## step 3:
For ownership transfer, contract checks if msg.sender is the current owner of the product.
## step 4:
If valid, contract updates currentOwner to the new owner's address and emits an event.
## step 5:
Repeat the ownership transfer at each supply chain checkpoint by authorized parties.
## step 6:
Buyer or verifier inputs productId to retrieve product details from the smart contract.
## step 7:
Contract returns the product’s name, currentOwner, and verified status for authenticity check.
## step 8:
All actions (registration and transfers) are permanently recorded on-chain for transparency and trust.



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
![Screenshot 2025-04-24 143529](https://github.com/user-attachments/assets/cdfd7bd7-efa6-46d3-80e8-85707d21ef0f)


Ownership is transferred at every checkpoint.
![Screenshot 2025-04-24 143541](https://github.com/user-attachments/assets/1eb40ae6-7716-4b77-ad8f-6e10fb64fea3)


Buyers can check the authenticity before purchasing.
![Screenshot 2025-04-24 143549](https://github.com/user-attachments/assets/d2297574-60f2-4b94-a77a-cfb90e8d6283)


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.


# RESULT : 
A smart contract that tracks the supply chain of luxury goods and ensuring authenticity is successfully executed.
