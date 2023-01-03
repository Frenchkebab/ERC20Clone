# Customizable ERC20 Clone Factory

## [0] Setup

### 1. Clone the repository

`$ git clone https://github.com/Frenchkebab/ERC20Clone.git`

### 2. Install dependencies

`$ npm install`

## [1] Contracts

```
contracts
├── ERC20CloneFactory.sol
└── ERC20Implementation.sol
```

### ERC20Implementation.sol

Simple implementation of upgradeable ERC20 contract

### ERC20CloneFactory.sol

```solidity
function clone(string calldata _name, string calldata _symbol, uint256 _cap) external returns (address) {
    address clone = Clones.clone(implementation);
    ERC20Implementation(clone).initialize(_name, _symbol, msg.sender, _cap);

    emit Clone(msg.sender, clone);
    return clone;
}
```

Contract that lets users create new ERC20 tokens.
Can customize its `name`, `symbol`, `cap`, and `owner`.


## [2] test

`npx hardhat test`

### result

```
  ERC20 Clone
    ✔ should make an instance with expected parameters (82ms)

  Clone Pattern vs Creating New Contract
            Create : 1860350 gas
            Clone  :  196645 gas
            Diff   : 1663705 gas
    ✔ Compare Gas Cost (287ms)
```

