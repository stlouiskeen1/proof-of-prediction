[README (1).md](https://github.com/user-attachments/files/34912182/README.1.md)
#Proof of Prediction (PoP)

**A Layer 1 blockchain where prediction market bettors are the validators.**

[**Read the whitepaper (PDF)**](whitepaper.pdf) · Status: public draft v1.0 · Built on the Cosmos SDK

---

## The idea

Proof of Work secures a chain with electricity. Proof of Stake secures it with locked capital. Neither measures whether a validator is actually *right*.

PoP uses the **bet as the stake** ("bet-as-stake"). A validator's voting power depends on how much they put at risk, how accurately they have forecast, and how much risk they take on:

```
VP(i) = BetSize(i) × AccuracyScore(i) ÷ RiskMultiplier(i)
```

The cheapest way to gain influence is to be a calibrated forecaster who takes reasonable positions, which is the behavior a prediction market wants.

## Key design points

| Area | Design |
|---|---|
| Scoring | Logarithmic scoring rule (floor -2.0), EMA α = 0.1, calibration bonus every 50 predictions |
| Voting power | Frozen per 100-block epoch (~7 min) to keep BFT safe |
| Caps | 5% per validator, 30% per platform (hard-coded) |
| Oracle | Automated feeds, optimistic assertions, and a **Resolution Market** for disputes (no token voting) |
| Consensus | Tendermint-style BFT, 4s blocks, committee of 50-200 |
| Mempool | Encrypted (TPKE, BLS12-381) to reduce front-running |
| Token | 1B POP fixed supply; bonds and 70% of rewards paid in stablecoin |

## Status and roadmap

- [x] Whitepaper v1.0 (public draft)
- [x] Internal design audits, with fixes incorporated
- [ ] Independent audit
- [ ] Next.js demonstrator on real market data
- [ ] Testnet with ~50 genesis validators
- [ ] Platform integrations (Manifold and Augur first, then Kalshi, then Polymarket)

## Open problems

I'd rather list these myself than have them found for me:

1. **Verifying bets on centralized platforms** (e.g. Kalshi) without the platform's cooperation.
2. **The bet isn't slashable on this chain.** Security leans partly on the POP bond.
3. **Regulatory exposure** of the prediction markets this design depends on.
4. **Parameters are untested at scale.** Everything comes from design analysis, not live data.

## Feedback wanted

If you work on consensus, mechanism design, or prediction markets, I want your criticism. Open an [issue](../../issues) with your thoughts, or contact me directly:

**Contact:** YOUR_EMAIL_OR_LINK

## License

The whitepaper is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Disclaimer

This is a technical proposal for discussion. It is not an offer to sell or a solicitation to buy any token or security, and nothing here is financial or legal advice. Specifications may change as the design is reviewed and audited.
