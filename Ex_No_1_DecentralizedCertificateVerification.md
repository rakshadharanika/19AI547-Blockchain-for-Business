### Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:

1.Deploy a smart contract by the authorized university to manage certificate issuance.
2.Accept student details (name, degree, year) as input to create a unique certificate.
3.Generate a hash of the certificate data using a cryptographic hashing function.
4.Store the hashed certificate data on the blockchain in a mapping for verification.
5.Emit an event whenever a new certificate is issued for transparency and tracking.
6.Allow users to verify certificates by re-hashing input data and checking its existence on-chain.

## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
contract CertificateVerification {
address public university;
mapping(bytes32 => bool) public certificates; // Store hashed certificates
event CertificateIssued(bytes32 indexed certHash);
constructor() {
university = msg.sender; // University deploys the contract
}
function issueCertificate(string memory studentName, string memory degree, uint256 year) public {
require(msg.sender == university, "Only university can issue certificates");
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
certificates[certHash] = true;
emit CertificateIssued(certHash);
}
function verifyCertificate(string memory studentName, string memory degree, uint256 year) public view returns (bool) {
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
return certificates[certHash];
}
}
```
# Expected Output:
![image](https://github.com/user-attachments/assets/6252c382-b0ea-4784-a633-c2ecd446abc1)

```
● When the university issues a certificate, it gets stored as a hash.
● A student or employer can verify the certificate by entering the details.
● If valid, it returns true; otherwise, false.
High-Level Overview:
● Used to prevent fake certificates.
● Enables quick verification by employers or other institutions.
● Shows how blockchain can be used in education and credential verification.
```
# Result:
The smart contract was successfully implemented to issue and verify academic certificates on Ethereum, ensuring authenticity and preventing forgery
