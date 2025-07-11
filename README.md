# Capcoin-blockchain-
---

🧠 CapChain Software Bio

🔗 Overview

CapChain is a blockchain-integrated system that rewards users with cryptocurrency (CAPCOIN) by scanning physical bottle caps. It’s designed to blend real-world interactions with tokenized digital rewards, using technologies like smart contracts, mobile scanning apps, Firebase authentication, and IPFS for decentralized metadata storage.


---

🏗️ System Architecture

CapChain is composed of five main components:

Component	Technology	Purpose

Smart Contract	Solidity on EVM chain	Manages CAPCOIN minting, volatility freeze logic, and scanner permissions
Mobile App	React Native	Captures cap images/QR, handles scanning and wallet interactions
Backend API	Node.js + Express	Validates caps, communicates with smart contract, logs to Firebase and IPFS
Firebase	Firestore + Auth	Stores scanned cap metadata securely and manages scanner access
IPFS	ipfs-http-client	Stores tamper-proof metadata for caps, publicly accessible



---

🧩 Feature Breakdown

1. 🪙 CAPCOIN Token

Type: ERC-20 token

Reward Model: Pennyblock-style (e.g. 1 ETH = 1,000,000 CAPCOIN)

Scan Reward: 1000 CAPCOIN per unique cap (double for rare caps)

Volatility Protection:

7% Dip = Sell Freeze

14% Recovery = Sell Re-enabled



2. 📲 Mobile App (React Native)

Uses camera to scan QR codes or text from bottle caps

Connects user’s crypto wallet (e.g. MetaMask Mobile)

Sends scanned cap ID to backend API

Shows balance and cap history


3. 🖥️ Backend Server (Node.js/Express)

Validates if a cap was already scanned

Uploads metadata to IPFS

Writes cap info to Firebase Firestore

Calls mintFromCap(capID, userAddress) on the smart contract

Manages volatility logic via price oracle or admin feed


4. 🔒 Firebase Integration

Stores capID, scan timestamp, user wallet, scanner ID

Authenticates scanner apps or devices

Prevents abuse (duplicate caps or unauthorized scanners)

Firebase Rules enforce read/write security


5. 🌐 IPFS Logging

Metadata (cap ID, brand, timestamp, scanner) stored on IPFS

Returns a CID (content hash) stored in Firebase

Makes cap metadata publicly accessible, immutable, and trustless



---

🔄 Cap Scan Flow

1. User scans bottle cap → generates unique capID


2. Mobile app sends:

POST /scan-cap
{
   capID: "ABC123XYZ",
   userAddress: "0xUser...",
   scannerToken: "auth-token"
}


3. Backend:

Checks capID in Firebase

Logs metadata to IPFS

Stores CID in Firebase

Calls mintFromCap(capID, userAddress) on the smart contract



4. User receives CAPCOIN




---

🛡️ Volatility Lock Logic (in Smart Contract)

If token price drops 7% from last stable price → Selling is frozen

Must recover by 14% from dip level before users can sell again

Protects against pump-and-dump or flash crashes

Applies globally or can be adjusted to user-specific rules in future versions



---

🔧 Developer Notes

Contract written in Solidity 0.8.20

Uses OpenZeppelin ERC20 + Ownable

Intended for deployment on Base, Ethereum, or custom chain like PennyBlock

IPFS uses public gateway or self-hosted node

Backend modularized into capRouter.js, ipfs.js, and firebase.js



---

🔮 Future Add-ons

Cap rarity scoring (mint rare NFT for limited edition caps)

Geo-location logging (track cap origins)

Recycling reward bonus (scan at certified drop-off point = higher reward)

Marketplace integration (sell/trade rare caps or CAPCOIN)



---

🚀 Deployment Stack

Layer	Stack Used

Contract	Solidity + Hardhat
Backend	Node.js + Express + ethers.js
Mobile App	React Native + Expo or CLI
Firebase	Firestore, Auth, Hosting (optional)
Storage	IPFS via ipfs-http-client



---
