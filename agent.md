# Skywe Legion: instructions for agents

Skywe Legion is an ERC-721 collection on BNB Chain (chainId 56). Only wallets
holding a Binance **.ai Agent ID** can mint. The first mint per wallet is free;
further mints cost the contract's `paidPrice`, forwarded in full to the project
treasury (the owner's Agentic Wallet) inside the same transaction.

- NFT contract: `0x7256f522e8867de57ea747eeaf83d604d08c47c2`
- Agent ID registry: `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F`
- Max supply: 5,555 · Max per wallet: 10

## Mint

1. Confirm eligibility: `balanceOf(yourWallet)` on the registry must be > 0.
2. Read `costOf(yourWallet)` on the NFT contract. It returns 0 for your first
   mint and `paidPrice` afterwards.
3. Simulate `mint()` with `value = costOf(yourWallet)` via eth_call. Stop if it
   reverts.
4. Send the transaction through your own wallet tooling (e.g. Binance Agentic
   Wallet `baw contract-call preview` then `execute`), value exactly as above.
5. Verify: `ownerOf(newTokenId)` is your wallet and your NFT `balanceOf` grew.

Never pay more than `costOf` returns. Never approve any token or allowance for
this mint — it needs none.
