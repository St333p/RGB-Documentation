# Standard Interfaces by LNP/BP Association

In this section, we will provide some description of the Interface standards developed by the [LNP/BP Association](https://www.lnp-bp.org/) which represent a good starting point to work with RGB. The list is divided into [already-coded interfaces](https://github.com/RGB-WG/rgb-std/tree/master/src/interface) (ready-to-use) and interfaces that will be developed in the future.

It's important to point out again that Interface provides naming to data structure and operation to be used in the wallet or to be visualized by users, but the actual "contract job" is done primarily by the [Schema](../schema/) to which the appropriate [Interface](../../annexes/glossary.md#interface) (or set of Interfaces) can be connected through the respective [Interface Implementation](../../annexes/glossary.md#interface-implementation)(s).

## Ready-to-use Interfaces

The following Interfaces are compatible and tested to work with RGB consensus and standard libraries.

* **RGB20** is an interface that provides the same scope as ERC20's, but which actually allows much more functionalities than Ethereum's standard. **It is the RGB standard meant to address the parsing of any fungible asset**: stocks, bonds, or, in general, anything that requires fungibility. It can be connected for example to the [Non-Inflatable Asset (NIA)](https://github.com/RGB-WG/rgb-schemata/blob/master/src/nia.rs) contract Schema. Among the features that RGB20 possesses over the ERC20 standard, there are:
  * **Asset renaming** and the possibility to change other specifications such as the token **ticker**.
  * **Stock splits**, similar to those of the stock markets, or the possibility to **change the precision** of the token.
  * **Secondary issuance**, which can be unlimited, limited to specific values, or unique.
  * **Asset burning or replacement** by the issuer. The interface is designed to allow for specific parties to accomplish these operations or their combination, e.g. the issuance of a new contract which happens simultaneously with a burning action of the same asset. This feature allows for the reduction of the size of the contract [stash](../../annexes/glossary.md#stash) by the users, as the client-side data required to validate the new emission starts from the new issuance events allowing for the discard of burned asset data.
* **RGB21** is the interface that is designed to address **NFT contracts or in general any unique digital production contract** such as digital media, books, movies, music, etc. It can be connected to the [Unique Digital Asset (UDA)](https://github.com/RGB-WG/rgb-schemata/blob/master/src/uda.rs) contract schema. As interesting additional features, it provides:
  * The built-in support for direct fetch of the media file from the contract itself if its size it is below 16MB.
  * The possibility, for the Owner, to register an [engraving](../../annexes/glossary.md#engraving). With this feature, an owner may mark the possession of the asset allowing this information to be stored in the asset's history after it has been transferred. This feature is provided in order to leverage in a direct and trustless way some notable user's possession in the NFT exchange history.
* **RGB25** represents **a hybrid of RGB20 and RGB21 standards** thus addressing the need to interface **partially fungible asset** contracts. For instance, it is made for assets that need to be fractionated but which need to maintain a relationship with the unique root asset issued in the first place. A typical example would be the use of such an interface for real estate tokenized assets. It can be connected to [Collectible Fungible Asset (CFA)](https://github.com/RGB-WG/rgb-schemata/blob/master/src/cfa.rs) schema.

## Planned interface to be developed

These interfaces haven't been implemented yet, but their development has been planned for the future:

* **RGB22** is a standard interface meant to **implement digital identities**.
* **RGB23** is aimed at implementing a more advanced version of the [Opentimestamps Protocol](https://opentimestamps.org/) with additional features suitable to provide a provable commitment history of digital timestamped documents.
* **RGB24** addresses the need to interface to contracts providing a **Decentralized Domain Name System** like Ethereum's ENS.
* **RGB26** represents the RGB **standard for DAOs** which can have complex contract configurations.
* **RGB30** interface concept is very similar to an RGB20 interface, however, it can connect to contracts which embeds **decentralized issuance**. RGB30 is the only standard that is foreseen to use [state extensions](../../annexes/glossary.md#state-extension).

In the following section, we will report and give some comments on the code of the RGB20 Interface.

***
