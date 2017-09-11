# ETH_ColdBrainWallet
Ethereum brain wallet that can be inferred from several input parameters with transactions signing, fully offline.

Functionality:
- Offline Ethereum wallet (private key and address) generation as a function of 3 parameters:
  1. Hardness: integer value in [1000, 3000] range.
  2. Email.
  3. Secret phrase. 
Dependencies: 
1. Browserifyed [ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx) v1.3.3 for general Ethereum / crypto functions.
2. [QRCode.js](https://github.com/davidshimjs/qrcodejs) for QR Codes.

These is also standalone version where all js libraries are embedded into single html. This could be more convinient when transferring and using in different devices. It could be used on an old smartphone with no internet access for an example.

