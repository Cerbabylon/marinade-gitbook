---
description: >-
  When you stake your SOL on Marinade, they are delegated to a number of
  validators. How are these validators chosen? Can you be one of them? Let's
  review in details Marinade's delegation strategy.
---

# Delegation Strategy

## How are validators selected by our algorithm?

Marinade follows the Solana Foundation strategy to **spread the stake among the long tail of high-performance, low-commission, non-concentrated validators**, in order to increase decentralization and censorship resistance for Solana.&#x20;

![Solana Foundation delegation strategy](https://lh5.googleusercontent.com/93GZfqjM\_ciC\_MXOL349QCnCC81S-r4w0yvUt-kcKdyy2zOGpiWdiUPw4xVM5lQZbqGUEbEpTs2WdXr3cXuyuSiDx3OstnpkPDU6m6Nhe9Bk1jxP4HQZm5vNt4hHGOHQtEQcuyxs)

As you can see, this translates by delegating SOL to **** [**nodes that do not belong to the security group**](https://medium.com/solana-labs/announcing-the-solana-foundation-delegation-strategy-5bcccf9104ab)**.** (i.e. Marinade is not staking to big validators that are already in place, but trying to encourage and support more validators to exist).&#x20;

Once those nodes are excluded, here are the different parameters that are taken into account in the validator score:&#x20;

* Performance (APY)
* Commission
* Delinquency
* Decentralization objectives&#x20;
* Version of the node

{% hint style="info" %}
[StakeView](https://stakeview.app) is used to check APY and validators.app is used to determine your data center. The rest is directly extracted from Solana itself. \
This allows us to penalize the score of validators that are concentrated in the same data center, as we aim to decentralize the network as much as possible. If you encounter an issue with the data center displayed by validators.app, please reach out to them.
{% endhint %}

We evaluate **all validators.** Our formula and the code to compute it are available online and the results are published on-chain.&#x20;

**The ethos is to be totally transparent and open to all validators.**&#x20;

{% hint style="info" %}
Our target is to balance the best value for our users and value means APY but also SOL market cap. For example, making Solana more decentralized and censorship resistant will help all SOL token holders and can be reflected in SOL price.&#x20;
{% endhint %}

## **Delegation formula**

Marinade uses **open-source code to compute a “score”** awarded to validators **based on performance, commission and decentralization objectives**.

For example, a validator will get points added for good performance, low delinquency and low commission, but will get all points deducted if it’s already one of the top concentrated validators (measured by stake) in the Solana ecosystem.&#x20;

Based on their received points, validators are automatically awarded a percentage of the total stake. As users stake and unstake, Marinade bot distributes stake and unstake operations as to match staked percentage with score (i.e. changes in score are slowly applied as users stake and unstake)&#x20;

### Open source **calculation**

The results of the calculations and a SQLite database with historical data is published each epoch here:  [https://github.com/marinade-finance/staking-status](https://github.com/marinade-finance/staking-status)

You can preview what the staking bot will do, by executing this SQL query on the published database:

```
select should_have - marinade_staked, A.* 
  from scores2 A
  where epoch = 281
    and should_have > marinade_staked
  order by score desc
```

To compute validators metrics, Marinade is using a forked version of the SPL Stake-o-Matic code (from the Solana Program Library), available here: [https://github.com/marinade-finance/delegation-strategy](https://github.com/marinade-finance/delegation-strategy). It is very similar to the Stake-o-Matic while adding improvements and allowing to compile the score and apply post-processing computations directly.

### Calculation details

Here are the different steps used to calculate score and post-process it to determine staking/unstaking operations:&#x20;

1. A scoring is performed on **all validators**, based on the last 5 epochs. This score is based on the fork of the Stake-o-matic, available in [this repository](https://github.com/marinade-finance/delegation-strategy). It takes into account _Epoch credits_, _Commission_, _Decentralization_ (by analyzing the Data Center used) and _Node Version_.&#x20;
2. The top 300 validators according to this score are selected (and will vary each epoch). All the others validators will get a 0 score.&#x20;
3. All validators are analyzed (to identify the unstakes needed.) For stake operations, the performance for the **ongoing epoch** will only be analyzed for those 300 top validators, and some factors then modify the score:&#x20;

**Credits within the epoch are observed** (in relation to **all** validators on the blockchain):&#x20;

* If the credits for the validator are below 80% of the average, an emergency unstake will be performed at the moment where this is observed.
* If the credits for the validator are below 90% of the average of other validators, the score is divided by 2.&#x20;

**APY within the epoch is observed** (in relation to the average of **all** validators that have >4% APY on the blockchain):&#x20;

* If the APY is less than 50% of the average, an emergency unstake will be performed at the moment where this is observed.
* If the APY is less than 80% of the average, the score is divided by 2.&#x20;

**Delinquency**, based on the `solana validators` command is then taken into account.&#x20;

4\.  Those calculations are run twice during the epoch (for backup and accuracy purposes), one time 24 hours before the estimated end of the epoch, and one time 7 hours before. Scores are then uploaded on-chain.

### **Staking/Unstaking operations**

Finally, the bot responsible for staking and unstaking operations runs a last set of adjustments on the on-chain scores and analyze them to find a good balance between staking and unstaking operations, depending on the available stake to distribute or to unstake. For example, even in the case of a positive stake delta, meaning that Marinade has to add stake to new validators, some unstake operations may be needed.&#x20;

Here are the detailed steps of this final computation:&#x20;

* Some validators are [blacklisted](https://github.com/marinade-finance/delegation-strategy/blob/main/cli/score-post-process/src/process\_scores.rs#L561) for cheating the system or changing their fees at the last possible time before the end of the epoch. Every epoch, any stake in such a validator will be unstaked immediatly.&#x20;
* If the score of a validator is 0 (e.g. not in the top 300) and Marinade delegates more than 0.45% of its total stake to the validator, it gets unstaked unless Marinade represents more than 20% of their total stake.&#x20;
* If a validator has more than 250% of the stake they should have from Marinade, it gets unstaked unless Marinade represents more than 20% of their total stake.&#x20;
* A Maximum Stake cap has been implemented and is set at 1.5% of the total Marinade stake.
* Finally, one last cap is applied: the **received stake for an epoch cannot be superior to 0.1% of the overall stake currently delegated to validators**.
  * There is one exception: if the validator is severely understaked (could potentially receive more than 2x their current Marinade stake), their score is capped to 80% of their current score and they will not be affected by this cap.

{% hint style="info" %}
**Note:**  Having a 0 score **** for a validator **does not mean** the automated bot will unstake all from the validator. It only means it will not stake in the next epoch and will unstake if users requests large unstake orders.
{% endhint %}

{% hint style="info" %}
**Note:** No matter the previous epoch score, delinquent validators are always unstaked.
{% endhint %}

{% hint style="info" %}
**Note:** The selection parameters can be adjusted after each epoch, based on performance results and with the objective to increase token holders value. In order to do that we look for **a good balance between maximizing user's APY (direct method) and increasing Solana censorship-resistance (indirect method, increase network value and then SOL price)**. All changes are public and available in the [Changelog](../changelog.md) and each validator is able to pre-compute its own score.&#x20;
{% endhint %}

## Who is Marinade delegating to?

Currently, Marinade delegates SOL to more than 450 validators.&#x20;

You can see the full list of our current validators on [our website](https://marinade.finance/app/staking) or [Solana Beach](https://solanabeach.io/address/4bZ6o3eUUNXhKuqjdCnCoPAoLgWiuLYixKaxoa8PpiKk/stakes).

## How are stake accounts handled?&#x20;

If you already are staking your SOL, you own a stake account linked to a specific validator. You can deposit this stake account on Marinade and receive mSOL in exchange but your validator needs to:

* Have a commission under 30%.
* Not be delinquent

If this is not the case, your stake account will not be accepted. You will have to unstake and retrieve your SOL before depositing them directly on Marinade.
