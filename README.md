# ETH_ColdBrainWallet
Ethereum client side brain wallet that can be inferred on demand from several input parameters with transaction signing. Fully offline.

These is also standalone version where all js libraries are embedded into single html. This could be more convinient when transferring and using at different devices. It could be used on an old smartphone with no internet access for an example.

You can try it [online](https://amchercashin.github.io/ETH_ColdBrainWallet/ColdBrainWallet.html), but for real personal use you should download it from [github repo](https://github.com/amchercashin/ETH_ColdBrainWallet/) and put on a offline device.

## Goal
Find a sweet spot between safety from theft, safety from loss and ease of use.

## Functionality
### Offline Ethereum wallet (private key and address) generation as a function of 3 parameters (inspired by [original idea and code by Vitalik](https://www.reddit.com/r/ethereum/comments/535ovp/is_there_a_javascript_library_for_generating/d7q8hq7/?st=j7gaygm8&sh=435756ff)):
  1. Hardness: integer value in [1000, 3000] range. This (with the function iteslf) ensures to take some coputational effort to get a key. Thus making it more time consuming to brute-force. 
  2. Email. To protect from batch key picking attack, where keys generated for every popular password or phrase, then check for positive balance. 
  3. Secret phrase. Actually a password. Should be long enough, not a actual meaningfull phrase in any language, not a "popular" password and not used anywhere else.
  
     Function [keccak_256](https://en.wikipedia.org/wiki/SHA-3) implemented as recursive (but not a standardised SHA-3 version, but one that used inside Ethereum):
     
     Step_(1) = keccak_256[ hardness * ( email + phrase ) ]
     
     Step_(hardness) = keccak_256[ hardness * Step_(hardness-1) ],
     
     Where "+", "*" are string operations: concatenation and string multiplication.
     
     So in first step we concatenate _email_ and _phrase_, then concatenating this string with iteslf _hardness_ times to get one very long string. Then feed this string to keccak_256, which returns a hash: string of 64 hex characters always, despite the input.
     
     Every next step we take the result from previous step (string of 64 hex chars, without leading "0x"), concatenate it with iteslf _hardness_ times again, and then feed again to keccak_256. Repeat this _hardness_ times.
     
     Total steps = _hardness_ parameter.
     
     It takes form 10s on my laptop to 1.5 minutes on a smartphone to get keypair or sign transaction.

### Get address from any private key
Simply, infer Ethereum address from private key you can provide. Usefull if you have your own way to generate private key.

### Sign offline transaction
This can be done with key, generated on the fly again with hardness, email, and secret phrase parameters. Or with raw private key instead.

Generated transaction code contains no private information and could be safly posted everywhere (if you are going to actually make it, surely). To _make_ a transaction you should broadcast this code to the blockchain (use MyEtherWallet.com or etherscain.io servoces for an example).

## Dependencies: 
1. Browserifyed [ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx) v1.3.3 for general Ethereum / crypto functions.
2. [QRCode.js](https://github.com/davidshimjs/qrcodejs) for QR Codes.
