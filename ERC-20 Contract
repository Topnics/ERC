// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract Tems is ERC20, Ownable {
    constructor() ERC20("tems", "TEM") {
         uint256 n = 1000000;
        _mint(msg.sender, n * 10 * uint(decimals()));
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }


  // Our Token Contract
  Tems yourToken;

  // token price for ETH
  uint256 public tokensPerEth = 1000;

  // Event that log buy operation
  event BuyTokens(address receiver, uint256 amountOfETH, uint256 amountOfTokens);

  

  /**
  * @notice Allow users to buy token for ETH
  */
  function buyTokens() public payable returns (uint256 amountOfTokens) {
    require(msg.value > 0, "Send ETH to buy some tokens");

    uint256 amountToBuy = msg.value * tokensPerEth;

    // check if the Vendor Contract has enough amount of tokens for the transaction
    uint256 vendorBalance = yourToken.balanceOf(address(this));
    require(vendorBalance >= amountToBuy, "Vendor contract has not enough tokens in its balance");

    // Transfer token to the msg.sender
    (bool sent) = yourToken.transfer(msg.sender, amountToBuy);
    require(sent, "Failed to transfer token to user");

    // emit the event
    emit BuyTokens(msg.sender, msg.value, amountToBuy);

    return amountToBuy;
    }
}


   
