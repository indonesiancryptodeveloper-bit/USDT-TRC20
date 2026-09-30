# USDT-TRC20
Tether USD (USDT) is a TRC20 utility token deployed on the TRON network with a total supply of 10,000,000,000 tokens and 6 decimals, designed to facilitate secure decentralized transactions and ecosystem liquidity.
# Tether USD (USDT) - TRC20 Official Repository

Official repository and documentation for the **Tether USD (USDT)** TRC20 utility token deployed on the TRON network.

## 📌 Token Specifications
* **Network:** TRON Mainnet
* **Token Standard:** TRC20
* **Token Name:** Tether USD
* **Token Symbol:** USDT
* **Decimals:** 6
* **Total Supply:** 10,000,000,000 USDT
* **Contract Address:** [`TQS34dDVoraAoFErmLC5KX8vgZF7AYaG83`](https://tronscan.org/#/contract/TQS34dDVoraAoFErmLC5KX8vgZF7AYaG83)
* **Verification Status:** Verified & Published on TronScan

---

## 🛠️ Smart Contract Source Code
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract InternalUtilityToken {
    string public name = "Tether USD";
    string public symbol = "USDT";
    uint8 public decimals = 6;
    uint256 public totalSupply = 10_000_000_000 * 10**6;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    address public owner;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor() {
        owner = msg.sender;
        balanceOf[msg.sender] = totalSupply;
        emit Transfer(address(0), msg.sender, totalSupply);
    }

    function transfer(address recipient, uint256 amount) public returns (bool) {
        require(balanceOf[msg.sender] >= amount, "Saldo tidak cukup");
        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint256 amount) public returns (bool) {
        allowance[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
        require(balanceOf[sender] >= amount, "Saldo tidak cukup");
        require(allowance[sender][msg.sender] >= amount, "Allowance tidak cukup");
        allowance[sender][msg.sender] -= amount;
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }
}
