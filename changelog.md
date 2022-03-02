---
description: >-
  All major modifications to Marinade protocol will be detailed here and
  communicated to our users in advance.
---

# 🗓 Changelog

{% hint style="info" %}
A dedicated changelog for the Marinade application is available on [Notion](https://marinade.notion.site/ae38d58b9bab46d7aba829518b5dc017?v=3c8807c10a8541a8ae5beaf1ee459c38).
{% endhint %}

## 02/21/2022

### Improvement - Validators' management

**Status**: Online.&#x20;

Marinade stakes SOL to validators using a set [delegation strategy](marinade-protocol/validators.md) where all validators have a score calculated each epoch.&#x20;

Before this update, Marinade was using the Solana program [Stake-O-Matic](https://github.com/solana-labs/stake-o-matic), before post-processing those scores to determine the stake and unstake operations to perform.   &#x20;

This program has been forked and modified in order to add small improvements and allow a better post-processing of the on-chain scores. Those changes have minor impacts on how the score is calculated.&#x20;

This new repository is open-source and available here:&#x20;

{% embed url="https://github.com/marinade-finance/delegation-strategy" %}

Another set of changes has been applied on the post-processing rules in order to improve the distribution of the stake and reach more validators than before, with the goal to spread the stake more evenly and decentralize the network even more. Some improvements have also been implemented to avoid 'overstaking' to validators and unstake them in some situations. Please check the Delegation Strategy page for details.&#x20;

{% content-ref url="marinade-protocol/validators.md" %}
[validators.md](marinade-protocol/validators.md)
{% endcontent-ref %}

If you are a validator and have questions or want to participate to the future discussions related to the delegation strategy, please join our [Discord](https://discord.com/invite/6EtUf4Euu6).&#x20;

## 01/14/2022

### Incident report - Bot operations delayed

**Status**: Fixed.&#x20;

On January 14th, the permissionless bot responsible for moving the staking rewards to the pool (causing the mSOL price to go up each epoch) was not able to finish all the planned operations because it ran out of SOL to perform them. This issue was resolved in a few hours and the operations were resumed and completed.&#x20;

This incident resulted in a delay of 24h in the mSOL/SOL price update.

A monitoring tool has been added on the same day to prevent this issue from happening in the future.&#x20;

## 01/09/2022

### Smart contract update - Delayed unstake period

**Status**: Confirmed and applied.

## 01/04/2022

### Smart contract update - Delayed unstake period

**Status**: Communication phase. Changes will be applied on January 4th 2022.&#x20;

* The number of epochs you have to wait when withdrawing your funds via the "Delayed unstake" function is reduced by one epoch.&#x20;

See the planned code modification on Github: [https://github.com/marinade-finance/liquid-staking-program/commit/028c6e579f662e8cc5b92344f96797f49c4eec88](https://github.com/marinade-finance/liquid-staking-program/commit/028c6e579f662e8cc5b92344f96797f49c4eec88)

Documentation will be updated to reflect the future changes once the change is active. See [Delayed Unstake](marinade-protocol/system-overview/#delayed-unstake).

For more information about the process, please see our [Medium](https://medium.com/marinade-finance/setting-security-standards-marinade-is-upgrading-a-smart-contract-6b7ce2b6dcd4) article.&#x20;
