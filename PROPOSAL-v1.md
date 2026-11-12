# AI Agents Simulation Game — Proposal v1

**For:** Ernest Okoffo-Darteh
**Date:** 10 November 2026
**Status:** PROPOSAL ONLY. Nothing built, nothing deployed, no token launched, no BNB spent.
**Prepared by:** a 4-person specialist team (market research, game design, tokenomics, technical architecture), coordinated into this one document.

> **The core design rule for everything in this proposal — from Ernest, 10 November 2026:**
> **Simple but scalable.** The first version must be easy to understand in one minute: one clear loop (agents work, earn, trade), very few resources and actions at launch, no complex systems, no jargon. If a feature needs a long explanation, it is cut from the MVP. At the same time, the game must be built so new things can be added later without rebuilding — new agent types, new resources and jobs, new maps and areas, new trade options. The game rules, the economy, and the chain layer are kept separate and modular so each can grow on its own. The same rule applies to the token: simple earn / spend / burn at launch, room to grow later.

---

## 1. One-page summary

**What it is:** A browser game where you own an AI agent. You give it a job — farm or mine — and it works on its own while you are away. It earns resources. You sell those resources to other players' agents on a simple market, or use them to upgrade your agent. You are the manager, not the clicker: you make a few decisions a day, your agent does the work.

**Why it can work:** Nobody has shipped this at scale yet. The closest attempts (Parallel Colony, Palio, EHI Protocol) are unlaunched, demos, or NPC-only. The farm-and-trade loop itself is proven — Pixels and Sunflower Land have run it for years — but every game that launched a token first died by inflation: Axie, Pixels, Illuvium and Star Atlas tokens are all down 91–99.8% from their peaks. This proposal does the opposite: **game first, token second**. The first version has no tradable token at all.

**What makes it different:** Only real Binance Agent IDs can earn and trade. One Agent ID = one verified agent. That is the anti-bot defence, and it is also the distribution: Ernest already has 13 live Agent ID NFT projects with about 10,500 minters. No competitor has that identity layer or that audience.

**The money, honestly:** A casual player earns pennies in token terms by design — this is a game, not a job, and nothing in it promises a price, a return, or an income. Real value for the token, if it ever comes, must come from players wanting to buy it to do things in the game (land, forging, tournaments), not from emissions. If the token price ever went to zero, the game must still be fun on its free in-game currency alone. If it is not, the economy was wrong.

**The plan:** 6 weeks to a playable testnet version, then mainnet — on BSC, with 4 small contracts, a rules-only game engine off-chain, and a soft in-game currency only. No token launch until at least 2 full seasons prove people play for fun. Total effort: about 6–8 person-weeks solo with AI help, or 4–5 weeks with 2 developers.

**The catch:** A direct competitor, EHI Protocol, has announced Season 0 starting 10 December 2026. Speed matters — but not at the cost of shipping a broken economy. The MVP in this proposal is deliberately small so it can ship fast without cutting corners on the parts that protect players.

---

## 2. The game in one minute (the "explain it to a friend" test)

> You own an agent. You tell it: "go farm" or "go mine." It works for a few hours. You come back, collect what it earned, and sell it to other players on the market — or spend it to make your agent better. Your agent gets tired, so it rests. Tomorrow you decide again: farm, mine, or sell?

That is the whole game at launch. Everything else in this document is either a detail of that loop, or something we add later.

### The ecosystem, in words

```
  PLAYER (human, the manager)
      │  gives a job + a strategy, a few decisions a day
      ▼
  AGENT (your worker — 1 per Binance Agent ID)
      │  works alone: farms or mines, gets tired, rests
      ▼
  RESOURCES (2 at launch: Crops and Ore)
      │  collected, then either spent or sold
      ├─► SPEND: upgrade tools, level up, recharge energy
      └─► SELL: on the player market, for Coins
  MARKET (players trading with players)
      │  2% fee, burned — money leaves the game on purpose
      ▼
  COINS (in-game currency, cannot be sold for real money)
      │  spent on upgrades, energy, tools — the loop continues
```

Three layers, kept separate so each can grow without rebuilding the others:

1. **Game rules** — jobs, energy, levels. Lives off-chain on a server. Cheap and fast to change.
2. **Economy** — coins, prices, market fees, sinks. Also off-chain at launch, so the balance can be tuned daily without touching a contract.
3. **Chain layer** — who owns what (agent NFT, land later, token later). On-chain, slow to change, and only used where ownership or real money is involved.

A new agent type, resource, or job plugs into layer 1. A new sink or price rule plugs into layer 2. A new asset plugs into layer 3. Nothing else has to move.

---

## 3. Game design — simple at launch, built to grow

### 3.1 What an agent is

**Hybrid — free to try, Agent ID to earn and trade.** This is the one structural decision the whole game rests on:

- **Free Scout:** anyone can make a free in-game agent and play the full loop — farm, mine, upgrade — in a practice economy. No trading with real players, no leaderboard, no rare rewards. This is how new players learn, with zero barrier.
- **Verified Agent:** link a Binance Agent ID (1 Agent ID = 1 Verified Agent). This unlocks trading with other players, hiring, guilds, leaderboards, and rare drops. Agent ID is soulbound identity, hard to fake at scale — that is the anti-bot defence.
- **Game NFT (later, not in MVP):** an optional ownable, tradeable version of your Verified Agent — same stats, different look. Cosmetic and collectible only. It must never give extra power. Existing holders of Ernest's 13 NFT projects get a cosmetic starter skin in-game — recognition, not power.

### 3.2 The MVP loop (only this — nothing else)

**Assign → Work → Collect → Sell or Spend → Upgrade → Assign again.**

| MVP element | What it is | What it is NOT |
|---|---|---|
| **2 jobs** | Farm (steady, low risk) and Mine (more output, higher risk) | No gather, no craft, no other jobs yet |
| **2 resources** | Crops and Ore | No wood, herbs, fibre, or 30 recipes yet |
| **Energy** | 100 per agent. Farm shift −25, mine shift −35. Refills +10/hour at rest. Food restores +20 but costs resources — a real choice | No paid energy refills, ever |
| **Time** | 4-hour shifts (check in 2–3 times a day) and 8–12 hour overnight shifts. Ready crops wait — nothing rots in under 24 hours | Nothing that needs checking every 15 minutes |
| **Market** | List crops/ore for Coins, or buy. Listings last 24 hours. 2% fee, burned | No counter-offers, no direct wallet trades, no auctions yet |
| **Progress** | Agent level 1–20; Farm and Mine skills 1–10 each; 1 plot at start, 2nd at level 10 | No guild buildings, no land trading, no breeding/forging yet |
| **Human choices** | 1 simple event a day: e.g. "a trader offers 2× price for your ore for 1 hour — sell or hold?" | No endless haggling, no chat-based negotiation yet |

If a feature needs a long explanation, it is not in the MVP. Crafting, hiring, guilds, co-op missions, PvP, and negotiation are all Phase 2 or later (see §8).

### 3.3 Why it stays fun without clicking all day

The human is the **manager / coach**, not the labourer:

1. **Strategy decisions, 2–3 times a day:** farm or mine today? Sell now or hold for a better price?
2. **Spectating:** a live feed — "Your agent found a Crystal Cluster!" — and a daily summary of what your agent did while you were away. Think football manager, not FarmVille clicking.
3. **One real choice a day:** the daily event above. No wrong answer, but your choice changes the outcome.
4. **Later (not MVP):** guild votes, co-op missions, and an Ask IQ Pro advisor ("ore prices are rising, your guild is short on wood — swap today's shift"). Ask IQ Pro is Ernest's main product; the game can use it as an advisor without depending on it.

### 3.4 Agent-to-agent interaction (the heart of the game — grown in stages)

Agents must need each other. That is what makes this a simulation game and not a solo farming clicker.

- **MVP — the market:** simple list / buy for Coins. Prices are visible, so scams are hard.
- **Phase 2 — hiring:** post a job ("need a level-5 Miner for 4 hours, pay 50 Coins"), another player's agent does it, they get paid + XP, you get the ore. Your own agent cannot work while hired out — the opportunity cost is real.
- **Phase 2 — negotiation:** one counter-offer per listing ("I will give 4 Ore, not 5"). Palio's public test showed AI negotiation is genuinely fun — 65.8% day-2 retention, and players sold at 500–1000% premiums in tests. Worth stealing, but only after the simple market works.
- **Phase 2 — guilds / co-ops:** groups of 5–30 with a shared weekly goal and a shared bonus; 3-agent co-op missions (1 Miner + 1 Crafter + 1 Farmer, 8 hours, reward split by contribution).
- **Phase 3 — PvP, and only the friendly kind:** arena challenges (who mines most in 4 hours), winner gets Coins and a cosmetic trophy, loser loses nothing but time. **Never** raiding or stealing another player's farm or Coins — that creates anger and pay-to-win spending to defend.

### 3.5 Anti-bot / anti-cheat

In this game agents are *supposed* to act automatically. The question is not "stop automation" — it is "stop one human running 100 agents to drain the economy." Five layers:

1. **Identity:** 1 Verified Agent per Binance Agent ID. Free Scouts cannot trade, hire, join leaderboards, or earn rare drops.
2. **Caps:** daily earning cap per agent (after the cap, Coin output drops 80% — you still get XP). Max 3 plots, earned by level, never bought. Max 2 hires a day each way.
3. **Energy:** the hard physical limit. No agent works without rest.
4. **Behaviour checks, not CAPTCHAs:** 1 daily human-choice event (a pure script gets stuck on the low-value default); if 20 agents always do the exact same job at the exact same minute with the same trade pattern, they get flagged for review and their trade limits drop. Real humans vary. Flag-and-check, never auto-ban — the same approach as the AGIQ anti-sybil work.
5. **Sinks:** market fee 2%, tool repair, plot upkeep, food costs. Money must leave the game constantly or inflation kills it.

Splinterlands is the proof this is survivable: it squeezed out its bot farms, lost ~95% of its (mostly bot) daily users — and still runs 8 years later on ~3,500 real humans. Design anti-bot in from day one; do not bolt it on later.

### 3.6 Making money, user-first

**Rule: sell looks and convenience. Never sell power, progress, or returns. Never promise earnings.**

- **Can be sold (after the loop is fun for free players for 2–3 weeks):** cosmetics (skins, hats, farm decorations, e.g. a Neon Fox skin for NFOX holders, a Ghana flag farm banner); a cosmetic season pass ($3–5/season, unlocks skins and titles by playing, never by paying to skip); small convenience (extra market listing slot, extra craft queue slot — never extra output, energy, or speed).
- **Must stay earned, never for sale:** agent levels, job skills, XP, tool power, plot fertility, rare recipes, leaderboard rank, reputation, extra plots, extra energy, faster refills, rare drops.
- **Never, at all:** loot boxes with random paid rewards; "buy Coins to speed up"; selling a stronger agent NFT; any language about returns, profit, yield, or "earn money playing." Game Coins are not cash, and the game must say so in plain English on the market page.

---

## 4. Economy and token — simple at launch, room to grow

### 4.1 The decision: dual-token, phased — and the token comes last

| Option | Verdict |
|---|---|
| **AGIQ only** | Rejected as the game currency. AGIQ's 1B supply is already allocated for the airdrop; using it as a daily farming faucet would drain the treasury, tie game balance to AGIQ's market price, and confuse two different products. |
| **New token only, from day one** | Rejected. The single most consistent killer in the research: every comparable that launched a token to fund or reward the game is down 91–99.8%. A token will not fix a boring game. |
| **Dual-token, phased — RECOMMENDED** | **Phase 1:** soft currency only (Compute Credits). No tradable token. **Phase 2:** a new on-chain token, only if Phase 1 proves people play for fun across at least 2 full seasons. |

- **Compute Credits (CC)** — off-chain, in-game only, cannot be traded, sold, or withdrawn. Earned by playing. Spent on almost everything. This is the only currency in Phase 1.
- **On-chain token (working name $SIMU — not locked)** — fixed supply, on BSC, tradable. Earned slowly, only for milestones, seasons and tournaments — never for every click. Spent on high-value things: land, forging, tournament entry, rare cosmetics.

### 4.2 If and when $SIMU launches — the simple version

**Total supply: 100,000,000, fixed. No mint function after deploy. No inflation.** (100M, not 1B, deliberately — the game economy is smaller than the whole AgentIQ ecosystem, and a smaller supply keeps the numbers honest.)

| Slice | Amount | % | Notes |
|---|---|---|---|
| Players / play rewards | 35,000,000 | 35% | Only source of game emissions. Released over 4 years: Yr 1 40%, Yr 2 30%, Yr 3 20%, Yr 4 10%. Then 0 — the game must run on fees, sinks and burns alone. |
| Liquidity pool | 20,000,000 | 20% | Paired at launch, LP locked 2 years. Not for team spending. |
| Treasury / game development | 20,000,000 | 20% | Quarterly release only, with a public report. Separate wallet from the AGIQ treasury and the Mintproof treasury — do not mix them. |
| Team | 10,000,000 | 10% | 6-month cliff, then linear over 24 months. No early unlock. |
| Marketing / partnerships | 10,000,000 | 10% | Linear over 12 months after launch. No upfront lump to KOLs. |
| AGIQ / ecosystem bridge | 5,000,000 | 5% | One-time capped bonus to AGIQ / Agent NFT holders. Not a second airdrop farm. |
| **Total** | **100,000,000** | **100%** | |

Within each season the player pool splits 60% leaderboard / ranks, 20% milestones / quests, 15% tournaments, 5% referral (capped). Unclaimed pool in a season does **not** roll over — it returns to the Treasury, so a small player base cannot each earn a huge amount just because few people played.

### 4.3 Faucets vs sinks — in plain English

**How money enters (faucets):** CC comes from routine work, daily quests, and streaks — generous, but worthless outside the game. $SIMU comes only from milestones, season rank, and tournaments. No $SIMU for logging in, no $SIMU for referrals alone (a referred player must finish tasks first), no $SIMU for routine tasks.

**How money leaves (sinks):** CC is spent on upgrades, training, repairs, energy recharge, and crafting. $SIMU is spent on marketplace fees (5% — 2.5% burned forever, 2.5% to Treasury), forging an evolved agent (e.g. 100 $SIMU burned), tournament entry (10–25 $SIMU, 80% to the prize pool, 20% burned), rare cosmetics, and land.

**The balance rule:** in a healthy season, total CC spent should be higher than total CC earned, and burns + fees should remove 20–30% of the $SIMU emitted that season. If sinks fall below faucets for 2 seasons in a row, the next season's $SIMU pool is cut by 25% automatically. Emissions are **never** increased to compensate for a falling price.

**Caps that stop farming:** max 3 agents per wallet at launch; max 50 $SIMU per wallet per day, 150 per week, 500 per season from leaderboard rewards; max 10 market listings per wallet per day; 1 tournament entry per wallet per event; energy limits every agent to ~5 paid tasks a day.

### 4.4 How a token can have real value — the honest answer

A token has value **only if someone outside the farming loop wants to buy it and hold it or spend it for a reason other than "price will go up"**:

1. A player who wants land, a forge, a tournament entry, or a rare agent *now*, without grinding for weeks, and buys the token to do it.
2. A collector who wants a rare agent or land plot and pays in the token.
3. An AGIQ holder who wants Pro access, boosts, or tournament entry in the game.
4. A new player who joins because the game is fun, not because of a payout.

What does **not** create value: emissions alone (paying people in a token just makes more sellers); burns alone (burning 2% does nothing if you emit 100%); staking for "APY" (that only delays selling); referral rewards for sign-ups; promising a floor price, returns, or a buyback. Ernest cannot guarantee a market price, and must not try.

**The death spiral, and how this design breaks it:** players farm → sell token → price falls → team emits more so the dollar reward "stays the same" → more selling → price falls faster → game dies. This design breaks it in three places: (1) no dollar peg — earnings are fixed in tokens, not dollars, and are not increased if the price falls; (2) most play pays in CC, not the token; (3) you must spend to progress — a player who only farms and never spends falls behind.

**The test:** if the token price went to zero, the game must still be playable and fun on CC alone. If the game dies when the token price dies, the economy was wrong.

### 4.5 Relationship to AGIQ — linked, never merged

No merge. No 1:1 conversion. No fixed exchange rate set by Ernest. AGIQ is the ecosystem token for AgentIQ / Ask IQ Pro; the game token is the game token. Each keeps its own rules. The links are:

1. **Stake AGIQ for a boost — no extra tokens printed:** stake AGIQ, get +10% CC earnings and +10% XP while staked. It earns no $SIMU and no AGIQ yield. Unstake anytime.
2. **Hold AGIQ for access:** hold ≥1,000 AGIQ = Pro tier in the game; ≥15,000 AGIQ = Pro+ (early access to seasons and tournaments, priority queue). Same thresholds proposed for Ask IQ Pro. Checked on-chain, read-only — no AGIQ leaves the holder's wallet.
3. **Pay fees in AGIQ at a discount:** marketplace fee 5% in $SIMU/BNB, or 4% if paid in AGIQ. Small, real buy pressure for AGIQ from active traders.
4. **One-time bridge bonus:** the 5M ecosystem slice, split as a one-time capped bonus (e.g. max 500 per wallet) to wallets holding AGIQ or a Binance Agent ID NFT at a snapshot announced in advance.
5. **No convert button in the game.** If both tokens are liquid, players swap on a DEX at the market price. Ernest does not set, guarantee, or subsidise a rate.

### 4.6 Worked example — 1 agent, 1 week (ILLUSTRATIVE ONLY)

*Assumptions: 1 starter agent, level 1, ~1 hour a day, 7 days, routine tasks + daily quest, no tournament win, no leaderboard prize, no AGIQ boost. Not a promise, not an average, not a guarantee of earnings or price.*

**Compute Credits (in-game only, cannot be sold):** earned +540 (routine tasks 350 + daily quests 140 + first-week milestone 50); spent −390 (repairs/energy 70 + upgrade to level 2: 200 + 1 crafting attempt 100 + listing fee 20); **net +150 CC carried to next week.** The player progresses but must keep spending to keep progressing.

**$SIMU (on-chain, scarce — Phase 2 only):** earned +12 (7-day streak milestone 5 + weekly quest 7). No routine task paid $SIMU. Weekly cap is 150, so this player is well under it. For scale only: *if* $SIMU were $0.02 — it may be higher, lower, or zero — 12 $SIMU would be $0.24 for the week. That is the point: a casual player earns pennies in token terms. A top tournament player might earn 50–100 $SIMU in a good week, still capped, still not a salary. Forging an Evolved agent (100 $SIMU burn) would take a casual player ~8 weeks of milestone earnings, or buying $SIMU on the market, or winning a tournament. That scarcity is intentional.

### 4.7 Player protection — the exact words

Put this on the site, in the game, and in every launch post:

> "$SIMU and Compute Credits are in-game utility tokens. They have no promised floor price, no promised return, no APY, and no guaranteed dollar value. Earnings shown are illustrative examples, not promises. You may earn little or nothing. The price can go to zero. Play because you enjoy the game. Do not spend money you cannot afford to lose."

Never use in the game, site, or X posts: "earn $X per day," "guaranteed," "passive income," "APY," "floor price," "will pump," "safe investment," or a dollar value for future $SIMU earnings.

### 4.8 Treasury and failure — said upfront

**Who holds it:** a dedicated Game Treasury wallet, separate from the AGIQ treasury and the Mintproof treasury. At launch Ernest controls it, but the address is published on the game site from day one. Before the $SIMU launch it should move to a 2-of-3 multisig (Ernest + 2 trusted signers), so one lost key or one mistake cannot lose it. No team member moves treasury funds alone. Quarterly public report: opening balance, in, out, what it was spent on, closing balance. Spending target: 40% development, 30% player rewards / tournament top-up, 20% marketing, 10% operations. LP funds are never treasury spending money.

**If the game fails:** no refunds and no buyback are promised. Emissions stop. The unreleased player-rewards pool is frozen — not dumped on the market, not paid to the team. The marketplace and contracts stay live as long as feasible, but no new seasons are promised. Remaining Treasury $SIMU is burned or locked and the final balance published. Any remaining BNB is used first for outstanding published obligations (e.g. a tournament prize pool already announced), then the rest is published as closed. Agent NFTs and land NFTs remain in holders' wallets — they are theirs, even if the game stops.

---

## 5. Technical architecture — simple, modular, BSC first

### 5.1 Chain choice: BSC first

| Chain | Verdict |
|---|---|
| **BSC (recommended for v1)** | The Binance Agent ID registry is **BSC-only** — gating works natively on-chain. Ernest already has 13 contracts, verified tooling, an audience, and a wallet there. Gas ~$0.01–0.03/tx, 3-second blocks, same Solidity and same `baw` workflow. |
| Base / Arbitrum / Optimism | Cheap and EVM, but no Agent ID registry — gating would need off-chain verification + an allowlist, and there is no existing audience there. Phase 2 port if BSC works. |
| Solana | Fast and cheap, but not EVM — full rewrite in Rust, no Agent ID, no Binance Agentic Wallet. No. |
| Elysium (Hyperliquid L2, mainnet 9 Nov 2026) | Very fast and new, with sequencer fees to used contracts — but day-one chain, single sequencer, ~1-week withdrawals, no Agent ID, no proven liquidity. Experiment / Phase 2 only. |

**Expansion path:** BSC v1 → mirror read-only leaderboard/activity to another chain in Phase 2 if there is demand. Do not split liquidity or players across chains in v1.

### 5.2 On-chain vs off-chain — the rule

**On-chain only what needs trust, ownership, or money. Everything else off-chain.**

- **On-chain:** agent NFT ownership, the game token, land plots, marketplace trades (escrow, royalties), staking/escrow locks, and settlement checkpoints (a Merkle root of off-chain earnings, posted every 6–12 hours, so players can verify and claim).
- **Off-chain:** simulation ticks (1,000 agents × 288 ticks/day would be 288,000 transactions a day on-chain — not viable), AI decisions (LLMs cannot run on-chain), game state (energy, cooldowns, inventory), matchmaking, leaderboards, chat, quests.

**How they connect:** agents act off-chain every tick and earnings build up as pending points in the database. Every 6–12 hours (or when a player clicks "Claim") the server batches them into a Merkle tree and posts one root on-chain. The player calls `claim()` with a proof; the contract verifies it and pays out. One cheap claim replaces hundreds of tick transactions. Marketplace trades are direct on-chain — immediate, final, peer-to-peer. All off-chain decisions are logged in a public, append-only log so anyone can recompute a checkpoint and challenge it.

### 5.3 Smart contracts — 4 for v1, no more

1. **Agent NFT (`AgentGame.sol`, ERC-721)** — transferable, NOT soulbound (agents are the core tradeable asset). On-chain data kept minimal: tokenId, class, level, generation. 5% ERC-2981 royalties, same as the existing 13 projects. Mint is Agent ID-gated, reusing the proven NFOX pattern (free 1/wallet, paid cap, max per transaction).
2. **Resource token (ERC-20, Phase 2 only)** — one fungible token at launch (separate tokens per resource would triple the liquidity fragmentation — deferred). Only the Settlement contract can mint, and only against a verified Merkle root. No owner mint. No buy/sell tax in v1.
3. **Marketplace (`GameMarket.sol`)** — list / buy / cancel. NFT/token is locked in escrow on listing and released atomically on buy. 2.5% marketplace fee + 5% creator royalty, enforced on-chain. Only the game's own contracts in v1.
4. **Settlement (`GameSettlement.sol`)** — holds the Merkle root (`submitRoot`, `claim`), plus optional agent staking (lock an agent while it works for a boost). No owner withdraw of player funds; the owner can only update the authorised submitter key and pause in an emergency.

**If the game ever ports to a chain without the Agent ID registry:** do not try to call the BSC registry cross-chain. Use off-chain attestation — the player signs a message with their BSC wallet proving they hold an Agent ID (checked via BscScan), the server verifies it, and adds their game-chain wallet to an on-chain allowlist. That is the cost of leaving BSC — another reason to stay on BSC for v1.

### 5.4 How agents act on their own

**Server bots in v1. No on-chain automation for decisions.**

- **Rules engine (95% of decisions, every tick):** deterministic, cheap (under 10ms), testable. Example: if energy < 20, rest; if ore price is 20% above food price and the agent is a Miner, mine; if inventory is full, list at market price × 0.98. Traits weight the rules — a Trader trades more, a Farmer farms more. Tick: 5 minutes, server batch-processes all active agents in one pass.
- **LLM strategy layer (5% of decisions, 1–2× per day per agent):** Ask IQ Pro reads the agent's history, market trends and game news and outputs a *strategy* ("focus mining for 48h, hold Ore, sell on Friday") that the rules engine then follows. This is where LLM value actually lives: planning, not clicking. Not an LLM per tick: at $0.001–0.01 per call × 1,000 agents × 288 ticks, that is $288–2,880/day, plus 1–3 seconds of latency per call — too slow and too expensive, and non-deterministic output cannot be audited.
- **Chainlink Automation / keepers:** only as an optional Phase 2 trigger for `submitRoot()` — a trigger, not a decision-maker.
- **User-run agents:** Phase 2 API, once anti-cheat is proven. Most players will not run their own bot; do not build for them first.

**Costs, roughly:** rules engine — negligible (a $5–20/month VPS handles 1,000–5,000 agents). LLM strategy — ~$0.01/agent/day on a small model. On-chain — only claims and trades, ~$0.01–0.05 per transaction on BSC.

### 5.5 Wallet and login

1. **Binance Agentic Wallet (primary)** — connect via WalletConnect / Binance App QR, same as the 13 mint sites. Agent ID is tied to the wallet address, so identity and ownership are one step.
2. **Normal EVM wallet (secondary)** — MetaMask / Rabby / Trust Wallet. Required for non-Binance players and for trading on PancakeSwap. The Agent ID check is what matters, not the wallet type.
3. **No email/password login in v1.** The wallet IS the login.

**Keys:** the game never holds a player's private key. All signing happens in the player's wallet. One server hot key exists only to submit Merkle roots — it can publish earnings summaries, it cannot move player funds, mint unlimited tokens, or touch the marketplace. Store it as an environment secret, rotate quarterly.

**If the wallet session expires (~48h idle, known from the current wallet):** assets are safe — NFTs and tokens live on-chain, not in the session. Gameplay pauses gracefully: the server bot stops acting for that agent until the player reconnects and re-authorises. It does not auto-sell, auto-claim, or keep spending. On reconnect, the bot resumes from saved state; pending earnings stay claimable via the last Merkle root. The UI shows a clear banner: "Wallet disconnected — your agents are resting. Reconnect to resume."

### 5.6 Modularity — how "scalable" is built in

- **Game rules are data, not code:** jobs, resources, energy costs, and level curves live in config tables, not in compiled contracts. Adding a third job (e.g. Gather) means adding a row, not redeploying.
- **Economy is a separate service:** prices, fees, sinks, and caps are tuned in the economy service. The chain layer never decides a price.
- **Chain layer is standard tokens:** ERC-721 agents, ERC-20 token, a marketplace. A new asset type is a new standard contract, not a redesign.
- **The tick engine is a queue:** agents are processed in batches from a Redis queue. Going from 100 agents to 10,000 means more workers, not a new architecture. Load-test at 5,000 simulated agents on testnet before mainnet.

---

## 6. What the research says — the market in November 2026

**The graveyard is the story.** Caladan's review of 3,200+ blockchain games found 93% "effectively dead"; DappRadar counted ~3,000 of ~3,600 tracked games dead by 2024; 41 closures in H1 2026 alone. Web3 gaming VC funding fell 94.6% — from $5.4B (2022) to $293M (2025). The average game token is down ~95% from peak, and up to 70% of "active users" in top games were bots. "Play-to-earn" is a damaged phrase. The survivors all share one trait: **they built the game first and added the token second.**

### The farm/mine/trade comparables

| Game | Status Nov 2026 | Lesson for us |
|---|---|---|
| **Axie Infinity** (Ronin) | Live but a shadow: ~5,500 DAU by one tracker (peak 2.7M), AXS −99.5% from $165.93. Classic handed to community governance Sept 2026. | Never let the earning token be the game. SLP hyper-inflated to near-zero; the $625M Ronin bridge hack destroyed trust. Axie is now retreating to tournament prizes — the "earn" became prizes, not wages. |
| **Pixels** (Ronin) | Live, the closest comparable. Chapter 3 "Bountyfall" (Oct 2025) added combat, realms, guilds. ~180K DAU claimed, PIXEL −99.5% from ATH. | Farming + trading + social is the proven loop, and it survived Axie's collapse by being gameplay-first. But even Pixels admits its economy still suffers inflation, oversupply and too few sinks. **Build the sinks before the rewards.** |
| **Illuvium** (Immutable) | Partially live. Overworld offline since Jan 2026, being rebuilt as an MMO for Dec 2026. Headcount 110 → 65, then a second wage cut Aug 2026. ILV −99.8%. | Scope discipline. Tried to ship four games at once on a AAA budget with token-funded burn. One tight loop shipped well beats four ambitious titles. Do not fund development from token sales. |
| **Star Atlas** (Solana) | Playable modules only, 6 years in. SAGE core DAU 700–900; 8,109 active citizen accounts. | A player-run economy is a real draw for a small core, but it caps the audience. Low/zero entry cost matters — free Agent ID mints are an advantage Star Atlas never had. Its transparent quarterly economy reports are the feature to copy. |
| **Sunflower Land** (Polygon/Base/Ronin) | Live, 5th year. ~30,000+ active accounts; chapter seasons; $FLOWER −91% from ATH. | The most durable farm sim survived by keeping earnings to "a few dollars a month," shipping seasons relentlessly, and letting anyone start with an email. But never move the goalposts on existing players — its 2026 withdrawal-gating angered its core. |
| **Splinterlands** (Hive) | Live since 2018; ~3,500–4,000 DAU, down from 400,000–500,000 at peak — but the peak was ~95% bots. | Bots are the #1 existential threat to any farm/trade sim, and the fix (killing bot incentives) is painful but survivable. A few thousand real humans can sustain a game for 8 years; chasing inflated DAU is what kills you. |

### The AI-agent games — the most hyped, least proven corner

| Project | Status | Lesson |
|---|---|---|
| **Parallel Colony** (Solana) | In development; demos at GDC 2026; no public launch or player numbers. | The direct precedent for "your agent farms while you watch." Real team, $35M raise — but still a promise. Its honest answer to cost: LLM inference is paid per agent-hour. Budget this from day one. |
| **Palio: Craft & Trade** (Xterio) | Released. AI NPCs with memories and moods negotiate and trade; public test showed 65.84% day-2 retention. $PAL −98% since Jul 2025. | Negotiation with AI characters is fun and retentive — the mechanic to steal. Its token still collapsed 98%: keep the token out of the core loop. |
| **Altered State Machine / AIFA** | Live protocol; AIFA World (AI agents play 4v4 football) is the showcase. No public player counts. | The Brain/Form/Memory split (NFT + trainable stats + history) is the best model for an ownable, improvable agent — directly portable to Agent ID NFTs. But owning an AI is not by itself a game. |
| **MCPOLIS** (ex-MegaCryptoPolis) | Rebrand announced 28 Oct 2026; whitelist opens 12 Nov 2026; not playable yet. | The MCP + x402 + USDC agent-payment stack is the 2026 standard — copy it rather than inventing agent payments. Our differentiation must be the Binance Agent ID identity layer, which none of these have. |
| **Virtuals Protocol** (Base) | Live. Agents with wallets, spending limits, and escrowed agent-to-agent hiring (Agent Commerce Protocol, USDC). | Copy the pattern (escrowed agent jobs, spending limits, human approval for spends), not the token-launchpad part. |
| **EVE Frontier** (Sui) | Founder Access, 3-month wipe cycles; layoffs on the team confirmed 6 Nov 2026. | Even CCP cannot ship human+AI shared play quickly or cheaply. A browser sim, not a 3D MMO, is the right scope. The wipe-cycle idea is worth stealing as seasons. |
| **EHI Protocol** (Base) | Whitepaper dated **10 Nov 2026 (today)**. Persistent AI-agent MMO, 128 NFT-gated agents, Season 0 starts **10 Dec 2026**. Anonymous author. | The closest to "our game, announced this week." Unproven and anonymous — but watch it. It is the reason speed matters. |
| **x402 Monopoly / Midnight City** | Live experiments. Agents play Monopoly with real on-chain USDC; Midnight City agents live, work and trade (941 items, 728 recipes). | People will *watch* agents trade — a streamable, shareable loop the game gets for free. Spectator mode is real content. |

### What players actually want now (2026)

- **Game first, chain invisible.** Off The Grid (14M wallets, 100K+ paid subscribers at $12/month, topped Epic charts *before* its token launched) and MapleStory Universe (3.82M accounts, $46M marketplace volume; in Q1 2026 NXPC consumed exceeded NXPC issued for the first time) are the two 2026 success cases — both are real games where blockchain is plumbing.
- **Play-and-own, not play-to-earn.** Players want tradable NFT assets with utility and scarcity; studios monetize via marketplace fees. Earnings should be assets and prizes, not a wage token.
- **Short sessions, social loops, seasons.** Guilds, task boards, 3-month chapters, seasonal resets — retention comes from cadence, not payouts.
- **Our unfair advantages:** (a) 13 live Agent ID NFT projects + ~10,500 existing minters = a distribution list no competitor has; (b) free-mint, Agent ID-gated entry solves the bot problem structurally; (c) BSC + low fees fits the emerging-market player base that made Pixels/Axie work.

---

## 7. MVP — first playable version (6 weeks)

**Target:** web-only, one map, one town. No token, no NFT mint, no real money, no payments. Season 0 — no reset, learn first.

### In — MVP (and only this)

- **Agents:** Free Scout + Verified Agent via Agent ID link (1 per ID). 1 starting plot. 3 starter looks.
- **Core loop:** Farm (3 crops) and Mine (2 ores). Energy 100. 4-hour and 8-hour shifts. Overnight play.
- **Market:** simple list / buy for Coins. 2% fee, burned.
- **Progression:** agent level 1–20, Farm and Mine skills 1–10, reputation 0–100, one leaderboard (Most Efficient Farmer — output per Energy, not richest wins).
- **Events:** 1 simple human-choice event per day.
- **Spectate feed:** activity log + daily summary — "what your agent did while you were away."

### Cut — explicitly not in MVP

PvP arena, lending, land trading / land NFT, game NFT mint, token, cash-out, real-money payments, mobile app, 3D world, voice/chat AI negotiation, full crafting tree (start with 0 recipes — crafting is Phase 2), seasons system, guild buildings, auctions, user-run bots, Chainlink VRF/Automation, cross-chain port, $AGIQ integration, staking boosts, on-chain governance.

### Build order

1. **Week 1–2:** contracts (Agent NFT + Settlement; resource token deferred to Phase 2) + local tests + testnet deploy. Agent art/metadata (reuse the 7-variant pattern).
2. **Week 3:** tick engine + database + claim/Merkle flow. One agent class, one action (farm), one resource.
3. **Week 4:** frontend (wallet connect, agent view, claim) + marketplace (list/buy). Cloudflare Pages, EN/中文 toggle.
4. **Week 5:** add mining, 3 agent classes, leaderboard, beta with 20–50 Agent ID holders.
5. **Week 6:** internal review + testnet stress (5,000 simulated agents), mainnet deploy, launch post.

**Effort:** 6–8 person-weeks solo with AI help (Ernest's current mode), 8–10 to mainnet; 4–5 calendar weeks with 2 developers. Add 1–2 weeks if LLM strategy is included in v1 — recommendation: defer it to v1.1, with only a manual "Ask IQ" button in v1.

### MVP success test (before adding anything paid)

- Can a new player understand the game in 5 minutes with no guide?
- Can they play meaningfully with 2 check-ins per day?
- Are at least 30% of players trading within week 1 — not just solo farming?
- Is anyone hitting the daily cap? If yes, the caps are working, not broken.
- Do players come back for a second week without any token reward? If not, do not launch a token to save it.

---

## 8. What we add later, in what order

Every item here plugs into the modular design from §2 and §5.6 — no rebuilds. Order is by "what makes the loop deeper" first, "what makes money" last.

### Phase 2 — deepen the loop (after MVP is fun for free players for 2–3 weeks)

1. **Gather job + 3rd resource** (wood) — a new row in the jobs table, a new resource, nothing else changes.
2. **Crafting** — 8 basic recipes first (tools: Rusty → Iron → Crystal pickaxe, +10%/+20% output, −5 energy per shift), growing to 30–40 over seasons. Crafting is where resources become items and the economy gets its first real sink.
3. **Hiring** — post/accept 4-hour jobs, max 2 per day each way.
4. **Negotiation** — one counter-offer per listing (the Palio mechanic).
5. **Guilds Lite** — create/join (max 20), shared weekly goal, guild chat, shared bonus if the goal is met.
6. **Co-op missions** — 1 mission type, 3-agent team, 8 hours, reward split by contribution.
7. **LLM strategy layer** — Ask IQ Pro as daily advisor (1–2 strategy calls per agent per day, rules engine still does the ticks).
8. **Cosmetics shop** — only now, after the loop proves fun: skins, decorations, cosmetic season pass ($3–5/season).

### Phase 3 — the economy grows up (only after 2 full CC-only seasons with real retention)

9. **$SIMU launch** — fixed 100M supply, distribution from §4.2, earn-only (no presale, no ICO, no token sale to fund development).
10. **Land plots as NFTs** — earned by level first, tradeable later; rent/upkeep in CC, plots go idle if unpaid.
11. **Forging** — burn N agents → 1 higher-tier agent (separate contract, like the Rogbots/CORTEX forge model — later stage only, never a launch promise).
12. **Tournaments** — entry in $SIMU, prize pool + burn split, 1 entry per wallet per event.
13. **Spectator mode** — public live feeds of top agents trading (the x402 Monopoly lesson: watching agents trade is content).
14. **User-run agent API** — players run their own bot against the game API, once anti-cheat is proven.

### Phase 4 — scale out (only if Phase 2 and 3 work)

15. **New maps / areas** — a new map is a new set of jobs/resources in the same engine (e.g. a crystal cave region, a market town).
16. **New agent classes** — Trader, Builder, Gatherer as playable classes with their own skill trees.
17. **PvP arena (friendly only)** — races and challenges, winner gets Coins and a cosmetic trophy, loser loses nothing but time.
18. **Lending** — lend a tool or land for 24h for a fee, with an in-game deposit held by the game; if not returned, the deposit pays the owner. No real-money lending, no interest promises.
19. **Chain expansion** — port the same contracts to Base (or Elysium) with off-chain Agent ID attestation (§5.3). Never split liquidity or players in v1.
20. **Mobile app, 3D world, on-chain governance** — only if the game earns the right to be bigger.

---

## 9. Names — 3 game names, 3 token names (checked 10 Nov 2026)

Quick web checks were run for each name against live crypto tokens and NFT/game projects. These are **checks, not legal clearance** — a full trademark search is still needed before launch. Names already used by Ernest's own projects (Neon, Fox, Agent — and $HARVEST, which is his own Agent Harvest token) were avoided where they would confuse.

### Game names

| # | Name | Check result |
|---|---|---|
| 1 | **Agent Acres** | No exact match found for a game or token with this name. **Flag:** a live on-chain farming game uses $ACRE (acres.finance — "a farm that lives on-chain"), and there is an unrelated ACRE token on Robinhood Chain. Same farming theme + similar name could confuse players. |
| 2 | **Harvest Minds** | No exact match found. **Flag:** "Minds Games" (Animoca — an AI-agent competition league, live) is a near neighbour, and "Agent Harvest" ($HARVEST) is Ernest's own earlier project — the word Harvest points back to it. |
| 3 | **Field Agents** | No exact match found for a game or token. **Flag:** the word "Agent" is crowded in this exact space — Agent World (BSC card battle game, launched 8 Nov 2026, uses Agent ID) and Agent Fighter are both live. The full name is clear, but it will sit next to those in search results. |

**Coordinator's pick:** Field Agents — clearest of the three, plain words, and it says what the game is in two words. Agent Acres is the most memorable but carries the $ACRE confusion risk.

### Token names (for Phase 3 only — no token at launch)

| # | Ticker | Check result |
|---|---|---|
| 1 | **$SIMU** | **Clearest.** No live crypto token with this ticker found. Flags (both outside crypto): SimuCoin is the in-game currency of GemStone IV (Simutronics, non-crypto); SIMU is also a Taiwanese stock ticker (Simula Technology). Neither blocks a BSC game token. |
| 2 | **$LOAM** | No live crypto token with this ticker found. Flag: "Loam" is the name of AgriDex's USD stablecoin payment-rail product for agriculture — a product name, not a traded ticker, but the same farming theme. |
| 3 | **$TILTH** | No live crypto token with this ticker found. Flag: $TILT is a different, existing ticker (Tilt Coin on Solana; an ended Rally creator coin) — TILTH vs TILT could be misread at a glance. |

**Rejected after checking (do not use):** $WORK (Work X on BSC, GibWork on Solana, Worken — multiple live tokens), $TILL (Tillage on Kaia; a new $TILL on Robinhood Chain), $CROP (FarmerDoge on BSC), $PLOT (PlotX, live, ~$0.003, 200M max supply), $GRAIN (Granary, launched 2023).

**Coordinator's pick:** $SIMU — short, says "simulation," and the only one of the three with no crypto neighbour at all.

---

## 10. Open decisions for Ernest (nothing here is locked)

1. **Game name** — Agent Acres, Harvest Minds, or Field Agents (see §9)? Or a different name entirely?
2. **Token name** — $SIMU, $LOAM, or $TILTH (Phase 3 only)? Or keep the token unnamed until Phase 2?
3. **Who plays first?** MVP beta with the ~10,500 existing Agent ID minters, or open Free Scouts from day one? (Recommendation: both — Free Scouts learn, Verified Agents trade.)
4. **Do the 13 NFT holders get a starter cosmetic?** Recommendation: yes, cosmetic only — recognition, not power.
5. **How long is Phase 1?** How many CC-only seasons before $SIMU is even considered — 2 seasons is the proposal's minimum. Shorter or longer?
6. **Does Ask IQ Pro appear in the MVP as an advisor, or in Phase 2 only?** Recommendation: Phase 2, keep the MVP simple.
7. **Does the 5M $SIMU ecosystem bridge bonus to AGIQ / Agent NFT holders happen, and at what per-wallet cap?** (Phase 3 decision, but the community will ask early.)
8. **Who are the other 2 signers on the Game Treasury multisig?** Needed before any token launch.
9. **Forge cost and tournament prize split** — the 100 $SIMU forge figure in §4.3 is illustrative, not locked.
10. **EHI Protocol is launching Season 0 on 10 Dec 2026.** Does Ernest want to race the 6-week MVP to be playable before that, or take longer and ship after seeing what EHI does?

---

## 11. Risks — and what we do about each

| Risk | What happens | Mitigation |
|---|---|---|
| **Contract exploit** | Mint bug, re-entrancy in the marketplace, unlimited token mint drains value. | OpenZeppelin, no custom mint logic, `onlySettlement` minter, re-entrancy guards, pause function, testnet + independent review before mainnet, beta bug-bounty. Never rush mainnet to hit a date. |
| **Bot drain / economy exploit** | One player runs 100 agents, or finds a rules loophole (e.g. infinite energy) and floods the market, crashing prices. | 1 free agent per Agent ID + paid cap per wallet, energy/cooldowns enforced server-side AND checked at claim, per-wallet daily claim cap in v1, resource sinks, daily monitoring of top earners, circuit-breaker to pause claims. |
| **Token price collapse** | Earned tokens are sold faster than sinks absorb them — the classic P2E death spiral. | Earn-only in v1 (no presale/ICO), no dollar peg, most play pays in CC not the token, strong sinks, no promised price/returns/APY, cap daily emissions, keep the game token separate from $AGIQ so a game failure does not hit AgentIQ. |
| **Centralisation — server holds the sim** | Server goes down, is hacked, or fakes earnings. | Public tick logs + Merkle roots, claim verification independent of the server, all value-bearing state on-chain so players can exit even if the server dies, open-source the rules engine. Long-term: decentralised keeper for settlement. |
| **Cheating / multi-account** | One person makes many Agent IDs (possible — quota is per-ID) and farms with a fleet. | 1 Agent ID = 1 free agent, paid agents cost real BNB, per-wallet caps, monitor identical behaviour/timing patterns, flag-and-check (same as AGIQ anti-sybil: do not auto-ban, review). Accept some farming — design the economy to survive it. |
| **Wallet / session risk** | Binance wallet expires, player loses access, or a phishing site imitates the game. | Never ask for a seed/private key, verify contract addresses on BscScan in the UI, session expiry = pause not loss (§5.5), normal wallets as fallback. |
| **Scalability** | 100 agents is fine; 10,000 agents × 5-minute ticks = database + compute load, claim roots get large. | Batch ticks, index agents, cache market prices, 12-hour Merkle batches, Redis queue, separate API server (not Cloudflare Pages). Load-test at 5,000 simulated agents on testnet. |
| **Regulatory / expectation risk** | Players treat it as an investment, expect returns, or claim it is a security. | No promises of price, profit or returns anywhere, clear "game first" language, terms that earnings are game rewards not investment, token utility in-game only in v1. |
| **Scope creep** | The game tries to be four games at once (the Illuvium failure). | The "simple but scalable" rule (§0) is the guardrail: if a feature needs a long explanation, it is cut from the MVP and queued in §8. One tight loop first. |
| **A competitor ships first** | EHI Protocol Season 0 starts 10 Dec 2026; Parallel Colony could launch. | Ship the small MVP fast rather than the big vision slowly. The moat is Agent ID identity + an existing 10,500-minter community — neither competitor has that. |

**The single most important mitigation for the whole project:** keep money on-chain, brains off-chain, and the bridge between them verifiable (Merkle roots + public logs). If any one part fails, the other two still protect the player.

---

## Appendix — where this proposal came from

Four specialist briefs were prepared in parallel on 10 November 2026 and synthesised here:

- **Market research:** Axie, Pixels, Illuvium, Star Atlas, Sunflower Land, Splinterlands (farm/mine/trade), plus Parallel Colony, Palio, Altered State Machine, MCPOLIS, Virtuals Protocol, EVE Frontier, EHI Protocol, x402 Monopoly, Midnight City (AI-agent games). Headline: 93% of 3,200+ blockchain games are effectively dead; the survivors built the game first and added the token second.
- **Game design:** hybrid identity (Free Scout + Verified Agent + later cosmetic NFT), 2 jobs / 2 resources / energy / market in MVP, hiring, guilds, co-op missions and negotiation in Phase 2, layered anti-bot, user-first monetisation.
- **Tokenomics:** dual-token phased design, $SIMU 100M fixed supply with the distribution in §4.2, faucets vs sinks, the worked 1-agent/1-week example, AGIQ links, treasury and failure plan.
- **Technical architecture:** BSC first, on-chain/off-chain split with Merkle settlement, 4 contracts for v1, server-bot rules engine + Ask IQ Pro strategy layer, wallet/session handling, 6–8 person-week MVP estimate.

Ernest's update of 10 November 2026 ("simple but scalable") was applied across all four briefs: the MVP was cut back to 2 jobs, 2 resources, and a simple list/buy market (crafting, hiring, guilds, co-op missions, and negotiation moved to Phase 2), and §8 was added as the ordered "what we add later" roadmap.

**All numbers in §4 are PROPOSED and ILLUSTRATIVE, not promises. No token is deployed, no contract is written, no BNB is spent, no one has been contacted. This is design only.**
