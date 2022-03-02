# Unstake Liquidity Pool

## Overview

The Marinade mSOL/SOL unstake pool is an internal mSOL-SOL pool which is **intentionally unbalanced** and **operating at its best if 100% of its liquidity is filled with SOL** from liquidity providers.

### No Impermanent Loss

Because liquidity providers only deposit SOL, the Marinade Unstake Liquidity pool is **free from** [**divergent/impermanent loss**](https://www.solana.news/post/cryptonomics-what-is-impermanent-loss). You are guaranteed by code that you will remove the same or more SOL value than the amount you deposited (minus the 0.00001 transaction fees from Solana).

![Marinade unstake pool](<../../.gitbook/assets/image (7).png>)

This liquidity pool serves multiple purposes:&#x20;

* Provide immediate liquidity for unstaking.
* Match staking and unstaking orders (see [Order matching](unstake-liquidity-pool.md#order-matching)).
* Provide a fair-price, no-slippage source for mSOL liquidations.

The pool has a linear swap fee decreasing until the target liquidity is reached to cover for operation costs and incentivize liquidity providers. 75% of the fees goes to liquidity providers and 25% to the Marinade treasury.

{% hint style="info" %}
Current parameters are:\
\- max fee: 3%\
\- min fee: 0.3%\
\- liquidity target 100,000 SOL
{% endhint %}

![Fee structure of the mSOL/SOL pool. As long as the liquidity target is maintained after your unstake, the fees will be 0.3%.](<../../.gitbook/assets/image (8).png>)

Any user can become a liquidity provider.&#x20;

Liquidity providers can add or remove liquidity at any time, and they receive a LP Token representing their share of the liquidity pool. As other users utilize the liquid-unstake option, fees are added to the pool and then to LP's share value.

![Composition and flow of the mSOL/SOL liquidity pool.](<../../.gitbook/assets/image (5).png>)

### Example

Let's take a scenario where the parameters of the pool are close to the current situation:&#x20;

* Unstake liquidity: 581,250 SOL
* Amount you want to unstake immediately: 90 SOL

Your fees are calculated as such:&#x20;

> 581,250 - 90 = 581,140
>
> Is 581,140 above 'liquidity target'?
>
> Yes. The fees are 0.3%.
>
> 90 SOL - 0.3% = 89.73 SOL

You receive 89.73 SOL after your transaction and you pay 0.27 SOL in fees for unstaking without delay.&#x20;

Now, let's take a (fictive) scenario where the parameters of the pool are very different:

* Unstake liquidity: 100,030 SOL
* Amount you want to unstake immediately: 9030 SOL&#x20;

Your fees would be calculated as such:&#x20;

> 100,030 - 9030 = 91,000
>
> Is 91,000 above 'liquidity target'?&#x20;
>
> No. We calculate the fees with the following formula:
>
> unstake\_fee = max\_fee - (max\_fee - min\_fee) \* amount\_after / target
>
> unstake\_fee = 3 - (3 - 0.3) \* 91,000 / 100,000
>
> unstake\_fee = 3 - 2.457 = 0.543
>
> 9030 - 0.543% = 8980.9671 SOL

In this scenario, you would receive 8980.9671 SOL immediately and pay 49.0329 SOL in fees.

{% hint style="info" %}
As you can see, in some cases 'Unstake now' will generate more fees because your withdrawal impacts the liquidity of the pool. In this situation, consider using ['Delayed unstake'](./#delayed-unstaked) if you want to avoid fees.&#x20;
{% endhint %}

### **Order matching**

To minimize unnecessary operations and achieve the best efficiency of the liquidity pool, Marinade continuously adjusts the liquidity pool to be 100% SOL. This is how it’s done:

1. Once an immediate unstake operation is done, the liquidity pool now includes the mSOL (sent by the user unstaking) and original SOL liquidity.&#x20;
2. When another stake operation is called, the mSOL is provided from the liquidity pool.
3. Marinade refills the liquidity pool with user deposited SOL at no cost for the user to achieve pool adjustments and full liquidity for immediate unstaking.
