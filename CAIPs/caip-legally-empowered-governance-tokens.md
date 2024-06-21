---
caip: CAIP-LEGT
title: Legally Empowered Governance Token Standard for Real World Assets
author: Tony Nacumoto (@tonynacumoto)
discussions-to: <https://docs.legt.co> 
status: Draft
type: <Standard | Meta>
created: 2020-02-02>
updated: <2024-07-20>
requires: <ERC-173, ERC-721>
---
## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the CAIP.-->
A standard to address how to satisfy jurisdictional compliance for real world asset tokens.

## Abstract
<!--A short (~200 word) description of the technical issue being addressed.-->
Physical asset types are so diverse and jurisdictions so varied that in order for any kind of standard to address them all we must create a very simple mechanism in which the needed flexibility may occur.

## Motivation
<!--The motivation is critical for CAIP. It should clearly explain why the state of the art is inadequate to address the problem that the CAIP solves. CAIP submissions without sufficient motivation may be rejected outright.-->
Real World Assets are vital to integrate.  If we don't define a clear, simple token standard then we will only inherit the fragmented issues found today in the the off-chain world, which makes international commerce complicated.
We have the opportunity to create a standard that will allow interoperability accross all jurisdictions so that RWAs may enjoy the same modularity that popular standards like ERC20 & ERC721 enjoy today allowing for a robust ecosystem.

## Specification
<!--The technical specification should describe the standard in detail. The specification should be detailed enough to allow competing, interoperable implementations. -->
Our interface extends ERC-173 & ERC-721 to provide owner abilities to all significant functions in the contract.
It is important to note that the address of the owner be someone that can be held accountable and will not act unless direct to do so by the powers that be.
This same pattern must also be applied to any cooresponding token referenced as a fractional representation.
```
function *_owner (){
    // place duplication of contract function here with any needed alterations for owner to execute
};
```
It will also include a "lock" function that will lock the metadata of an NFT to prevent any future tampering at a certain point:
```
function lock onlyOwner(id){
    // updates a mapping to be used in a "onlyUnlocked" modifier that restricts the updaing of metadata in the _setTokenURI function used in ERC-721
};
```
There will be some additional public variables, such as the URI for the attached legal document. 
While an attached ERC-20, or ERC-1155 token is not neccessary in all instances, it is likely that each LEGT NFT will be paired with a token that represents fractional representation of the rights & responsibilities descirbed in the legal document attached.  
In which case it should be described as a public variable so that it's value can be used in other contracts that reference it.
```
string public documentURI; // the legal documentation linking the token to the real world asset
string public ownerInfo; // identifying information for who the jurisdictional admin is for the token, such as a name, address, phone number, email etc
string public status; // review | verified | revoked | archive - used to identify how the token sits in respect to it's jurisdictional compliance.

string public linkedToken; // optional address of token.  This will be present on both the NFT and it's linkedToken so anyone can verify a 1:1 relationship.
string public linkedTokenStandard; // optional to allow for contract logic as needed, could use "supportsInterface" as well.
```
There will most likely be sub-standards that will be defined, such as what attributes to include in the metadata of the NFT for specific asset classes.
An example of this is for any real estate token to have a longitude & latitude defined using the OpenSea attribute standard. 
These standards will most likely vary from jurisdiction to jurisdiction and can be re-defined as needed.  A governing board will most likely help curate these similar to the pattern CAIP / EIP uses.
```
{
      "display_type": string, 
      "trait_type": string, 
      "value": string | number
}
```
In instances that an asset has profits to distribute, needs to be liquidated or has been destroyed and compensation needs to be dispersed the token can own the distribution and be accessed by token holders in relation to their balance.
```
function claim (){
    // transfered tokens owned by the contract in proportion to their balance
}
```

## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->
The reationale behind this approach is to allow for maximum flexibility.  It places a lot of responsibility upon the owner of the contract.  This is an inherit flaw and goes against some innate blockchain sentiment as it creates a "backdoor".  However, this backdoor is necessary for jurisdictional compliance so is a necessary evil. While there are standards that ensure compliance with specific locals such as USA SEC etc, we desire a broader international use case.
Our flexibility allows for SEC type regulations to occur, but does not impose uneeded restrictions or functionality for non-SEC regulated assets.


## Test Cases
<!--Please add diverse test cases here if applicable. Any normative definition of an interface requires test cases to be implementable. -->

## Security Considerations
<!--Please add an explicit list of intra-actor assumptions and known risk factors if applicable. Any normative definition of an interface requires these to be implementable; assumptions and risks should be at both individual interaction/use-case scale and systemically, should the interface specified gain ecosystem-namespace adoption. -->

## Privacy Considerations
<!--Please add an explicit list of intra-actor assumptions and known risk factors if applicable. Any normative definition of an interface requires these to be implementable; assumptions and risks should be at both individual interaction/use-case scale and systemically, should the interface specified gain ecosystem-namespace adoption. -->

## Backwards Compatibility
<!--All CAIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The CAIP must explain how the author proposes to deal with these incompatibilities. CAIP submissions without a sufficient backwards compatibility treatise may be rejected outright.-->
All CAIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The CAIP must explain how the author proposes to deal with these incompatibilities. CAIP submissions without a sufficient backwards compatibility treatise may be rejected outright.

## References 
<!--Links to external resources that help understanding the CAIP better. This can e.g. be links to existing implementations. See CONTRIBUTING.md#style-guide . -->

- [CAIP-1][CAIP-1] defines the CAIP document structure

[CAIP-1]: https://ChainAgnostic.org/CAIPs/caip-1

## Copyright
Copyright and related rights waived via [CC0](../LICENSE).
