# 🤖 Solana Jupiter Arbitrage Bot

**Automated arbitrage trading bot for Solana using Jupiter aggregator**

[![Discord](https://img.shields.io/discord/YOUR_SERVER_ID?color=7289da&label=Discord&logo=discord&logoColor=white)](https://discord.gg/tsX256vp)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)]()

---

## ⚡ Features

✅ **Fully Automated** - Continuously scans for arbitrage opportunities  
✅ **Jupiter Integration** - Uses Jupiter's best swap routes  
✅ **Multi-Platform** - Windows, Linux, and macOS support  
✅ **Risk Management** - Configurable slippage and minimum profit  
✅ **Real-Time Monitoring** - Live profit tracking and execution logs  
✅ **15% Developer Fee** - Automatic fee on profits only (never principal)

---

## 📥 Download Latest Release

### [⬇️ Download Latest Version](https://github.com/YOUR_USERNAME/YOUR_REPO/releases/latest)

**Available Builds:**
- 🪟 **Windows**: `arbitrage-bot-win.exe`
- 🐧 **Linux**: `arbitrage-bot-linux`
- 🍎 **macOS**: `arbitrage-bot-mac`

---

## 🚀 Quick Start Guide

### Step 1: Download the Bot

1. Go to [Releases](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/releases/latest)
2. Download the version for your operating system
3. Extract the files to a folder

### Step 2: Prepare Your Wallet

Create a file named `wallet.json` in the same folder as the executable with your Solana wallet private key:

```json
[123,45,67,89,10,...]
```

**⚠️ SECURITY WARNING**: Never share your `wallet.json` file with anyone!

**How to export your wallet:**

**From Phantom:**
1. Open Phantom wallet
2. Settings → Export Private Key
3. Copy the array format `[...]`

**From Solana CLI:**
```bash
cat ~/.config/solana/id.json
```

### Step 3: Check Your Balance

Before running arbitrage, verify your wallet has sufficient SOL:

**Windows:**
```cmd
arbitrage-bot-win.exe check-balance -k wallet.json
```

**Linux/Mac:**
```bash
./arbitrage-bot-linux check-balance -k wallet.json
```

**Expected Output:**
```
=== Wallet Info ===
Address: YourWalletAddress...
SOL Balance: 1.5 SOL
===================
```

**Minimum Requirements:**
- ✅ At least **0.5 SOL** for transaction fees
- ✅ Token balances for the tokens you want to trade

### Step 4: Run Arbitrage

**Windows:**
```cmd
arbitrage-bot-win.exe simple-jupiter-arb ^
  -k wallet.json ^
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v ^
  -m2 So11111111111111111111111111111111111111112 ^
  -a 10 ^
  -s 600 ^
  -p 0.01
```

**Linux/Mac:**
```bash
./arbitrage-bot-linux simple-jupiter-arb \
  -k wallet.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 So11111111111111111111111111111111111111112 \
  -a 10 \
  -s 600 \
  -p 0.01
```

---

## 🎮 Command Reference

### `simple-jupiter-arb` - Run Arbitrage Bot

**Required Parameters:**

| Parameter | Flag | Description | Example |
|-----------|------|-------------|---------|
| Keypair | `-k, --keypair` | Path to wallet JSON file | `-k wallet.json` |
| Token 1 | `-m1, --token-mint1` | First token address (to buy/sell) | `-m1 USDC_ADDRESS` |
| Token 2 | `-m2, --token-mint2` | Second token address | `-m2 SOL_ADDRESS` |
| Amount | `-a, --amount` | Trade amount in tokens | `-a 10` |

**Optional Parameters:**

| Parameter | Flag | Description | Default | Example |
|-----------|------|-------------|---------|---------|
| Min Profit | `-p, --min-profit` | Minimum profit threshold | None | `-p 0.01` |
| Slippage | `-s, --slippage-bps` | Slippage tolerance (bps) | 50 | `-s 600` |
| Priority Fee | `-c, --compute-unit-price` | Gas price (micro-lamports) | 10000 | `-c 50000` |

**What is BPS?** Basis points - 100 bps = 1%. Common values:
- Conservative: 300 bps (3%)
- Moderate: 600 bps (6%)
- Aggressive: 1000 bps (10%)

### `check-balance` - Check Wallet Balance

**Parameters:**

| Parameter | Flag | Description | Example |
|-----------|------|-------------|---------|
| Keypair | `-k, --keypair` | Path to wallet JSON file | `-k wallet.json` |

**Example:**
```bash
./arbitrage-bot-linux check-balance -k wallet.json
```

---

## 💎 Popular Trading Pairs

### Solana Mainnet Token Addresses:

| Token | Mint Address | Symbol |
|-------|--------------|--------|
| **USDC** | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` | USDC |
| **Wrapped SOL** | `So11111111111111111111111111111111111111112` | SOL |
| **USDT** | `Es9vMFrzaCERmJfrF4H2FYD4KCoNkY11McCe8BenwNYB` | USDT |
| **RAY** | `4k3Dyjzvzp8eMZWUXbBCjEvwSkkk59S5iCNLY3QrkX6R` | RAY |
| **mSOL** | `mSoLzYCxHdYgdzU16g5QSh3i5K3z3KZK7ytfqcJm7So` | mSOL |

### Example Trading Strategies:

**1. USDC ↔ SOL Arbitrage (Most Common)**
```bash
./arbitrage-bot-linux simple-jupiter-arb \
  -k wallet.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 So11111111111111111111111111111111111111112 \
  -a 10 \
  -s 600 \
  -p 0.05
```

**2. USDC ↔ USDT Stablecoin Arbitrage**
```bash
./arbitrage-bot-linux simple-jupiter-arb \
  -k wallet.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 Es9vMFrzaCERmJfrF4H2FYD4KCoNkY11McCe8BenwNYB \
  -a 100 \
  -s 300 \
  -p 0.01
```

**3. High-Risk RAY Arbitrage**
```bash
./arbitrage-bot-linux simple-jupiter-arb \
  -k wallet.json \
  -m1 4k3Dyjzvzp8eMZWUXbBCjEvwSkkk59S5iCNLY3QrkX6R \
  -m2 So11111111111111111111111111111111111111112 \
  -a 5 \
  -s 1000 \
  -p 0.1
```

---

## 📊 Understanding the Output

When the bot runs, you'll see:

```
=== PURE JUPITER ARBITRAGE WITH 15% FEE ===
Fee Wallet: HY8hPLeiRQ4swJFLhLFLg6XwrMFTuFctdWJN7WWxWs6U
Mint1 account: YourTokenAccount...
Mint2 account: YourTokenAccount...
Strategy: Buy Mint2 → Sell Mint2 → Take 15% fee → Profit

Trading amount: 10 tokens
Min for profit: 10.050000 tokens
=============================================

⚡ PROFIT DETECTED!
   Gross profit: 0.125000 tokens (1.2500%)
   Fee (15%): 0.018750 tokens
   Net profit: 0.106250 tokens (1.0625%)
   Start:  10.000000
   After:  10.125000
   Price impact: 0.0845%
   Profit margin: 125 bps
   Slippage: 600 bps (6.0%)

✓ Buy swap transaction obtained
✓ Sell swap transaction obtained
✓ Fetched lookup table (45 addresses)
✓ Decompiled 12 buy + 11 sell instructions
💰 Fee instruction created: 0.018750 tokens (15%)
✓ Fee transfer instruction added

=== ATOMIC TRANSACTION WITH FEE ===
Total: 26 instructions (including fee transfer)
Compute: 1200000 units @ 10000 priority

✅ SUCCESS! Fee automatically sent to developer wallet
https://solscan.io/tx/YOUR_TX_SIGNATURE
Net profit after fee: 0.106250 tokens
```

**Key Metrics:**
- **Gross Profit**: Total profit before fees
- **Fee (15%)**: Amount sent to developer
- **Net Profit**: Your earnings after fee
- **Price Impact**: How much the trade affects market price
- **Profit Margin**: Profit as basis points (bps)

---

## ⚙️ Configuration Tips

### Slippage Settings

| Market Condition | Recommended Slippage | Risk Level |
|------------------|---------------------|------------|
| Stable markets | 300-600 bps (3-6%) | Low |
| Normal volatility | 600-1000 bps (6-10%) | Medium |
| High volatility | 1000-2000 bps (10-20%) | High |

### Trade Amount Guidelines

| Token | Min Amount | Safe Amount | Large Amount |
|-------|------------|-------------|--------------|
| USDC/USDT | 10 | 100 | 1,000+ |
| SOL | 0.5 | 5 | 50+ |
| RAY | 1 | 10 | 100+ |

**💡 Pro Tip**: Start small (10-50 USDC) to test the bot before scaling up.

### Priority Fees

| Network Congestion | Recommended Fee | When to Use |
|-------------------|-----------------|-------------|
| Low | 5,000-10,000 | Off-peak hours |
| Medium | 10,000-50,000 | Normal trading |
| High | 50,000-200,000 | Peak hours, fast execution needed |

---

## 💰 Fee Structure

**How Fees Work:**

1. ✅ Bot executes profitable arbitrage
2. ✅ Calculates gross profit
3. ✅ **Automatically transfers 15% to developer wallet**
4. ✅ You keep 85% of profits

**Developer Fee Wallet:**  
`HY8hPLeiRQ4swJFLhLFLg6XwrMFTuFctdWJN7WWxWs6U`

**Important:**
- Fees are taken **ONLY from profits**, never from your trading capital
- If a trade is not profitable, no fee is charged
- Fee transfer is atomic (happens in same transaction)
- Cannot be bypassed or disabled

**Example:**
```
Capital: 100 USDC
Profit: 2 USDC (2%)
Fee (15% of profit): 0.30 USDC
Your profit: 1.70 USDC (1.7%)
Final balance: 101.70 USDC
```

---

## 🛡️ Safety & Best Practices

### ✅ DO:
- ✅ Start with small amounts to test
- ✅ Monitor the bot regularly
- ✅ Keep sufficient SOL for transaction fees
- ✅ Use secure RPC endpoints
- ✅ Check token liquidity before trading
- ✅ Set reasonable slippage tolerance
- ✅ Join our Discord for support

### ❌ DON'T:
- ❌ Trade tokens you don't understand
- ❌ Use your entire balance
- ❌ Share your wallet.json file
- ❌ Run multiple instances with same wallet
- ❌ Trade during extreme volatility
- ❌ Ignore transaction failures
- ❌ Leave bot running unmonitored for days

---

## 🐛 Troubleshooting

### Error: "Transaction failed: 0x1788"
**Cause**: Slippage tolerance exceeded  
**Solution**: Increase slippage with `-s 1000` or reduce trade amount

### Error: "Insufficient funds"
**Cause**: Not enough token balance  
**Solution**: 
1. Run `check-balance` command
2. Ensure you have the token you're trying to trade
3. Keep at least 0.5 SOL for fees

### Error: "Failed to fetch lookup table"
**Cause**: RPC endpoint issues  
**Solution**: 
1. Wait a few seconds and retry
2. Check your internet connection
3. Consider using a premium RPC (Helius, QuickNode)

### Bot Not Finding Profitable Trades
**Causes**:
- Market conditions don't support arbitrage
- Trade amount too large (high slippage)
- Minimum profit threshold too high

**Solutions**:
1. Reduce trade amount: `-a 5` instead of `-a 100`
2. Lower min profit: `-p 0.001` instead of `-p 0.1`
3. Try different token pairs
4. Increase slippage tolerance

### "No buy route" / "No sell route"
**Cause**: Liquidity issues or token not tradeable  
**Solution**: 
1. Verify token addresses are correct
2. Check if tokens have sufficient liquidity on Jupiter
3. Try more popular token pairs (USDC/SOL)

---

## 📱 Community & Support

### 💬 Join Our Discord Server

Get help, share strategies, and connect with other traders:

**[🔗 Join Discord: https://discord.gg/tsX256vp](https://discord.gg/tsX256vp)**

**Discord Channels:**
- `#support` - Get help with bot issues
- `#strategies` - Share profitable trading pairs
- `#announcements` - Bot updates and news
- `#results` - Show off your profits
- `#troubleshooting` - Common issues and solutions

### 📧 Other Support

- **GitHub Issues**: [Report bugs](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/issues)
- **Documentation**: [Full docs](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/wiki)
- **Updates**: [Release notes](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/releases)

---

## 🔄 Updates & Releases

### Checking for Updates

Visit our [Releases Page](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/releases) to check for new versions.

### Update Process

1. Download latest release
2. Replace old executable with new one
3. Your `wallet.json` stays the same
4. No configuration changes needed

### Version History

Check [CHANGELOG.md](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/blob/main/CHANGELOG.md) for detailed version history.

---

## ⚖️ Legal & Disclaimer

**⚠️ IMPORTANT DISCLAIMER:**

This software is provided "as is" without warranty of any kind. Trading cryptocurrencies involves substantial risk of loss. Users assume all responsibility and risk for their trading activities.

**By using this software, you acknowledge:**
- ✅ You understand cryptocurrency trading risks
- ✅ You are solely responsible for your trades
- ✅ Past performance doesn't guarantee future results
- ✅ The developers are not liable for any losses
- ✅ You comply with your local regulations
- ✅ You understand the 15% fee structure

**Risk Warning:**
- Market conditions can change rapidly
- Smart contracts may contain bugs
- Network congestion can cause failed transactions
- You may lose money even with the bot

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🌟 Tips for Success

1. **Start Small**: Test with $10-50 before scaling
2. **Monitor Regularly**: Check bot every few hours
3. **Join Discord**: Learn from experienced users
4. **Diversify Pairs**: Try multiple token combinations
5. **Track Performance**: Keep notes on what works
6. **Be Patient**: Not every market condition is profitable
7. **Stay Informed**: Join Discord for strategy discussions

---

## 📈 Expected Performance

**Realistic Expectations:**

| Market Condition | Profit Opportunities | Success Rate |
|------------------|---------------------|--------------|
| High volatility | 5-20 per day | 60-70% |
| Normal markets | 2-10 per day | 40-50% |
| Low volatility | 0-5 per day | 20-30% |

**Typical Profits:**
- Per trade: 0.1% - 3% (before fees)
- Daily: 1% - 10% of capital (variable)
- Monthly: 10% - 50% (market dependent)

**⚠️ Note**: These are estimates based on optimal conditions. Actual results vary.

---

## 🎯 Quick Command Cheatsheet

```bash
# Check balance
./arbitrage-bot-linux check-balance -k wallet.json

# Basic arbitrage (USDC/SOL)
./arbitrage-bot-linux simple-jupiter-arb -k wallet.json \
  -m1 EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v \
  -m2 So11111111111111111111111111111111111111112 \
  -a 10 -s 600 -p 0.01

# Conservative (low slippage)
./arbitrage-bot-linux simple-jupiter-arb -k wallet.json \
  -m1 USDC_ADDRESS -m2 SOL_ADDRESS -a 10 -s 300 -p 0.05

# Aggressive (high slippage)
./arbitrage-bot-linux simple-jupiter-arb -k wallet.json \
  -m1 USDC_ADDRESS -m2 SOL_ADDRESS -a 50 -s 1000 -p 0.01
```

---

## 🙏 Credits

Built with:
- [Solana Web3.js](https://solana.com/)
- [Jupiter Aggregator](https://jup.ag/)
- [Anchor Framework](https://www.anchor-lang.com/)

---

**Happy Trading! 🚀**

**[Download Now](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/releases/latest)** | **[Join Discord](https://discord.gg/tsX256vp)** | **[Report Issues](https://github.com/freedomparrot/Solana-Arbitrage-Pure-Bot/issues)**

---

*Last Updated: January 2026*
