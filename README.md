# ETH_ColdBrainWallet
Ethereum brain wallet that can be inferred from several input parameters with transactions signing, fully offline.

## Functionality:
### Offline Ethereum wallet (private key and address) generation as a function of 3 parameters ([original idea and code](https://www.reddit.com/r/ethereum/comments/535ovp/is_there_a_javascript_library_for_generating/d7q8hq7/?st=j7gaygm8&sh=435756ff)):
  1. Hardness: integer value in [1000, 3000] range. This (with the function iteslf) ensures to take some coputational effort to get key. Thus making more time consuming to brute-force key. 
  2. Email. This ensures possible attack to be personal. Protecting against non-personal large scale brute-forse search for non empty wallets. 
  3. Secret phrase. Actually a password. Should be long enough and not used anywhere else.
  
     Function is recursive:
     
     Step_(1)_: keccak_256[>hardness * (email + phrase)]
     
     Step_(hardness)_: keccak_256[Step(hardness-1)]

## Dependencies: 
1. Browserifyed [ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx) v1.3.3 for general Ethereum / crypto functions.
2. [QRCode.js](https://github.com/davidshimjs/qrcodejs) for QR Codes.

These is also standalone version where all js libraries are embedded into single html. This could be more convinient when transferring and using in different devices. It could be used on an old smartphone with no internet access for an example.

