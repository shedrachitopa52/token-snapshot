A smart contract written in Clarity for the Stacks blockchain that implements a **Token Snapshot System** for **SIP-010 tokens**.  
This contract allows tracking of token states (balances, ownership, etc.) across different snapshots — enabling analytics, governance, and auditing of token distribution at specific block heights.

---

## 🚀 Features

- 📸 **Snapshot Tracking** — Record the current state of a SIP-010 token contract.
- 🔢 **Snapshot Counter** — Auto-incremented ID for each snapshot.
- ⛓️ **Block Height Mapping** — Each snapshot is tied to the block height it was taken at.
- 👤 **Admin Management** — Define an admin for access-controlled operations.
- 🧾 **Expandable Design** — Future updates can include storing user balances, admin-only access, and event logging.

---

## 🧩 Contract Overview

| Component | Type | Description |
|------------|------|-------------|
| `admin` | `data-var` | Stores the administrator principal. |
| `snapshot-counter` | `data-var` | Tracks the total number of snapshots. |
| `snapshots` | `map` | Maps a snapshot ID → block height. |
| `snapshot-balances` | `map` | (Planned) Maps `{ snapshot-id, user }` → token balance. |
| `ERR_ALREADY_SNAPSHOTTED` | `constant` | Error code `u100`. |
| `ERR_NOT_FOUND` | `constant` | Error code `u101`. |
| `ERR_UNAUTHORIZED` | `constant` | Error code `u102`. |
| `ERR_TOO_MANY_USERS` | `constant` | Error code `u103`. |

---

## ⚙️ Public Functions

### `take-snapshot`
```clarity
(define-public (take-snapshot) ...)
Creates a new snapshot:

Increments the snapshot-counter.

Records the current stacks-block-height.

Returns the new snapshot ID.

Returns: (ok uint) — The ID of the created snapshot.
```

`get-total-snapshots`

```clarity
`(define-read-only (get-total-snapshots) ...)`
Retrieves the total number of snapshots taken.

Returns: (ok uint) — The current snapshot count.
```

🧱 Example Usage
1. Take a Snapshot
```clarity
(contract-call? .token-snapshot take-snapshot)
;; => (ok u1)
```
2. Get Total Snapshots
```clarity
(contract-call? .token-snapshot get-total-snapshots)
;; => (ok u1)
```
🧮 Future Improvements (v0.2+)
🔐 Restrict `take-snapshot` to admin only.

💰 Capture and store user balances at snapshot time.

🪶 Add event emissions for snapshot creation.

🧾 Implement retrieval of per-user balances from historical snapshots.

🧠 Tech Stack
Language: Clarity

Blockchain: Stacks

Token Standard: SIP-010 Fungible Token Standard

