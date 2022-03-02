# Glossary

### APY

Also known as Annual Percentage Yield, APY refers to the compounded returns that you get on your investments over a period of one year. In DeFi, the value of APY changes widely based on different factors and can change quickly.&#x20;

It is different than APR, which means "Annual Percentage Rate" and represents the returns of an investment over one year without compounding.&#x20;

### Custodial / Non-custodial protocol

In a custodial protocol, the protocol controls the keys of the assets you own and stores these assets on your behalf (think Binance or FTX).

In a non-custodial protocol, the protocol does not have access to the private keys of the assets its users deposit. Moreover, the protocol cannot block any users from withdrawing their funds at any point of time, i.e, the smart contract that runs the protocol is permissionless and cannot be changed to stop the users from withdrawing their funds.

For example, when you interact with Marinade, your SOL tokens are exchanged for mSOL that gives you ownership over a part of the staking pool. The mSOL tokens are equivalent in value to the SOL deposited. You can also get back your staked SOL tokens at any time by using the immediate unstake option without any hold ups. This makes Marinade a non-custodial protocol.

### Delegators

Delegators are those who let their SOL tokens count towards the stake of a selected validator through a smart contract. As a result, a part of the rewards distributed is automatically shared with the delegator based on the smart contract.

### Epoch

In the Solana network, an epoch has a variable time and corresponds to the time a [leader schedule ](https://docs.solana.com/terminology#leader-schedule)is valid. An epoch lasts an average of 2 days and you can follow the evolution of the current and previous epochs on [Solana Beach](https://solanabeach.io) or directly on [Marinade](https://marinade.finance/app/staking).&#x20;

### Liquidity

Liquidity refers to the total available circulating supply of a given asset in a protocol.

### Liquidity Mining

Liquidity mining is a distribution method where the tokens of a newly created platform are distributed between users who provide liquidities to the protocol. It aims at distributing those tokens over time instead of going with sales round.&#x20;

### Liquidity Pool

A liquidity pool is a smart contract where a pair of tokens is locked and made available for swaps. Any pair of tokens can have liquidity pools created for them (mSOL/SOL, SOL/USDC, MNDE/SOL, etc.). This smart contract allows anyone to exchange one of the token of the pair for the other, in exchange for a small fee distributed to the liquidity providers, people who made their liquidity available in this smart contract.&#x20;

Liquidity pools are one of the pillars of DeFi since they allow to swap a token for another without the need of an order book and in a trustless manner.&#x20;

### Multisig Wallet

A multisig wallet is a crypto wallet that has multiple layers of control in order to make transactions with the wallet. Such a wallet is defined by a set of smart contract rules that mandates multiple approvals from different users in order to make a transaction from the wallet.

### Stablecoin

A stablecoin is a cryptocurrency designed to always match as closely as possible the price of a fiat currency. Each stablecoin (USDT, USDC, DAI, BUSD, etc.) has its own backing mechanisms and needs to be considered individually. Stablecoins are mostly used to easily swap between crypto and dollars without involving fiat transactions.&#x20;

### Stake account

In the Solana network, a stake account is created when a wallet stakes to a validator. This stake account is the "stake receipt" proving that their funds are staked to a specific validator.&#x20;

Marinade offers the opportunity to easily [transfer an existing stake acount](../marinade-protocol/system-overview/#deposit-an-existing-stake-account) to Marinade. You will immediatly receive mSOL without having to worry about unstaking your SOL.

### Total Value Locked (TVL)

TVL is a metric that represents the total amount of money present in a protocol.

### Unstake Liquidity

In the Marinade protocol, "Unstake Liquidity" is the number of SOL available in the [Unstake Liquidity Pool](../marinade-protocol/system-overview/unstake-liquidity-pool.md#overview). This pool is used by the "[Unstake Now](../marinade-protocol/system-overview/#unstake-now)" function and makes SOL available for an instant withdrawal against mSOL.&#x20;

### Validators

Validators are nodes that validate transactions by staking (locking) their SOL tokens to keep the Solana network secure. They receive compensation in terms of staking rewards to the proportion of the total tokens staked by them. In order to stake more SOL, they can be delegated SOL by users who wish to contribute to their node in exchange for a share of their rewards.
