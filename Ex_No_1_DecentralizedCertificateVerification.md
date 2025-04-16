### Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
1. Deploy a smart contract where universities can issue certificates.
2. Store a hash of certificate data on-chain.
3. Provide a verification function that checks certificate authenticity.
4. Users can verify the certificate by comparing the stored hash.
## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CertificateVerification {
    address public university;  // University address

    // Mapping to store issued certificate hashes
    mapping(bytes32 => bool) public certificates;
    event CertificateIssued(bytes32 certHash);
    constructor() {
        university = msg.sender;
    }
    function issueCertificate(string memory studentName, string memory degree, uint year) public {
        require(msg.sender == university, "Only university can issue certificates");
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));

        certificates[certHash] = true;
        emit CertificateIssued(certHash);
    }
    function verifyCertificate(string memory studentName, string memory degree, uint year) public view returns (bool) {
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
        return certificates[certHash];
    }
}
```
# Expected Output:
```
● When the university issues a certificate, it gets stored as a hash.
● A student or employer can verify the certificate by entering the details.
● If valid, it returns true; otherwise, false.
High-Level Overview:
● Used to prevent fake certificates.
● Enables quick verification by employers or other institutions.
● Shows how blockchain can be used in education and credential verification.
```
# Output
```
![Screenshot 2025-04-16 090619](https://github.com/user-attachments/assets/9e5b5441-1d7d-44e5-b6a1-8af4473deeda)
![Screenshot 2025-04-16 090637](https://github.com/user-attachments/assets/4cbb6bd8-58f8-4437-bd7e-344fb9ff4f6a)
![Screenshot 2025-04-16 090906](https://github.com/user-attachments/assets/06162b1d-5f4f-4980-8fd1-422526a872b7)

# Result:
To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity is done successfully.


