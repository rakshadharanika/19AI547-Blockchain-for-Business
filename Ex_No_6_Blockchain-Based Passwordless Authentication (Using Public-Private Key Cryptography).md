# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
### Name   : V Raksha Dharanika
### Reg No : 212223230167
# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
1.User Registration:
The user registers by submitting their Ethereum public key to the system (no password required).

2.Challenge Generation:
When the user wants to log in, the system generates a random challenge message and sends it to the user.

3.Signature Creation:
The user signs the challenge using their private key and sends the signature back to the system.

4.Signature Verification:
The system (or smart contract) uses the user’s public key to verify the signature.

 If valid, the login is successful.

 If invalid, access is denied.


# Program:
```py
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    function authenticate(bytes32 hash, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");
        address signer = ecrecover(hash, v, r, s);
        return signer == msg.sender;
    }
}
```

# Expected Output:

1.Passwordless Registration Using Wallet Address.

![image](https://github.com/user-attachments/assets/7324a859-75ec-4c7d-88d9-e555853215f2)

2.Authentication via Cryptographic Signature.

![image](https://github.com/user-attachments/assets/c2f2af30-fe7e-41d8-becb-ce6351d9cca5)

3.Smart Contract Verifies User Signature On-Chain.

![image](https://github.com/user-attachments/assets/e65eafbc-86c7-4106-a28b-d32c5cafb499)


# High-Level Overview:
Eliminates password hacks & phishing attacks.


Uses Ethereum's built-in cryptographic functions.


Inspired by Web3 login solutions like MetaMask authentication.

# RESULT: 
Successfully implemented a passwordless authentication system using Ethereum public-private key cryptography.
