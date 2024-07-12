# Introduction

**Protocol Name:** Uniswap  
**Category:** DeFi  
**Smart Contract:** UniswapV2Router02  

## Function Analysis

**Function Name:** swapExactTokensForTokens  
**Block Explorer Link:** [UniswapV2Router02 on Etherscan](https://etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f#code)  

### Function Code
```solidity
function swapExactTokensForTokens(
    uint amountIn,
    uint amountOutMin,
    address[] calldata path,
    address to,
    uint deadline
) external ensure(deadline) returns (uint[] memory amounts) {
    TransferHelper.safeTransferFrom(
        path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amountIn
    );
    amounts = UniswapV2Library.getAmountsOut(factory, amountIn, path);
    require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    _swap(amounts, path, to);
}
