# marketplace-data_2026

Hourly snapshots of BBL + Boost marketplace state for the aDAO ecosystem.

Produced by the [`marketplace-stats`](https://github.com/defipatriot/cron-scripts/tree/main/marketplace-stats) cron in [`cron-scripts`](https://github.com/defipatriot/cron-scripts).

---

## Files

| File | Description | Cadence |
|---|---|---|
| [`data/marketplace.json`](./data/marketplace.json) | Current floors + listed counts + cumulative sales (master file) | Hourly |
| [`data/listings/bbl-{collection}.json`](./data/listings/) | Per-collection full BBL listings | Hourly |
| [`data/listings/boost-{collection}.json`](./data/listings/) | Per-collection full Boost listings | Hourly |
| [`data/activity-7d.json`](./data/activity-7d.json) | BBL activity feed, last 7 days | Hourly |
| [`data/sales/nft-sales-{year}.json`](./data/sales/) | Per-year sales history (BBL + Boost) | Hourly (append-only) |
| [`data/sales/index.json`](./data/sales/index.json) | Sales year index + cumulative totals | Hourly |
| [`data/heartbeat.json`](./data/heartbeat.json) | Uniform freshness signal | Hourly |

---

## Tracked collections

| Key | Label | Contract | BBL | Boost |
|---|---|---|:---:|:---:|
| `alliance_dao` | Alliance DAO | `terra1phr9...` | ✓ | ✓ |
| `pixelions` | pixeLions | `terra17z7...` | ✓ | ✓ |
| `tla_locks` | TLA Locks | `terra1uqhj...` | — | ✓ |

---

## Schema — `marketplace.json`

```json
{
  "schemaVersion": 1,
  "capturedAt": "2026-05-15T01:15:00.000Z",
  "epoch": 185,
  "prices_used": { "LUNA": 0.068, "bLUNA": 0.118 },
  "bbl": {
    "alliance_dao": {
      "floor_bluna": 230,
      "floor_usd": 27.14,
      "listed_count": 25,
      "broken_listed": 5,
      "unbroken_listed": 20,
      "unbroken_floor_bluna": 250,
      "volume_bluna": 12500,
      "volume_usd": 1475
    }
  },
  "boost": {
    "alliance_dao": {
      "listed_count": 8,
      "floor_by_token": {
        "LUNA":  { "floor": 1500, "floor_usd": 102 },
        "bLUNA": { "floor": 230,  "floor_usd": 27 }
      }
    }
  },
  "cumulative": {
    "bbl":   { "total_sales": 482, "total_volume_bluna": 95000 },
    "boost": { "total_sales": 31,  "total_volume_usd":  2840 },
    "combined_sales": 513
  }
}
```

---

## Consumers

- **`index.html` (Alliance DAO dashboard)** — replaces direct BBL/Boost API hits:
  - BBL Floor / Listed / Volume tiles
  - Boost Floor / Listed tiles  
  - Live Activity Feed
  - Sales History year-tabs
  - Listings modal (per-collection full listings)

---

## Companion data

[`nft-inventory-data_2026`](../nft-inventory-data_2026) provides on-chain per-NFT data (owner, broken, rank). The dashboard merges both feeds — `marketplace.json` knows which NFTs are listed; `nfts.json` knows their broken status, rank, and chain owner.
