# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
A project owner starts a campaign with a funding goal and deadline.


Contributors can send ETH to the campaign.


If the goal is met before the deadline, funds are released to the project owner.


If the goal is not met, contributors can withdraw their funds.


## Program:
```
DEVELOPED BY:SACHIN J M
REG NO:212225100041
```
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:
<img width="1917" height="1078" alt="Screenshot 2026-11-18 143134" src="https://github.com/user-attachments/assets/586e0338-c0da-4af9-9cef-904eef65f79d" />
<img width="1917" height="1078" alt="Screenshot 2026-11-18 143203" src="https://github.com/user-attachments/assets/4de3c056-86ef-4fa9-bc69-9fd964ccb89a" />
<img width="1575" height="1078" alt="Screenshot 2026-11-18 143401" src="https://github.com/user-attachments/assets/54cb8ca6-0b9f-4c8f-bb33-3e756a857950" />

# High-Level Overview:
Teaches decentralized fundraising.


Avoids fraud by ensuring funds are only transferred if the goal is met.

# RESULT: 
the Blockchain-Based Crowdfunding (Kickstarter Alternative) has verified successfully
