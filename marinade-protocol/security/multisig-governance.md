---
description: >-
  In order to modify our code or the parameters of our smart contracts, a
  multisig needs to be used. Let's see what this means.
---

# Multisig governance

## What is a multisig?

Multisig is a tool composed of multiple wallets that share the power on the decisions taken.&#x20;

With a multisig tool, one signature from one wallet is not enough; you need multiple signatures from different private keys, distributed across multiple parties and often on multiple continents. In order to validate any decision, a majority of the members will have to sign with their private key.&#x20;

Thanks to this, it is possible to **distribute the governance power among multiple wallet holders**.

Marinade decided that while waiting for DAO tooling, which will enable MNDE holders to directly vote on decisions, the best and most transparent way to ensure that our protocol is maximally decentralized was to use Anchor's Framework Multisig tools.&#x20;

With our multisigs (introduced below), a decision can only be implemented if it is validated by a majority of our multisig owners. This empowers our DAO and is a first step toward fully decentralized governance.

## Marinade multisigs

### Main multisig

Our first multisig is composed of 11 wallets, distributed among some of the most reputable parties in the Solana ecosystem:&#x20;

* [Raydium](https://raydium.io)
* [Saber](https://saber.so)
* [Serum](https://projectserum.com/#/)
* [Mercurial finance](http://mercurial.finance)
* [Orca](https://orca.so)
* [Alameda Research](https://www.alameda-research.com)
* [Triton.one](https://www.triton.one)
* [Miton C](https://mitonc.com)
* [Marinade team ](https://marinade.finance)(3 votes)

**This multisig controls contract-code upgrades**. To modify our smart contract, this multisig has to confirm it. For a decision governed by this multisig to go through, **a majority of 6 out of 11 has to be reached**.&#x20;

This system includes multiple trusted parties in the process to make sure that only agreed upon decisions are integrated in the protocol.&#x20;

This multisig ensures that no one is the sole owner of the code and can act maliciously without being stopped by other parties.

### Treasury multisig

Multisig has many advantages but a big multisig like our main one can be unnecessary for other needs. Marinade's second multisig controls all the treasury related decisions. This multisig is owned by the Marinade team and composed of 7 differents wallets shared among the Marinade team. This multisig controls the procotol treasury and the community MNDE account used to feed liquidity mining incentives to all our ecosystem partners. **A majority 4 out of 7 needs to be reached in order to execute related decision.**

### Operational multisig

Finally, Marinade has a third multisig that is used to modify operational parameters. This wallet is also controlled by the Marinade team and is composed of 5 different wallets, spread among Marinade stakeholders.

This multisig can modify the following operational parameters of the [mSOL-SOL liquidity pool](../system-overview/unstake-liquidity-pool.md):&#x20;

* `liquidity-target: 100,000 SOL`
* `max-fee: 3%`
* `min-fee: 0.3%`

This multisig can also modify the following operational parameters of the protocol:&#x20;

* `liquidity-sol-cap` (maximum SOL amount in the mSOL-SOL liquidity pool)
* `min-deposit: 0.000000001 SOL` (minimum SOL amount that can be staked)
* `min-stake: 1 SOL` (minimum SOL amount for stake/unstake actions executed by our bot and for depositing a stake account)
* `min-withdraw` (minimum SOL amount that can be withdrawn)
* `slots-for-stake-delta: 3 hours` (number of hours before the end of the epoch at which the bot starts to stake/unstake)
* `staking-sol-cap: 11M` (maximum SOL amount that can be staked in the protocol)
* `rewards-fee: 2%` (fees of the protocol)

For example, the multisig was recently used to raise the cap of staked SOL on Marinade (`staking-sol-cap`). With 3 audits and months of activity without any issues, this multisig will probably be used in the near future to fully remove this limit.&#x20;

{% hint style="info" %}
The `rewards-fee` parameter is now 2% (effective is 1.95%). There are **no plans to change it**, but if changed, it could never go above 10% (that limit is set in the code).
{% endhint %}

{% hint style="info" %}
Marinade aims to become a fully decentralized protocol, governed by MNDE holders. When DAO tooling is available and MNDE token is properly distributed_,_ most of these powers will be delegated and governed by the DAO.
{% endhint %}
