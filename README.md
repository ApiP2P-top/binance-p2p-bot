<div align="center">

**🌐 Select Language /  选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: Advanced Binance & Bybit Automated P2P Trading Bot
Automated P2P trading, crypto arbitrage, and auto-bidding bot for Binance and Bybit merchants.

# [P2P Trading Bot (Binance & Bybit) Official Site](https://apip2p.top)

Discover the ultimate automation software customized for P2P merchants. Optimize your trading efficiency, maintain constant price competitiveness, and execute high-frequency [automated crypto arbitrage](https://apip2p.top/) seamlessly via `binance_p2p_bot`.

## 📝 Overview & Architecture
**binance_p2p_bot** is a professional-grade desktop client engineered specifically for **P2P Merchants (Advertisers)** operating on **Binance** and **Bybit**. By transitioning from manual market monitoring to API-driven programmatic execution, this bot ensures you maintain persistent price advantages and unmatched order processing speed. 

Built on efficient automated polling and algorithmic execution principles, it resolves manual tracking delays, revenue leakage to arbitrageurs, and the exhausting "screen trap". 


---

## 🎬 Live  Demo

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **Click the image above to watch the full demo on YouTube**

*See the `binance-p2p-bot` in action — real-time auto-bidding across Binance, Bybit, and OKX P2P markets.*

</div>

---

## 🚀 Core Features (Algorithm & Workflow)

### 1. Auto-Bidding & Real-time Price Adjustment (Smart Rank Sniping)
* **Competitor Monitoring:** The `binance_p2p_bot` engine tracks competitor price fluctuations in the P2P advertisement list in real time.
* **Algorithmic Auto-Ranking:** Dynamically tweaks your ad pricing based on precision strategies (e.g., maintaining a $0.01 edge over the top bidder) to guarantee premium ad placement.
* **Targeted Multi-Competitor Logic:** Input specific competitors' P2P usernames. The bot will algorithmically snipe the optimal ranking slot and apply your custom markup.
* **Safe Range Protection:** Enforces strict price ceilings and floors to block unprofitable transactions during extreme fiat/crypto volatility, anchoring your "Maximum/Minimum Price Limit".

#### 💡 Implementation Concept (Smart Sniping)
```python
# [Pseudocode Example] Auto-Ranking Mechanism
async def snipe_top_position(ad_id, target_merchant, offset_amount=0.01, min_price=1.00):
    # Fetch real-time ladder data
    orderbook = await p2p_api.get_competitor_ladder(target_merchant)
    
    # Calculate absolute supremacy price
    new_competitive_price = orderbook.top_price + offset_amount
    
    # Execute within strict risk boundaries
    if new_competitive_price >= min_price:
        await p2p_api.update_ad(ad_id, new_competitive_price)
```

### 2. Volatile Asset Fast Sync & Stablecoin Bulk Management
* **Live Spot Market Sync:** For high-volatility assets (BTC, ETH, SOL), `binance_p2p_bot` ingests live exchange spot prices and multiplies them by your predefined ratio, auto-correcting your P2P ad prices in milliseconds.
* **Stablecoin Bulk Operations:** Simplifies USDT, USDC, and FDUSD inventory. Toggle dozens of stablecoin ads online/offline concurrently via a unified dashboard.

#### 💡 Implementation Concept (Spot Sync)
```javascript
// [Pseudocode Example] Auto-Syncing P2P Ads with Spot Prices
async function runSpotMarketSync(symbol, your_multiplier) {
    // 1. Fetch real-time spot price from exchange
    const spotData = await exchange.api.fetchSpotTicker(symbol); // e.g., "BTC/USDT"
    
    // 2. Compute dynamic markup value
    const p2pTargetPrice = spotData.lastPrice * your_multiplier;
    
    // 3. Throttle and broadcast new prices safely
    await p2pManager.debounceUpdateAdsPrice(symbol, p2pTargetPrice);
}
```

### 3. Native Multi-Platform Support
* Integrates flawlessly with **Binance** and **Bybit** merchant API backends. 
* Handles native platform logic intelligently (e.g., dynamically adjusting to Bybit's distinct usable funding threshold constraints).

### 4. Ad Lifecycle Management & Inventory Monitoring
* Manages ad publishing, pausing, and status transitions through direct API calls.
* **Inventory Monitoring:** Through regular API polling, the bot reads your ads' current inventory, min limits, and balance data. When changes are detected, it keeps your ad parameters synchronized, helping maintain accurate available quantities across all active listings.

#### 💡 Implementation Concept (Ad State Machine)
```python
# [Pseudocode] Ad Lifecycle State Machine — ONLINE/OFFLINE transitions
class AdLifecycleManager:
    VALID_STATES = ["OFFLINE", "ONLINE", "FROZEN"]
    
    async def transition_ad(self, ad_id: str, target_state: str):
        current = await self.api.get_ad_status(ad_id)
        if current == target_state:
            return  # No-op: already in desired state
        
        if target_state == "ONLINE":
            await self.api.update_ad_status(ad_id, online=True)
        elif target_state == "OFFLINE":
            await self.api.update_ad_status(ad_id, online=False)
        
        self.state_cache[ad_id] = target_state
        logger.info(f"Ad {ad_id}: {current} → {target_state}")
    
    async def bulk_toggle(self, ad_ids: list, online: bool):
        """Batch switch multiple ads with rate-limit spacing"""
        for ad_id in ad_ids:
            target = "ONLINE" if online else "OFFLINE"
            await self.transition_ad(ad_id, target)
            await asyncio.sleep(0.5)  # 500ms spacing to avoid API burst
```

### 5. State Persistence & Session Recovery
* **Zero-loss Configuration:** All UI parameters, target usernames, multipliers, safe ranges, and bidding group configs are continuously written to a local JSON file.
* **Crash Recovery:** On restart, the bot reads the persisted state and restores all panels to their exact pre-shutdown configuration — no manual re-entry required.
* **Auto-save on Change:** Every parameter modification triggers an immediate write-through to disk, ensuring real-time durability.

#### 💡 Implementation Concept (State Persistence Engine)
```python
# [Pseudocode] JSON-Based State Persistence — Auto-save on every UI change
import json, os, time

class StatePersistence:
    CONFIG_FILE = "bot_state.json"
    
    def save_state(self, ui_state: dict):
        """Serialize full UI state to disk"""
        data = {
            "api_keys_encrypted": ui_state.get("encrypted_keys"),
            "target_usernames": ui_state.get("targets", []),
            "multipliers": ui_state.get("multipliers", {}),
            "safe_ranges": ui_state.get("price_bounds", {}),
            "active_groups": ui_state.get("bidding_groups", {}),
            "exchange_platform": ui_state.get("platform", "binance"),
            "language": ui_state.get("language", "en"),
            "last_saved": time.time()
        }
        with open(self.CONFIG_FILE, 'w', encoding='utf-8') as f:
            json.dump(data, f, indent=2, ensure_ascii=False)
    
    def load_state(self) -> dict:
        """Restore state from disk, fallback to defaults"""
        if not os.path.exists(self.CONFIG_FILE):
            return self._default_config()
        with open(self.CONFIG_FILE, 'r', encoding='utf-8') as f:
            return json.load(f)
    
    def auto_save_on_change(self, field: str, value):
        """Triggered by PySide6 Signal on any parameter change"""
        state = self.load_state()
        state[field] = value
        state["last_saved"] = time.time()
        self.save_state(state)
```

### 6. Thread Concurrency & Event-Driven Architecture
* **QThread Worker Model:** Each operational module (Spot Sync, Bidding Scanner, Bulk Manager) runs in its own dedicated `QThread`, preventing UI freezes during intensive API polling.
* **Signal-Slot Communication:** Workers emit typed Signals (e.g., `price_updated`, `error_occurred`, `cycle_completed`) that the main UI thread consumes via Qt’s thread-safe Slot mechanism.
* **Graceful Shutdown:** All worker threads respond to a `stop()` signal, completing their current cycle before terminating cleanly.

#### 💡 Implementation Concept (Worker Thread Model)
```python
# [Pseudocode] PySide6 QThread Worker — Bidding Scanner with Signal/Slot pattern
from PySide6.QtCore import QThread, Signal

class BiddingWorkerThread(QThread):
    # Typed signals for thread-safe UI communication
    price_updated = Signal(str, float)      # (ad_id, new_price)
    error_occurred = Signal(str, str)        # (ad_id, error_message)
    cycle_completed = Signal(int)            # (cycle_count)
    
    def __init__(self, api_client, config):
        super().__init__()
        self._running = False
        self._api = api_client
        self._config = config
        self._scan_interval_ms = 2000  # 2-second scan cycle
    
    def run(self):
        """Main worker loop — executes in background thread"""
        self._running = True
        cycle = 0
        while self._running:
            try:
                ads = self._api.fetch_active_ads()
                groups = build_bidding_groups(ads)
                
                for key, group in groups.items():
                    target_price = self._calculate_target(key, group)
                    if target_price:
                        for ad in group["ads"]:
                            self._api.update_price(ad.id, target_price)
                            self.price_updated.emit(ad.id, target_price)
                
                cycle += 1
                self.cycle_completed.emit(cycle)
            except APIRateLimitError as e:
                self.error_occurred.emit("GLOBAL", str(e))
                self.msleep(300_000)  # 300s circuit breaker
            
            self.msleep(self._scan_interval_ms)
    
    def stop(self):
        """Graceful shutdown — completes current cycle then exits"""
        self._running = False
```

### 7. Platform Adapter Pattern (Binance ↔ Bybit)
* **Unified Interface:** A common adapter abstraction normalizes API differences between Binance and Bybit, allowing the core bidding engine to operate platform-agnostically.
* **Bybit Quirks Handling:** Bybit requires ads to be online before accepting price edits; its minimum funding threshold is ~5 USDT (vs. Binance’s 100 USDT). The adapter handles these constraints transparently.
* **Factory Pattern:** A single `create()` call returns the correct platform adapter based on user selection.

#### 💡 Implementation Concept (Platform Adapter Factory)
```python
# [Pseudocode] Cross-Platform Adapter Factory — Binance & Bybit unified interface
class PlatformAdapterFactory:
    @staticmethod
    def create(platform: str, api_key: str, api_secret: str):
        if platform == "binance":
            return BinanceP2PAdapter(api_key, api_secret)
        elif platform == "bybit":
            return BybitP2PAdapter(api_key, api_secret)
        raise ValueError(f"Unsupported platform: {platform}")

class BinanceP2PAdapter:
    BASE_URL = "https://api.binance.com"
    
    async def get_ad_detail(self, ad_no: str):
        """Binance: POST /sapi/v1/c2c/ads/getDetailByNo"""
        return await self._signed_post(
            "/sapi/v1/c2c/ads/getDetailByNo", {"adsNo": ad_no}
        )
    
    async def update_ad_status(self, ad_no: str, online: bool):
        """Binance: POST /sapi/v1/c2c/ads/updateStatus"""
        return await self._signed_post(
            "/sapi/v1/c2c/ads/updateStatus",
            {"adsNo": ad_no, "status": 1 if online else 0}
        )
    
    async def update_ad_price(self, ad_no: str, price: float):
        """Binance: POST /sapi/v1/c2c/ads/update"""
        return await self._signed_post(
            "/sapi/v1/c2c/ads/update",
            {"adsNo": ad_no, "price": str(price)}
        )

class BybitP2PAdapter:
    BASE_URL = "https://api.bybit.com"
    REQUIRES_ONLINE_FOR_EDIT = True
    MIN_FUNDING_THRESHOLD = 5  # USDT (vs Binance's 100)
    
    async def update_ad_price(self, item_id: str, price: float):
        """Bybit: requires ad online before price edit"""
        if self.REQUIRES_ONLINE_FOR_EDIT:
            await self._ensure_ad_online(item_id)
        return await self._signed_post(
            "/v5/p2p/item/update",
            {"itemId": item_id, "price": str(price)}
        )
    
    async def _ensure_ad_online(self, item_id: str):
        status = await self.get_ad_status(item_id)
        if status != "ONLINE":
            await self._signed_post("/v5/p2p/item/online", {"itemId": item_id})
```

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                       PySide6 Desktop UI                        │
│  ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌─────────────┐ │
│  │  Volatile   │ │ Stablecoin  │ │  Bidding    │ │  Settings    │ │
│  │ Assets Tab  │ │  Bulk Tab   │ │  Zone Tab  │ │    Panel    │ │
│  └──────┬─────┘ └──────┬─────┘ └──────┬─────┘ └──────┬──────┘ │
│        │             │             │              │          │
│  ┌──────▼─────────────▼─────────────▼──────────────▼──────┐ │
│  │               Signal / Slot Event Bus                     │ │
│  └──────┬─────────────┬─────────────┬─────────────┬──────┘ │
│        │             │             │             │          │
│  ┌──────▼─────┐ ┌─────▼─────┐ ┌────▼──────┐ ┌────▼──────┐ │
│  │  Spot Sync  │ │  Bulk Mgr  │ │  Bid Scan  │ │   State    │ │
│  │   Worker   │ │   Worker   │ │   Worker  │ │  Persist   │ │
│  │ (3s cycle) │ │(on-demand) │ │(2s cycle) │ │   (JSON)   │ │
│  └──────┬─────┘ └─────┬─────┘ └────┬─────┘ └───────────┘ │
│        │             │             │                        │
│  ┌──────▼─────────────▼─────────────▼───────────────────┐ │
│  │           Rate Limiter & Circuit Breaker                  │ │
│  │  ┌─────────────┐ ┌──────────┐ ┌─────────────────────┐ │ │
│  │  │Input Debounce│ │ Row Lock  │ │ Global 300s Breaker   │ │ │
│  │  │  (1500 ms)   │ │ (per-ad)  │ │ (API limit guardian)  │ │ │
│  │  └─────────────┘ └──────────┘ └─────────────────────┘ │ │
│  └──────────────────────────┬──────────────────────────┘ │
└─────────────────────────────┼───────────────────────────────────┘
                             │
                ┌────────────▼─────────────┐
                │   Platform Adapter Layer    │
                │  ┌──────────┐ ┌──────────┐ │
                │  │ Binance  │ │  Bybit   │ │
                │  │ C2C API  │ │ C2C API  │ │
                │  └────┬─────┘ └─────┬────┘ │
                └───────┼───────────┼───────┘
                        │           │
               ┌────────▼───┐ ┌────▼───────┐
               │ Binance API │ │ Bybit API   │
               │   Server   │ │   Server    │
               └────────────┘ └────────────┘
```

---

## ⚙️ Technical Specifications & Underlying Mechanisms
Optimized for system resource efficiency and reliable long-running automated execution. The internal thread model utilizes rigorous execution cycles to prevent API bans and maximize throughput:

| Component | Interval | Technical Detail |
|---|---|---|
| **Parallel Ad Polling** | 3000 ms | Master engine queries & audits active ad queue. Constant: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **Bidding Network Scanner** | 2000 ms | Deep queries intercept competitor price shifts. Constant: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **Input Debounce Threshold** | 1500 ms | Filters API spam during manual tuning. Constant: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **Risk Circuit Breaker** | 300,000 ms | Global safety pause on API rate-limit trigger. Both per-row and global scope |
| **Bulk Toggle Spacing** | 500 ms | Rate-limit spacing between batch status changes |
| **Spot Price Sync** | 2000 ms | Real-time exchange spot price ingestion for volatile assets |

### Safety Rate Limiting Architecture
```python
# [Pseudocode] Multi-Layer Rate Limiting & Circuit Breaker
class RateLimitGuard:
    def __init__(self):
        self.row_cooldowns = {}        # Per-ad cooldown tracking
        self.global_breaker = False    # Global circuit breaker state
        self.breaker_duration = 300    # 300-second safety pause
        self.debounce_ms = 1500        # Input debounce threshold
        self._last_input_time = {}
    
    def should_debounce(self, ad_id: str) -> bool:
        """Layer 0: Input debounce — reject rapid duplicate inputs"""
        now = time.time() * 1000
        last = self._last_input_time.get(ad_id, 0)
        if now - last < self.debounce_ms:
            return True  # Too soon, skip this update
        self._last_input_time[ad_id] = now
        return False
    
    async def execute_with_guard(self, ad_id: str, operation):
        # Layer 1: Check global circuit breaker
        if self.global_breaker:
            raise CircuitBreakerActive("Global 300s cooldown in effect")
        
        # Layer 2: Check per-ad row cooldown
        if ad_id in self.row_cooldowns:
            remaining = self.row_cooldowns[ad_id] - time.time()
            raise RowCooldownActive(f"Ad {ad_id} in cooldown ({remaining:.0f}s)")
        
        # Layer 3: Execute with exception handling
        try:
            result = await operation()
            return result
        except APIRateLimitError:
            self.row_cooldowns[ad_id] = time.time() + self.breaker_duration
            self.global_breaker = True
            logger.critical(f"API rate limit — breaker engaged {self.breaker_duration}s")
            await asyncio.sleep(self.breaker_duration)
            self.global_breaker = False
            del self.row_cooldowns[ad_id]
```

### API Authentication & Request Signing
```python
# [Pseudocode] HMAC-SHA256 Request Signing — Securing API communication
import hashlib, hmac, time, urllib.parse

class APIAuthenticator:
    def __init__(self, api_key: str, api_secret: str):
        self.api_key = api_key
        self.api_secret = api_secret.encode('utf-8')
    
    def sign_request(self, params: dict) -> dict:
        """Generate HMAC-SHA256 signature for exchange API"""
        params['timestamp'] = int(time.time() * 1000)
        query_string = urllib.parse.urlencode(sorted(params.items()))
        signature = hmac.new(
            self.api_secret,
            query_string.encode('utf-8'),
            hashlib.sha256
        ).hexdigest()
        params['signature'] = signature
        return params
    
    def get_headers(self) -> dict:
        return {
            "X-MBX-APIKEY": self.api_key,
            "Content-Type": "application/x-www-form-urlencoded"
        }
```

## 🌐 Industry Standard & Ecosystem Keywords
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 Frequently Asked Questions (Q&A)

**Q: What is binance_p2p_bot and what does it do?**
A: `binance_p2p_bot` is a professional-grade desktop automation client for Binance and Bybit P2P merchants. It automatically adjusts your ad prices based on spot market data, tracks competitor positions for smart bidding, manages stablecoin ads in bulk, and monitors ad inventory — all via direct API connections from your local machine.

**Q: Does binance_p2p_bot handle Binance/Bybit API limits safely?**
A: Yes. Via a 3-layer protection system: (1) 1500ms input debounce to filter spam, (2) per-ad row cooldowns, and (3) a 300-second global circuit breaker. The bot strictly adheres to API weight limits. All connections occur directly and securely from your local environment with zero middleman data leakage.

**Q: What cryptocurrencies and fiat gateways are supported?**
A: `binance_p2p_bot` works with all fiat currencies and crypto assets available on Binance and Bybit P2P marketplaces, including major tokens (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) and diverse fiat gateways (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD, and more). The bot groups your advertisements by their configured asset, fiat, trade direction, and payment type combination for independent bidding strategies per group.

**Q: How does the Smart Rank Sniping algorithm work?**
A: The bot monitors the P2P orderbook every 2 seconds. When a competitor changes their price, the algorithm calculates an optimal counter-price (e.g., +$0.01 above the top bidder) within your defined safe range (min/max price boundaries). It then updates your ad via the exchange API, ensuring you maintain the #1 position without ever bidding outside your profit margins.

**Q: Does binance_p2p_bot work in restricted network environments?**
A: The bot operates entirely on your local machine with zero external server dependencies. All API connections go directly from your device to the Binance/Bybit servers — no third-party relay involved. For users in regions with complex network conditions, standard system-level proxy or VPN configurations can be applied at the OS level.

**Q: What are the differences between Binance and Bybit P2P bot modes?**
A: `binance_p2p_bot` implements a Platform Adapter Pattern to handle platform differences transparently. Bybit requires ads to be online before accepting edits, and has a lower usable funding threshold (~5 USDT vs. Binance’s 100 USDT). The bot auto-adapts to these constraints without manual configuration.

**Q: Does the bot support volatile assets like BTC and ETH?**
A: Yes. The Spot Market Sync feature ingests real-time exchange spot prices and multiplies them by your predefined ratio, auto-correcting P2P ad prices in milliseconds. This is essential for BTC, ETH, and SOL ads where even a 1-second delay can cause significant margin erosion.

**Q: If I restart my computer, will I lose my configuration?**
A: No. `binance_p2p_bot` features fully automated JSON-based state persistence. All UI settings, target usernames, multipliers, and safe range configurations are continuously written to a local JSON cache on every change. On restart, the bot restores your exact configuration automatically.

**Q: What technology stack does binance_p2p_bot use?**
A: The bot is built with Python and PySide6 (Qt6), providing a native desktop experience. It uses QThread workers for concurrent API polling, Signal/Slot patterns for thread-safe UI updates, HMAC-SHA256 for API authentication, and JSON for configuration persistence. No external servers, databases, or cloud services are required.

## 🔗 Official Ecosystem & Contact
* **Official Home & Documentation:** [apip2p.top](https://apip2p.top/) *(Latest updates, high-frequency strategies, and algorithmic trading solutions)*
* **GitHub Repository:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Developer Telegram:** [@eason01993](https://t.me/eason01993)
* **Community Channel:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube Guidance:** [Eason's YouTube Channel](https://www.youtube.com/@eason01993)

## ⚠️ Disclaimer
`binance_p2p_bot` is provided for educational and structural reference. Cryptocurrency trading is highly volatile. Safely store your API Keys and **never** assign "Withdrawal" permissions to automated tooling. Use entirely at your own risk.

