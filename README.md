# ETH_ColdBrainWallet
Ethereum brain wallet that can be inferred from several input parameters with transactions signing, fully offline.

Basically, an offline MyEtherWallet clone with brain wallet generation algorithm. 

These is also standalone version where all js libraries are embedded into single html. This could be more convinient when transferring and using in different devices. It could be used on an old smartphone with no internet access for an example.

## Goal
Find a sweet spot between safety from theft, safety from loss of private key and ease of use.

## Functionality
### Offline Ethereum wallet (private key and address) generation as a function of 3 parameters ([original idea and code by Vitalik](https://www.reddit.com/r/ethereum/comments/535ovp/is_there_a_javascript_library_for_generating/d7q8hq7/?st=j7gaygm8&sh=435756ff)):
  1. Hardness: integer value in [1000, 3000] range. This (with the function iteslf) ensures to take some coputational effort to get key. Thus making more time consuming to brute-force key. 
  2. Email. This ensures possible attack to be personal. Protecting against non-personal large scale brute-forse search for non empty wallets. 
  3. Secret phrase. Actually a password. Should be long enough and not used anywhere else.
  
     Function [keccak_256](https://en.wikipedia.org/wiki/SHA-3) implemented as recursive (not a standardised SHA-3 version , but one that used inside Ethereum):
     
     Step_(1) = keccak_256[ hardness * ( email + phrase ) ]
     
     Step_(hardness) = keccak_256[ Step( hardness - 1 ) ]
     
     So in first step we concatenate _email_ and _phrase_, then repeat and concatenating this string _hardness_ times to get one very long string. Then feed this string to keccak_256.
     
     Every next step it takes the result from previous step (now 64 hex chars always) and feed again to keccak_256. 
     
     Total steps = _hardness_ parameter.

### Get address from any private key
If you have your own way to generate private key.

### Sign offline transaction
This can be done with key, generated on the fly with hardness, email, and secret phrase parameters. Or with raw private key instead.

Generated transaction code contains no private information and could be safly posted everywhere. To _make_ a transaction you should broadcast this code to the blockchain (use MyEtherWallet.com or etherscain.io for an example).

## Dependencies: 
1. Browserifyed [ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx) v1.3.3 for general Ethereum / crypto functions.
2. [QRCode.js](https://github.com/davidshimjs/qrcodejs) for QR Codes.
