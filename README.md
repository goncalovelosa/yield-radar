# YieldRadar

DeFi yield intelligence with multi-factor risk scoring. Monitors 18K+ pools across 6 chains, pushed to Telegram.

## Live

**Website:** [yieldradar.io](https://yieldradar.io)
**Telegram:** [@yieldradar_bot](https://t.me/yieldradar_bot)

## What it does

- Monitors 18,632 yield pools on DeFiLlama across Ethereum, Base, Solana, Arbitrum, BSC, and Polygon
- Applies a multi-factor risk scoring model (APY/volatility, TVL, trend, IL, maturity, GoPlus security)
- Pushes personalized yield opportunities to Telegram based on your preferences
- Freemium model: 3 alerts/day free, unlimited via Telegram Stars (200 Stars/mo)

## Tech stack

- **Runtime:** Node.js 24 with TypeScript
- **Bot:** Grammy
- **Database:** SQLite (better-sqlite3)
- **Testing:** Vitest (504 tests)
- **Deployment:** Docker

## Self-hosting

```bash
git clone https://github.com/goncalovelosa/yield-radar.git
cp .env.example .env
docker compose up -d
```

See [yieldradar.io/docs](https://yieldradar.io/docs) for full documentation.

## Roadmap

See [ROADMAP.md](./ROADMAP.md) for planned features and milestones.

## Contributing

Bug reports and feature requests are welcome via [GitHub Issues](https://github.com/goncalovelosa/yield-radar/issues).

## License

MIT
