# Decentralized Auction Application on Ethereum

This project aims to implement basic functionalities of an auction platform using Ethereum.

## Team Members
1. Brijesh Prajapati - Email: 
2. Kayla Nguyen - Email: knguyen1170@csu.fullerton.edu
3. Afolabi Olabode - Email: 
4. Zhiwei Su - Email:

## Link to Original Project
https://github.com/ethereumbook/ethereumbook/blob/develop/12dapps.asciidoc
https://github.com/ethereumbook/ethereumbook/tree/develop/code/auction_dapp

## Requirements

![Auction Diagram](auction_diagram.png)

The application should be decentralized and utilize Ethereum's stack:

1. Smart contracts for business logic(auctions, bids, refund and transfer of ownership)
2. Swarm for data storage(image and metadata)
3. Whisper for a peer-to-peer messaging(chatrooms)

### Deed Repository
Manage non-fungible tokens by implementing an asset/token/deed repository which holds unique asset/token/deed.

#### ERC: Non-fungible Token Standard #721 (NFT)
See following link: 
https://github.com/ethereum/eips/issues/721

### Auction Repository

Auction repository MUST act as an auction house which does the following:

- Holds asset/token/deed that is to be auctioned(ERC721 Ownership by smart contract)
- Allows users bid on auctions
- Keeps track of auctions/bids/ownership
- Transfers ownership of asset/token/deed to winder
- Transfers Funds to auction creator if auction is ended and there is at least one winner
- Cancels auction and deal with refunds
- UI to interact with the above functionality

### Front-end: Vuejs2.x + Vuetify

The front-end is developed using a reactive UI framework with integration of Vuetify, a Google's Material Design implementation.

## Implementation/Data flow

#### 1. Register an ERC721 Non-Fungible Token with the AuctionDaap Deed Repository

The idea of a Deed Repository is used across this project to hold any NFT with metadata attached to. A token/deed is registered by giving a unique ID and attaching metadata(TokenURI). The metadata is what makes each token important or valuable.

#### 2. Transfer Ownership of the NFT to AuctionRepository(Auction house)

The Auction house needs to verify that a NFT is owned by the auction creator, therefore before the auction is created, the owner should transfer the ownership of the NFT to the AuctionRepository smart contract address.

#### 3. Create Auction for NFT

Creating the auction is a simple process of entering auction details such as name, starting price, expiry date etc. The important part is to have the reference between the deed and the auction.

#### 4. Bid on Auction

Anyone can bid on an auction except the owner of the auction. Biding means that previous bidders are refunded and new bid is placed. Bid requirements are as follow:
1. Auction not expired
2. Bidder is not auction owner
3. Bid amount is greator than current bid or starting price(if no bid)

#### 5. Refunds

If an auction is canceled, the Auction Repository MUST return the ownership of the asset/token/deed back to the auction creator and refund bidders if any.

#### 6. Bidder Win Auction

If there is an auction winner, the asset/token/deed is transferred to the bidder and the bid amount is sent to the auction creator.


## How to Run Project: 
1. Clone project into preferred development environment
2. cd into backend folder and deploy contracts to Ganache local network
3. Run:
    - $ truffle init (creates necessary folders)
    - $ truffle compile (compiles contracts)
    - $ truffle migrate (compile smart contracts & uses migration.js to deploy contracts)
** Before deploying contracts, make sure to edit truffle-config.js to deploy to correct local network and don't forget to link project to Ganache.
4. Install web3. This is for connecting the contract.
    $ npm install -s web3@1.0.0-beta.37
5. $ cd frontend
6. $ npm install (install packages needed in the web app)
7. $ npm run dev (to run the app)
8. Web app should now render on http://localhost:8080/

