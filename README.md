# eth_avax_project-3


# Token.sol

This Repo is made for an Assessments for the eth-beginner project for Metacrafters. The purpose of this Repository is to showcase my knowledge and understanding of the smart contracts and especially, about creating my ERC20 Tokens,with mentioned requirements.
Functionality
Only contract owner should be able to mint tokens
Any user can transfer tokens
Any user can burn tokens

Description
This Repository consists of a contract named function.sol written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. This contract is basically a ERC20 token which have various functions and token Variables like name ,symbol ,digit and explain how can we interact with this contract using various functions.

Getting Started
Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., TokenContract.sol). Copy and paste the following code into the file:




// SPDX-License-Identifier: MIT


pragma solidity ^0.8.0;



contract MyToken {
    
    string public name = "My Token";
   
    string public symbol = "MTK";
   
    uint8 public decimals = 18;
    
    uint256 public totalSupply;
   
    address public owner;
   
    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor(uint256 initialSupply) {
        totalSupply = initialSupply * 10**uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    function transfer(address to, uint256 value) public returns (bool) {
        require(to != address(0), "Invalid recipient");
        require(balanceOf[msg.sender] >= value, "Insufficient balance");

        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;

        emit Transfer(msg.sender, to, value);
        return true;
    }

    function approve(address spender, uint256 value) public returns (bool) {
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }

    function transferFrom(address from, address to, uint256 value) public returns (bool) {
        require(from != address(0), "Invalid sender");
        require(to != address(0), "Invalid recipient");
        require(balanceOf[from] >= value, "Insufficient balance");
        require(allowance[from][msg.sender] >= value, "Allowance exceeded");

        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;

        emit Transfer(from, to, value);
        return true;
    }

    function mint(address account, uint256 amount) public {
        require(msg.sender == owner, "Only the owner can mint");
        require(account != address(0), "Invalid address");
        totalSupply += amount;
        balanceOf[account] += amount;
        emit Transfer(address(0), account, amount);
    }

    function burn(uint256 amount) public {
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");
        totalSupply -= amount;
        balanceOf[msg.sender] -= amount;
        emit Transfer(msg.sender, address(0), amount);
    }
}


To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile Token.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "Token.sol" contract from the dropdown menu, and then click on the "Deploy" button. Before Deploying ,you need to pass the value for name,symbol and total supply of tokens as mentioned in constructor.

Once the contract is deployed, you can interact with it by calling the function.

Authors
CodeCracker2 (https://github.com/CodeWithNoob )

License
This project is licensed under the MIT- see the LICENSE.md file for details
