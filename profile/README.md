<div align="center">

<img src="https://raw.githubusercontent.com/SpawnAgent/Spawn-Agent/main/docs/logo.png" alt="SpawnAgent" width="600" />

# SpawnAgent

**Real-time on-chain intelligence platform built on OTP-inspired architecture**

[![Spawn-Agent](https://img.shields.io/badge/Spawn--Agent-v0.4.2-blueviolet?style=flat-square)](https://github.com/SpawnAgent/Spawn-Agent)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](https://github.com/SpawnAgent/Spawn-Agent/blob/main/LICENSE)

---

*Conceived and architected by [**José Valim**](https://github.com/josevalim) — creator of [Elixir](https://elixir-lang.org) and co-founder of [Dashbit](https://dashbit.co).*

*SpawnAgent brings the battle-tested supervision tree patterns from Erlang/OTP and the BEAM virtual machine into the world of blockchain analytics — process-per-wallet isolation, fault-tolerant pipelines, and let-it-crash resilience applied to on-chain monitoring at scale.*

</div>

---

### 🧬 What is SpawnAgent?

SpawnAgent is an **async-first blockchain monitoring framework** that treats every wallet, contract, and mempool stream as an isolated supervised process — inspired by how the BEAM VM manages millions of concurrent lightweight processes with graceful failure recovery.

Instead of monolithic scanners that crash when one RPC call fails, SpawnAgent **spawns** independent worker processes per target, each with its own state, restart policy, and circuit breaker. If a monitor fails, only that process restarts — the rest of the system keeps running.

### ⚡ Core Features

| Feature | Description |
|---------|------------|
| **OTP Supervision Trees** | Process-per-wallet isolation with configurable restart strategies (`one_for_one`, `one_for_all`, `rest_for_one`) |
| **Multi-Stage Pipelines** | Backpressure-aware processing with bounded async queues between stages |
| **Graph Analysis** | Fund flow tracing, cluster detection, shortest-path analysis across transaction graphs |
| **Anomaly Detection** | Statistical outlier detection using Z-score, IQR, and adaptive thresholds |
| **Pattern Matching** | Detects wash trading, wallet drains, airdrop farming, LP manipulation, and flash loan patterns |
| **Alert Dispatching** | Fan-out to Telegram, Discord, webhooks — with deduplication and rate limiting |
| **Provider Abstraction** | Connection pooling, automatic batching, and seamless WebSocket reconnection |

### 🚀 Quick Start

```bash
pip install spawn-agent
```

```python
from spawn_agent import SpawnAgent

agent = SpawnAgent.from_config("config.yml")

# Monitor a wallet — spawns a supervised worker process
agent.watch("0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045", label="vitalik.eth")

# React to on-chain events
@agent.on("large_transfer")
async def handle(event):
    print(f"🚨 {event['label']}: {event['value_eth']:.2f} ETH moved")

agent.start()
```

### 🔬 Why OTP Patterns?

Traditional blockchain monitoring tools are fragile — a single failed RPC call, a rate limit, or a malformed response can take down the entire system. SpawnAgent applies decades of telecom-grade reliability engineering:

- **Let it crash** — Workers that fail are automatically restarted with exponential backoff and circuit breakers, without affecting other monitors
- **Supervision hierarchies** — Nested supervisor trees allow fine-grained failure domains
- **Process isolation** — Each wallet monitor has its own state, event loop, and failure boundary
- **Backpressure** — Bounded queues between pipeline stages prevent memory exhaustion under load

These patterns have kept Erlang/OTP systems running at 99.9999999% uptime (nine nines) in production telecom systems since 1986.

### 📦 Project

→ **[SpawnAgent/Spawn-Agent](https://github.com/SpawnAgent/Spawn-Agent)** — Full source code, documentation, and examples

### 📊 Tech Stack

`Python 3.10+` · `asyncio` · `aiohttp` · `Click` · `PyYAML` · `Docker`

---

<div align="center">
<sub>Built with the philosophy that blockchain infrastructure deserves the same reliability guarantees as telecom switches.</sub>
</div>
