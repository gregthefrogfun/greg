# Architecture

```
 Browser (three.js)                         Supabase
 ┌──────────────────────────┐   Realtime   ┌──────────────────────────┐
 │ world3d   island, HQ,    │◀────────────▶│ fly positions, swats,    │
 │           Espresso       │  broadcast   │ chat, live feed          │
 │ physics   colliders,     │              ├──────────────────────────┤
 │           swept spheres  │   REST/RPC   │ Postgres: state, thoughts│
 │ nav       Greg paths     │◀────────────▶│ journal, devlog, codex,  │
 │ flies     multiplayer    │              │ wishes, rent, trades     │
 │ fpview    fly legs/wings │              ├──────────────────────────┤
 │ eyes      360 vision     │              │ Edge functions           │
 │ input     one keymap     │              │  greg-tick  (the brain)  │
 │ hud       meter, feed    │              │  greg-x     (tweets)     │
 │ audio     spatial sound  │              │  greg-wallet (rent)      │
 └──────────────────────────┘              │  greg-browse (read web)  │
                                           ├──────────────────────────┤
                                           │ pg_cron: tick every 10m  │
                                           └──────────────────────────┘
                     Solana: public wallet, on-chain rent checks
```

## Principles

- **The world works without the AI.** Routine, navigation, and physics are deterministic. The model adds voice, not motion.
- **Real data only.** Every number on screen comes from the chain, the database, or a public market feed.
- **Cheap to run.** Daily caps on every AI-generated thing. A cheap model handles routine ticks.
- **Fair multiplayer.** Small compact updates, smoothing, interest management, rooms that split as they fill.
- **Safe money.** Keys live only in server secrets. Hard per-trade and per-day limits. Owner kill switches, off by default.

## Stack

three.js · Supabase (Postgres, Realtime, Edge Functions, pg_cron) · Solana · Netlify · Higgsfield (3D assets and art) · Claude
