# NFT Mint Bot

This project allows users to mint NFTs instantly from contract by inputing their wallet info and mint infos. And the project supports Ethereum, polygon, and other test networks.

The original repo is from [kamsec / nft-minter](https://github.com/kamsec/nft-minter)

## 1. Requirement
- Python 3.8+
- web3.py(install on command line, `pip install web3`)
- Blockchain API prodiver, Infura preferred, and Alchemy etc.

## 2. Installation
1. `Git clone https://github.com/websterhasnoheart/NFT_mint_bot.git`
2. `cd NFT_mint_bot`
3. `python goMint.py - [single] | [multi] | [newacc]`

## 3. How TO USE THIS SHIT?
1. Specify your settings in `settings.json`
```
{
    "CHAIN_NAME": "Ethereum",
    "CONTRACT_ADDRESS": "YOUR CONTRACT ADDRESS",
    "MINT_FUNCTION_NAME": "mint",
    "NUMBER_OF_MINTS": 6,
    "MINT_PRICE": 0.1,
    "EXTRA_MIXING_LAYERS": 0,
    "SEND_BACK": true,
    "LOGGING": true
    "MINT_DATE" : 14:00
}
```
2. Specify your secret keys in `secrets.json`
```
{
    "PRIVATE_KEY": "0x***",
    "PROVIDER": "***"
}
```

3. Run the program in one of the available modes
```
python minter.py -multi
```
The program will display selected settings and corresponding infos

## 4. Configuration
Settings (settings.json):

- CHAIN_NAME - set to one of available chains:
Ethereum, Ropsten, Rinkeby, Kovan, Polygon, Mumbai
If you need to add other chain, you can modify CHAINS dict in settings.py
- CONTRACT_ADDRESS - the address of smart contract deployed on selected chain, with verified source code (available on corresponding blockchain explorer api)
- MINT_FUNCTION_NAME - the exact name of the minting function of smart contract to execute
- NUMBER_OF_MINTS - the number of times for minting function to be executed.
In Multi mode this is also the number of accounts derived, each account will execute mint function once
- MINT_PRICE - the minimum price of single mint in Ether (or MATIC if we are on Polygon/Mumbai blockchain), not including transaction fee
- EXTRA_MIXING_LAYERS - only for -multi option - creates additional sets of addresses to mix coins and hide slightly the origin of funds
- SEND_BACK - only for -multi option - after minting, sends the remaining funds back to the master account
- LOGGING - enables printing transactions and logging in logs/ directory
- MINT_DATE - There is a count down function implemented, input the exact time that the NFT to be minted, the time needs to be converted to your own timezone.

Modes (command-line arguments):

- -h - help page
-newacc - New account mode - generates a new account, displays keys and quits the program
- -single - Single mode - initializes master_account from PRIVATE_KEY specified in secrets.json and calls specified mint function from it multiple (NUMBER_OF_MINTS) times.
- -multi - Multi mode - initializes master_account like in Single mode, by hashing the private key derives another NUMBER_OF_MINTS accounts, sends funds to them and mints once from every derived account