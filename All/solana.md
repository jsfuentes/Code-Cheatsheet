# Solana

Look at https://solscan.io/ for address/tx info

## CLI Tool

Setup command line tool

```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.9.4/install)"
```

Add to path if its not auto

```bash
solana --version
solana config get
```

### Making New CLI Wallet

```bash
solana-keygen new -o /Users/jfuentes/.config/solana/id.json
solana address #JIFJSPIOSJOIPJSDIOJ
```

#### Using in dev

```bash
solana config set --url https://api.devnet.solana.com
solana airdrop 1 <RECIPIENT_ACCOUNT_ADDRESS> --url https://api.devnet.solana.com #use solana address
```

## Making an NFT

Pretty easy actually

Generate layered art with [HashLips](https://github.com/HashLips/hashlips_art_engine)

Git clone the [Metaplex](https://github.com/metaplex-foundation/metaplex) repo and use CandyMachine. Edit the json, follow cli commands, and boom