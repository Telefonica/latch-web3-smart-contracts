# latch-web3-smart-contracts

To use latch-web3, we need to download Latcheable.sol and import it into the contract we want to secure.
Once your smart contract (SC) is deployed, you must set the latch-proxy. 
There is a function in **Latcheable** called `setProxyLatch` to set it.
We have one on the Amoy testnet and another on the Polygon mainnet:
 ```
PROXY_LATCH_AMOY = "0x495b9152967b022a539d21fE8C1620651095F4bf"
PROXY_LATCH_MAINNET = "0xc7F93A52d1715D0a8d697600a6baC2f03Cc146B7"
```
Using example

```solidity

pragma solidity ^0.8.7;
import "./Latcheable.sol";

contract TestLatch is Ownable, Latcheable {

    uint256 public num;
    uint256 public num2;
    
    function setNum(uint256 new_num) external isLatcheable {
        require(new_num > 0, "The new number has to be > 0");
        num = new_num;
    }

    function operation1(uint256 new_num) external isLatcheableMethod('operation1') {
        require(new_num > 0, "The new number has to be > 0");
        num = new_num;
    }

    function operation2(uint256 new_num) external isLatcheableMethod('operation2') {
        require(new_num > 0, "The new number has to be > 0");
        num = new_num;
    }

    function getNum() external view returns (uint256) {
        return num;
    }
}
```

