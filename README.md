# solana-mev

A flash loan arbitrage bot for Solana using Kamino Finance, Jupiter swaps, and Jito bundles.

## How It Works

1. Borrows tokens instantly via a Kamino Finance flash loan
2. Executes a two-leg swap through Jupiter (token1 → token2 → token1)
3. Repays the flash loan + fee
4. Keeps the profit
5. Submits transactions via Jito block engine for MEV protection
6. A 10% developer fee is taken from profit on each successful arbitrage

All of this happens atomically in a single transaction — if any step fails, the whole transaction reverts and you lose nothing except the transaction fee.

## Requirements

- Linux x86_64
- A Solana wallet keypair JSON file
- A funded wallet (SOL for transaction fees, and a token account for your chosen mint)
- A Jupiter API key (https://portal.jup.ag)
- A fast RPC endpoint (Helius, Triton, QuickNode recommended)

## Setup

**1. Download the binary**

Download `solana-mev` from the releases page and make it executable:

```bash
chmod +x solana-mev
```

**2. Create your config file**

Create a file called `config.toml` in the same folder:

```toml
# Path to your Solana wallet keypair JSON file
keypair = "/home/user/.config/solana/id.json"

# Token pair to arb (these are USDC and wSOL)
token_mint1 = "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v"
token_mint2 = "So11111111111111111111111111111111111111112"

# Flash loan amount in tokens (not lamports)
amount = 1000.0

# Minimum profit required before executing (in tokens)
min_profit = 0.5

# Your Jupiter API key from https://portal.jup.ag
jupiter_api_key = "jup_your_key_here"

# Your RPC endpoint
rpc_url = "https://your-rpc-endpoint.com"

# Jito tip in lamports (higher = more likely to land)
jito_tip_lamports = 10000

# Slippage in basis points (50 = 0.5%, 100 = 1%)
slippage_bps = 50

# Milliseconds to wait between quote checks
sleep_ms = 150
```

**3. Run it**

```bash
./solana-mev run config.toml
```

## Supported Token Pairs

Currently supported as the flash loan token (token_mint1):

| Token | Mint Address |
|-------|-------------|
| USDC  | EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v |
| wSOL  | So11111111111111111111111111111111111111112 |

token_mint2 can be any token Jupiter supports.

## Configuration Reference

| Field | Required | Default | Description |
|-------|----------|---------|-------------|
| keypair | Yes | — | Path to your wallet keypair JSON |
| token_mint1 | Yes | — | Flash loan token mint address |
| token_mint2 | Yes | — | Second token mint address |
| amount | Yes | — | Flash loan size in tokens |
| min_profit | No | 0 | Minimum profit to execute in tokens |
| jupiter_api_key | Yes | — | Jupiter API key |
| rpc_url | Yes | — | Solana RPC endpoint URL |
| jito_tip_lamports | No | 10000 | Jito tip in lamports |
| slippage_bps | No | 50 | Slippage tolerance in basis points |
| sleep_ms | No | 150 | Delay between quote fetches in ms |

## Tips

- Use a private or dedicated RPC endpoint — public RPCs are too slow for arb
- Start with a small `amount` to test before scaling up
- Lower `sleep_ms` means more quote checks per second but more RPC load
- Higher `jito_tip_lamports` increases your chance of landing bundles in competitive slots
- Set `min_profit` above 0 to avoid executing marginal trades that might fail due to slippage

## Fees

- Kamino flash loan fee: 0.001% of borrowed amount
- Jupiter swap fee: included in quote
- Jito tip: configurable via `jito_tip_lamports`
- Developer fee: 10% of profit per successful arbitrage

## Disclaimer

This software is provided as-is with no guarantees. Arbitrage is competitive and profits are not guaranteed. Use at your own risk. Never deposit more than you can afford to lose.
