## Description
Phoebe is an epistemic model checker for privacy properties in security protocols. 

### Features
* Phoebe implements a symbolic model of security protocols: messages are expressed as algebraic terms (not bitstrings) and a Dolev-Yao attacker is assumed 
* Phoebe works for protocols with bounded number of sessions.
* Phoebe assume a limited Dolev-Yao attacker: the DY attacker can only swap well typed terms
* Privacy properties are expressed with an Epistemic Logic Language
* Protocols are modelled using a Send/Receive language
* The user input: 
  - the protocol description
  - an epistemic formula expressing the desired property
  - the domains for protocol names, and long-term keys if necessary
  - the maximum number of sessions
* The protocol model in Phoebe is an Interpreted System


## Examples
* Private Authentication Protocol (By Abadi) 
* Basic Hash Protocol
* A Tag-Reader protocol

## Installation

You should have the [Haskell Tool Stack](https://haskellstack.org) installed.

    cd phoebe
    stack build
    stack ghci

## Usage Examples

Examples with PrivateAuth* and PrivateAuth

    > sat privAuthX (Neg goal3)
      Just [1.(a,A,1,{kb})!: (n1){⟨a,n1⟩}_b
      ,1.(a,C,1,{kb})?: (b,n2,a){⟨b,n2⟩}_a
      ,2.(a,C,1,{kb})!: (n3){⟨a,n2,n3⟩}_b
      ]
    > sat privAuth (Neg goal3')
      Nothing

Example with Basic Hash Protocol
Note that sat `negStrongUnlinkabilityBH` 

    > satNegStrongUnlinkabilityBH
      Just [1.(t1,T,1,{})!: (n1)⟨n1,hash(⟨n1,k1⟩)⟩
      ,1.(t1,T,2,{})!: (n2)⟨n2,hash(⟨n2,k1⟩)⟩
      ,1.(t1,T,3,{})!: (n3)⟨n3,hash(⟨n3,k1⟩)⟩
      ] 


Example with the Tag Reader Protocol TR

    > satKeyLinkTR
      Just [1.(t1,T,1,{})!: (n1)⦃n1⦄_k1
      ,1.(t2,T,2,{})!: (n2)⦃n2⦄_k1
      ,1.(r1,R,1,{k1,k2})?: ()⦃n1⦄_k1
      ,2.(r1,R,1,{k1,k2})!: (n3)⦃n3⦄_k1
      ,2.(t1,T,1,{})?: ()⦃n2⦄_k1
      ,2.(t2,T,2,{})?: ()⦃n1⦄_k1
      ,3.(t1,T,1,{})!: ()⦃⟨n2,n1⟩⦄_k1
      ,3.(t2,T,2,{})!: ()⦃⟨n1,n2⟩⦄_k1
      ]



## Todos
* Parser for protocol input
* Parser for epistemic formulas
* factor Abs in mes1 mes1' of LoRaWAN (2022-04-26 14:49:15)
* Datum takes name, be careful at possSigmaImages, at suitable in ProtModel

