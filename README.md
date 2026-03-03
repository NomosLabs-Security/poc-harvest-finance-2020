# Harvest Finance — Flash Loan Vault Price Manipulation PoC (2020)

> **Educational Purpose Only** — This PoC is created for security research and education
> purposes only. It is a simplified simulation, not a fork replay against mainnet.

**Category:** Oracle Manipulation
**Loss:** ~$34M
**Chain:** Ethereum
**Date:** October 26, 2020

## Overview
Harvest Finance's fUSDT and fUSDC vaults were exploited for ~$34M through repeated flash loan-powered price manipulation of the Curve y pool. The attacker used flash-borrowed USDT/USDC to manipulate the Curve pool's spot price, then deposited/withdrew from Harvest vaults at manipulated rates, profiting from the price discrepancy.

## How It Works
1. **SimpleVault** uses spot AMM price for deposit/withdrawal valuation
2. **Attacker** flash loans a large amount, manipulates AMM price, deposits at a low price, restores price, and withdraws at a higher price
3. **FixedVault** demonstrates TWAP-based pricing that resists single-block manipulation

## Run
```bash
git clone https://github.com/NomosLabs-Security/poc-harvest-finance-2020
cd poc-harvest-finance-2020
forge install foundry-rs/forge-std --no-git
forge test -vvvv
```

## Key Takeaway
Using spot AMM prices for vault share pricing creates an arbitrage opportunity. Any vault or protocol that values assets based on real-time DEX prices is vulnerable to flash loan manipulation. TWAP oracles, Chainlink price feeds, or deposit/withdrawal slippage checks are essential.

## Disclaimer
Educational purposes only. Simplified simulation of the vulnerability pattern.

## License

MIT — For educational use only.
