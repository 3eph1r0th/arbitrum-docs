This how-to is for **users** and **developers** who want to migrate (or "bridge") existing NFTs and NFT collections onto one of Arbitrum's layer-2 (L2) chains.

## Why migrate NFTs to Arbitrum?

There are two main reasons to migrate NFTs to Arbitrum:

 1. **Lower fees**. Arbitrum's gas fees are significantly lower than Ethereum's, meaning that you can mint, transfer, and trade NFTs without having to pay as much.
 2. **Fast transactions**. From the end-user's perspective, transactions on Arbitrum's rollup chains are processed more quickly than they are on Ethereum mainnet. This lets developers build NFT experiences that feel just about as fast as traditional web apps.

<!-- todo: when shouldn't you? Risks to call out? -->

:::caution

It's very important to understand that **the [Arbitrum Bridge](https://bridge.arbitrum.io/) does not support ERC-721 or ERC-1155 token transfers**; it supports transfers of **ERC-20 tokens** and **plain-old ETH** between Ethereum and Arbitrum's two chains.

:::

## NFT token-types and bridges

Before we begin, let's align on the various types of tokens that can be used as NFTs, and how they can be migrated to Arbitrum.

| Token type   | Description                                                             | Migration options                                                                                                                                                  |
| ------------ | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **ERC-20**   | Fungible tokens[^1] that can be transferred between users.              | - [Native token bridge](https://bridge.arbitrum.io/) <br/> - [Third-party bridge](#third-party-nft-bridging-solutions) <br/> - [DIY](#do-it-yourself-diy-bridging) |
| **ERC-721**  | Non-fungible tokens that represent ownership of a unique asset.         | - [Third-party bridge](#third-party-nft-bridging-solutions) <br/> - [DIY](#do-it-yourself-diy-bridging)                                                            |
| **ERC-1155** | A newer standard that allows for more flexibility in how NFTs are used. | - [Third-party bridge](#third-party-nft-bridging-solutions)  <br/> - [DIY](#do-it-yourself-diy-bridging)                                                           |


<!-- todo: fact check -->

## Migrate NFTs using the native token bridge

This option is suitable for **end-users** who want to independently migrate their **ERC-20 tokens** to Arbitrum. It's *not* the right option if you're trying to migrate other types of tokens, or if you're a developer who wants to batch-migrate all of your projects' user-owned tokens to Arbitrum. <!-- todo: is this true? -->

The [Arbitrum token bridge](https://bridge.arbitrum.io/) is a trustless, permissionless bridge that allows users to transfer **ERC-20 tokens** (not ERC-721 or ERC-1115 tokens) between Ethereum and <a data-quicklook-from="arbitrum-one">Arbitrum One</a> and <a data-quicklook-from="arbitrum-nova">Nova</a> chains. To use the bridge, visit the [Arbitrum Bridge portal](https://bridge.arbitrum.io/) and follow the instructions.


## Migrate NFTs using third-party NFT bridging solutions
 
This option is suitable for **end-users** and **developers** who want to migrate **non-ERC-20 tokens** (e.g. ERC-721 or ERC-1155 tokens) to one of Arbitrum's chains. There are many things to consider before using a third-party bridging solution, including:

 - Token metadata
 - Royalty mechanisms
 - Perception of which chain's NFTs are canonical
 - Representational clashes if multiple bridges are used for the same collection
 - etc

Using a third-party bridging solution may introduce new trust assumptions, forcing you to compromise with properties of permissionlessness and/or trustlessness. Consider these tradeoffs carefully when deciding to use any of the below solutions, and proceed with caution. This list is presented in alphabetical order, and does not represent an endorsement or recommendation; it's simply a list of options that are available, shared with the expectation that you'll **do your own research before using them**:

- [Axelar](https://axelar.network/)
    - Currently live on Arbitrum One for ERC721 and ERC1155
- [Layer Zero](https://layerzero.network/)
    - Currently live on Arbitrum One for ERC721 and ERC1155
- [Wormhole](https://wormhole.com/)
    - Currently live on Arbitrum One for ERC721
- [XP Network](https://xp.network/)
    - Currently live on Arbitrum Nova for ERC721 and ERC1155


### Other third-party solutions

There are some solutions that give you the best of both worlds: **canonical representation of foundational NFTs on their original chain**, *and* **Arbitrum's scaling capabilities to facilitate fast and cheap experiences**:

 - **Pirate Nation** has implemented a solution they coined as **[mirroring](https://piratenation.medium.com/mirroring-trade-on-l1-play-on-l2-3f53068a6a44)**, which allows users to trade NFTs on Ethereum and play with the mirrored versions of those NFTs on Arbitrum Nova. The NFTs on Nova's L2 chain can be transferred by a custodial central entity, but the NFTs on L1 remain fully self-custodial. This solution entirely avoids the need for bridging.
 - **0xEssential**'s [NFT Global Entry](https://docs.0xessential.com/0xessential/guides/nft-global-entry) offers a similar solution by hosting a public oracle that generates ownership proofs; these proofs can be easily consumed and used by their SDK.


## Migrate NFTs using do-it-yourself (DIY) bridging

This option is suitable for **developers** and project owners who want to migrate **non-ERC-20 tokens** and/or entire collections of tokens that have already been minted and distributed to users on Ethereum's L1 chain. There are four main options in this category:

1. **Set up cross-chain messaging between an old NFT contract to a new one on Arbitrum.** High engineering cost; seamless and unobtrusive UX for end-users.
2. **Mint a new collection on Arbitrum and distribute NFTs to existing holders.** No engineering cost; requires users to claim their NFTs on Arbitrum; carries assumptions about your intended use-case.
3. **Build contracts on Arbitrum that depend on NFT ownership from other EVM chains.** Low engineering cost; carries assumptions about your intended use-case.
4. **Building your own NFT Bridge.** High engineering cost; high flexibility.

### Build your own NFT bridge

The below workshop was hosted by a blockchain engineer at Offchain Labs, and walks you through the process of building a trustless ERC-721 bridge.

:::caution

The code in this workshop is provided for educational purposes only; it hasn't been audited and was designed for clarity of live demonstration (not for gas optimization, flexibility of functionality, etc). Use at your own risk and make sure to thoroughly review and test before using in any production environment.

:::

<iframe width="560" height="315" src="https://www.youtube.com/embed/7fyyaPuPtW0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


[^1]: Although ERC-20 tokens are fungible (mutually exchangeable with no expectation of uniqueness between tokens), they can and have been used to represent ownership of unique digital assets. For example, CryptoKitties and CryptoPunks were originally implemented as ERC-20 tokens with additional code that made each token uniquely identifiable. This use-case led to the [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/) standard, which offers protocol-canonical support for non-fungible tokens.