# Solidity

Solidity is statically typed, supports inheritance, libraries, and complex user-defined types, among other features.

Contract language for voting, auctions, multi-sig wallets, etc. Contract is collection of functions and data stored on blockchain.

Functions that aren't pure/view cost gas

Account have **storage** which is persistent between function calls/transcations. **Memory** for each call. 

### Foundry

Smart contract development toolchain with building, testing, etc

#### [Installation](https://book.getfoundry.sh/getting-started/installation)

```bash
curl -L https://foundry.paradigm.xyz | bash
```

Follow instructions perhaps

```
foundryup
```

## Solidity

#### Basic Program

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract Coin {
    // public variables accessible from other contracts
    address public minter;
    mapping(address => uint) public balances;

    // Events are subscribeable by clients
    event Sent(address from, address to, uint amount);

    constructor() {
        minter = msg.sender;
    }

    function mint(address receiver, uint amount) public {
        require(msg.sender == minter);
        balances[receiver] += amount;
    }

    error InsufficientBalance(uint requested, uint available);

    function send(address receiver, uint amount) public {
        if (amount > balances[msg.sender])
            revert InsufficientBalance({
                requested: amount,
                available: balances[msg.sender]
            });

        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        emit Sent(msg.sender, receiver, amount);
    }
}
```

### Variable Visibility

```solidity
// no visibility
string n1 = "N1"
//only within contract
string private n2 = "N2"
//only within contract, but can be inherited
string internal n3 = "N3"
//see within, outside, and can be inherited
string public n4 = "N4"

//similar for functions; internal, public, external
function increment() external {
  count = count + 1;
}
```

### Function Modifiers

```solidity
string public name = "Example 5";
uint public balance;

//doesn't modify state, but reads
function getName() public view return(string memory) {
	return name;
}

//can't read or modify state
function add(uint a, uint b) public pure returns(uint) {
	return a + b;
}

//recieves eth or crypto
function pay() public payable {
	payer = msg.sender;
	origin = tx.origin;
	amount = msg.value;
}
```

#### Custom Modifer

```solidity
address private owner;
string public name = "";

modifier onlyOwner {
	require(msg.sender == owner, 'caller must be owner');
	_;
}

function setName(string memory _name) onlyOwner public {
	name = _name;
}
```

#### Mapping

```solidity
   mapping(address => uint) public balances;

   function updateBalance(uint newBalance) public {
      balances[msg.sender] = newBalance;
   }
```

#### Enum

```solidity
contract EnumContract {
    enum ActionChoices { GoLeft, GoRight, GoStraight, SitStill }
    ActionChoices choice;
    ActionChoices constant defaultChoice = ActionChoices.GoStraight;

    function setGoStraight() public {
        choice = ActionChoices.GoStraight;
    }

    // Since enum types are not part of the ABI, the signature of "getChoice"
    // will automatically be changed to "getChoice() returns (uint8)"
    // for all matters external to Solidity.
    function getChoice() public view returns (ActionChoices) {
        return choice;
    }

    function getDefaultChoice() public pure returns (uint) {
        return uint(defaultChoice);
    }

    function getLargestValue() public pure returns (ActionChoices) {
        return type(ActionChoices).max;
    }

    function getSmallestValue() public pure returns (ActionChoices) {
        return type(ActionChoices).min;
    }
}
```

#### Custom Error

```solidity
    // custom error statement
    error LackOfFunds(uint withdrawAmt, uint availableAmt);
     
         function checkCustomError(address _receiver,uint _withdrawAmt) public {
        if (bal[msg.sender]< _withdrawAmt) {
            revert LackOfFunds({withdrawAmt: _withdrawAmt, availableAmt: bal[msg.sender]});
        }
        bal[msg.sender] -= _withdrawAmt;
        bal[_receiver]+=_withdrawAmt;
    }
```

## Foundry Unit Tests

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "forge-std/Test.sol";
import "../src/Counter.sol";

contract CounterTest is Test {
  // an address created by casting a decimal to an address
  address owner = address(1234);

    function setUp() public {
        counter = new Counter();
        counter.setNumber(0);
    }

    function testIncrement() public {
        counter.increment();
        assertEq(counter.number(), 1);
    }

  function testChangeOwner() public {
  		//prank to change msg.sender
      vm.prank(owner);
      contractToTest.changeOwner(newOwner);
      assertEq(contractToTest.owner(), newOwner);
  }
}


```

