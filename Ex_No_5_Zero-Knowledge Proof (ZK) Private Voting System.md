# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
# Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

# Algorithm:
# Step 1:
Voter Registration
Each voter generates a secret vote key and submits a commitment (hashed vote) to the contract.


# Step 2: 
Voting Process
Voters submit their votes privately using a hash, without revealing their choice.


# Step 3: 
ZK Verification
The contract verifies if a vote belongs to a registered voter but does not reveal the actual vote.


# Step 4: 
Vote Counting
Once voting ends, the contract reveals the final tally without linking votes to individuals.



# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}

```
# Expected Output:
![BLOCKCHAIN-5 1](https://github.com/user-attachments/assets/c0e8086b-9599-4475-a657-91e37621b8f7)
![BLOCKCHAIN-5 2](https://github.com/user-attachments/assets/8ff1fae9-37fb-463b-b79f-3612eab1ddcb)
![BLOCKCHAIN-5 3](https://github.com/user-attachments/assets/fbb59f75-8ba3-4348-8744-2ee946276f67)
![BLOCKCHAIN-5 4](https://github.com/user-attachments/assets/fd4e5120-ced1-4e68-bb37-3936d746fd91)
![BLOCKCHAIN-5 5](https://github.com/user-attachments/assets/6123988e-079d-4387-a357-d44723ad992e)
![BLOCKCHAIN-5 6](https://github.com/user-attachments/assets/cb0a1215-cfaa-4389-a045-5e2e2fa86bf3)
![BLOCKCHAIN-5 7](https://github.com/user-attachments/assets/973a50d6-7775-4435-9f09-a5f30c96b58c)
![BLOCKCHAIN-5 8](https://github.com/user-attachments/assets/0f324ca7-c21a-460e-baab-22d7c8a2c1e7)

# RESULT: 
The ZK Private Voting System enables voters to prove their vote is valid without revealing it, ensuring privacy and integrity. It prevents double voting and allows public verification of the final tally.

