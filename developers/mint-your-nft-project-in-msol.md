---
description: We know how cool NFTs are, so we made it possible to mint NFTs using mSOL!
---

# Mint your NFT project in mSOL

## Set up Metaplex Candy Machine with mSOL

### Setup

* Download [Metaplex ](https://github.com/metaplex-foundation/metaplex)or clone it using Git on terminal.

`git clone https://github.com/metaplex-foundation/metaplex.git`

* Open your terminal and go to the downloaded Metaplex folder.
* Build CLI tools.

`cd js`

`yarn install`

`cd packages/cli`

`yarn build`

{% hint style="info" %}
Before you upload the metadata and create your candy\_machine, you need to make sure that you have the right wallet configuration by using Solana CLI.
{% endhint %}

* Once the wallet configuration is done, prepare the metadata and upload them to Arweave (IFPS).&#x20;
* Prepare your metadata and create an assets folder with them.&#x20;

`ts-node ./src/candy-machine-cli.ts upload ./assets --env devnet --keypair ~/.config/solana/wallet.json`

* Verify if the metadata were uploaded correctly.

`ts-node ./src/candy-machine-cli.ts verify --env devnet --keypair ~/.config/solana/wallet.json`

### Candy\_Machine creation

* To create a candy\_machine with mSOL, you need a treasury account to receive mSOL from the mint. To create the mSOL account for your wallet, use the command below.

`spl-token create-account mSoLzYCxHdYgdzU16g5QSh3i5K3z3KZK7ytfqcJm7So`

* Create your candy\_machine with price, token address and treasury account address.&#x20;

`ts-node ./src/candy-machine-cli.ts create_candy_machine --env devnet --keypair ~/.config/solana/wallet.json --`<mark style="color:blue;">`price 1`</mark>` ``--`<mark style="color:blue;">`spl-token mSoLzYCxHdYgdzU16g5QSh3i5K3z3KZK7ytfqcJm7So`</mark>` ``--`<mark style="color:blue;">`spl-token-account HeiKAj3ENkAam3rR6q9EtEiSuk2ZEXp87ypQUMBuxpV`</mark>

* Finally, you can set the launch time of the mint using the `update_candy_machine` command.

`ts-node ./src/candy-machine-cli.ts update_candy_machine --env devnet --keypair ~/.config/solana/wallet.json --`<mark style="color:blue;">`date 1638023250`</mark>

{% hint style="info" %}
The `update_candy_machine` command can also be used to modify the mint price.
{% endhint %}

Congratulations, your candy machine is now set up in mSOL!&#x20;
