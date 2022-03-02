---
description: >-
  You'll find the answers to most of your questions here! If something is not
  yet answered, reach out to us on our Discord.
---

# FAQ

## **What is Marinade?**

Marinade.finance is a liquid staking protocol built on Solana. People stake their Solana tokens with Marinade using automated staking strategies and receive "staked SOL" tokens (mSOL) that they can use in DeFi or unstake at any time to swap back to SOL.

## Is Marinade custodial?&#x20;

No, Marinade is a non-custodial protocol. This means that your tokens are in your possession and always accessible.

Marinade is also permisionless, meaning that our bot or our smart contracts can be interacted with, even in the absence of the team.&#x20;

## **What is liquid staking?**

Liquid staking is an alternative to traditional staking: it allows users to stake any amount of SOL and to effectively unstake their SOL without the requirement of waiting 1\~3 days before the stake is warmed up or cooled down. Warming up or cooling down stake normally takes around 3 days.

## **How long does it take to stake and unstake?**

With Marinade, you can stake SOL and/or unstake SOL immediately. There is no waiting time with our [liquid staking solution](../marinade-protocol/system-overview/). However, immediate unstake will involve [fees](faq.md#what-fees-does-marinade-charge) (0.3% to 3%).&#x20;

You are also free to use the [delayed unstake](../marinade-protocol/system-overview/#delayed-unstaked) to get your SOL back without any fee. However, you will have to wait 1-2 epochs to get back your SOL and the accumulated rewards.&#x20;

{% hint style="info" %}
The time displayed on your claim ticket (when using the delayed unstake option) is displayed in your local timezone.
{% endhint %}

## **Are staking rewards staked automatically?**

Staking rewards are compounded automatically into the staked SOL.

## **What fees does Marinade charge?**

The fee structure of Marinade is as described below:

| Deposit fee                            | 0%                                                     |
| -------------------------------------- | ------------------------------------------------------ |
| Delayed unstake (1-2 epochs wait time) | 0%                                                     |
| Unstake now                            | 0.3% - 3%                                              |
| Commission                             | 1.95% on rewards (translates to \~0.14% on staked SOL) |

#### Deposit fee

Marinade does not charge any fee to deposit your SOL.

#### Delayed unstake

Marinade does not charge any fee for unstaking provided a user waits 1-2 epochs by using the delayed unstake feature.

#### Unstake now!

On Marinade, your SOL is not locked and you are free to withdraw it instantly at any time by paying a small fee.

The immediate unstake fee varies between 0.3% and 3% and depends on the total liquidity available in the Marinade pool and the amount to unstake. Marinade’s liquidity target is set at 100,000 SOL. As long as this target is maintained after unstaking, the fee will be at 0.3%.

If the liquidity in the Marinade pool goes below the given threshold, the "Unstake now!" fee is calculated as:

> unstake\_fee = max\_fee - (max\_fee - min\_fee) \* amount\_after / target

where:

* max\_fee = 3%&#x20;
* min\_fee = 0.3%
* amount\_after = liquidity remaining after unstaking&#x20;
* target = 100,000

{% hint style="info" %}
These parameters are used currently but could change. In the future, the Marinade DAO will be responsible for the fee structure and will vote on the parameters.&#x20;
{% endhint %}

The unstake now fee can also be viewed in the Marinade dashboard when you enter the amount of mSOL you want to unstake.

#### Commission

Marinade has an ongoing management fee of (\~0.14% p.a.) to support further product development. It is automatically taken from your staking rewards and represents 2% of your rewards.&#x20;

Eg. If you have 100 SOL staked for 1 year with a staking return of 7%, you would have earned 7 SOL with your rewards. Marinade takes a 1.95% commission on those rewards each epoch, amounting to 0.14 SOL and you are keeping 98.05% of the reward (6.86 SOL).&#x20;

Like the previous parameters, our management fee can be changed by the Marinade DAO. However, for the foreseeable future, our management fee will be 1.95%. This is the **only mandatory fee** when using Marinade.&#x20;

## Has Marinade been audited?

Back in July, while still on devnet, we asked [the Solana Foundation](https://solana.foundation) for recommendations of auditors who know the ins and outs of protocols running on Solana. They introduced us to the [Neodyme](https://neodyme.io) team (previously called ALLES! One), who reviewed most of the major protocols and even came up with a summary article: [Solana Smart Contracts: Common Pitfalls and How to Avoid Them](https://blog.neodyme.io/posts/solana\_common\_pitfalls). We passed their code review with no critical issues found, and after confirming this with another set of white-hat hackers we decided it was a green light for us to launch on mainnet.

* Their audit is available here: [https://marinade.finance/Neodyme.pdf](https://marinade.finance/Neodyme.pdf)

During our first week on mainnet, we started another audit with[ Ackee Blockchain](https://www.ackeeblockchain.com) and passed yet again with no critical issues by the end of August.

* Their code review is available here: [https://marinade.finance/AckeeBlockchain.pdf](https://marinade.finance/AckeeBlockchain.pdf)

We also submitted our protocol to an audit by [Kudelski Security](https://kudelskisecurity.com) which was published in November 2021.&#x20;

* Their audit is available here: [https://marinade.finance/KudelskiSecurity.pdf](https://marinade.finance/KudelskiSecurity.pdf)

To learn more about our security and multisig you can read our Medium article '[**Why We Take it Slow — Security First**](https://medium.com/marinade-finance/why-we-take-it-slow-security-first-ed9a2e17e3ac)**'.**

## **Where are my SOL tokens?**

When you deposit your tokens, Marinade automatically diversifies, delegating on the top-performing validators. You will receive 'marinated SOL' (mSOL) tokens back in your wallet. mSOL can be unstaked to receive your SOL tokens back, plus rewards. mSOL increases in value every epoch relative to SOL.

## Where can I see the validators Marinade delegates to?

You can find the full list of our current validators on [our website](https://marinade.finance/app/staking) or [Solana Beach](https://solanabeach.io/address/4bZ6o3eUUNXhKuqjdCnCoPAoLgWiuLYixKaxoa8PpiKk/stakes).

## How long does it take for a stake account to be redelegated?&#x20;

Marinade allows you to directly deposit your stake account and receive mSOL in exchange. This means that if you are already staking with a single validator, you can easily jump onboard.

But what happens if you are delegating to one of the top validators, excluded from our delegation strategy? Marinade will accept it and redelegate it shortly after (if your stake account is [eligible](faq.md#can-i-deposit-my-stake-account-directly)).&#x20;

Stake accounts are redelegated at the end of epochs and it can take 1 to 2 epochs to redelegate those stake accounts to validators chosen by our delegation strategy.&#x20;

## How can I get mSOL?

There are different ways of obtaining mSOL:&#x20;

* **Stake SOL to Marinade's staking pool and get mSOL**. This is the simplest way and has no fees.&#x20;
* **Trade mSOL on secondary markets** (centralized or decentralized exchanges like FTX, Raydium, Saber, etc.). Please keep in mind that in this case you are paying trading fees.&#x20;

## Where can I use mSOL?&#x20;

mSOL can be used in many DeFi protocols, all without losing your staking rewards.&#x20;

For example, you can:&#x20;

* Add mSOL to a liquidity pool on a decentralized exchange
* Lend your mSOL or use it as collateral on borrowing/lending protocols
* Supply mSOL to yield farming protocols
* Stake your mSOL to earn additional [MNDE rewards](../the-mnde-token/liquidity-mining.md#current-week)
* Trade your mSOL on CEXs and DEXs
* Etc.

We are always on the lookout for new protocols where mSOL could be integrated. Our[ DeFi page](https://marinade.finance/app/defi) contains a non-exhaustive list of mSOL use cases in DeFi.

## **Can I deposit my Stake Account directly?**&#x20;

Short Answer: **YES, it will help in the decentralization of the Solana ecosystem and its censorship resistance.**

Long answer: Yes, but your current validator:&#x20;

&#x20;  1\) Must not be delinquent&#x20;

&#x20;  2\) Must have a commission lower than 30%

If the previous conditions aren't met, then you need to deactivate the account, withdraw all the SOL, and deposit the SOL directly on Marinade.&#x20;

If you can't deposit your stake account, it can be for the following reasons:&#x20;

* Your stake account is not activated yet. This takes up to two epochs and you will have to try at a later time.
* Your stake account contains less than 1 SOL. We have a limit to avoid bots and overload.&#x20;

## I am a validator. Can I receive stake from Marinade?

Yes!&#x20;

Marinade is staking SOL to more than 450 validators. These validators are not whitelisted and do not have to do anything specific to be selected by Marinade's algorithm.&#x20;

You can refer to our [Delegation strategy](../marinade-protocol/validators.md) to see how our algorithm selects validators. You can also take a look at our[ Delegation formula](../marinade-protocol/validators.md#delegation-formula).

## **Any sale or IDO?**

We're bootstrapped and self-funded with help from ecosystem grants provided by Solana and Serum. We're not taking in any private investors or VC funds and are not doing any private or public sale. We plan to build our DAO around Marinade users.

## Is there any airdrop?

The last snapshot for the MNDE retroactive airdrop was taken on October 7th 2021. If you used the Marinade ecosystem before this date, you might be eligible for our upcoming MNDE airdrop.&#x20;

Missed out? No worries! You can participate in MNDE [liquidity mining ](../the-mnde-token/liquidity-mining.md)or be active in the Marinade community.&#x20;

## Do you have a governance token?&#x20;

The Marinade token (MNDE) was released on September 30th 2021 and is only accessible through liquidity mining or on secondary markets. Its max supply is 1 billion and you can find more information about it in our [tokenomics](broken-reference).

## When Marinade NFT?

Marinade Non-Fungible Chefs have been announced! Check[ this article](https://medium.com/marinade-finance/cooking-with-governance-introducing-marinade-non-fungible-chefs-8af7e54871ac) to learn more.

## Does Marinade vouch for the security of protocols using mSOL?

No. mSOL is a permissionless token that can be integrated anywhere and by anyone. If a project offers the possibility to use mSOL, this does not mean that the project is safe or audited by the Marinade team at all.&#x20;

We encourage you to always do your due diligence on the projects you invest in. If you have any doubts or questions, we will gladly discuss them with you on our Discord.&#x20;

## Why is the Orca mSOL/SOL pool not balanced?

As mSOL and SOL prices are correlated, Orca created what they are calling a stable pool. This stable pool does not have the same balancing requirements as other pools, as the values of the assets are correlated.&#x20;

We invite you to read the documentation provided by Orca on their [stable pools mechanism](https://docs.orca.so/#why-arent-stable-pool-pairs-balanced-like-other-pools).

