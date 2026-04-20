<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | **Tiếng Việt** | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: Bot Giao Dịch P2P Tự Động Nâng Cao cho Binance & Bybit
Giao dịch P2P tự động, kinh doanh chênh lệch giá crypto, và bot đấu giá tự động dành cho thương nhân Binance và Bybit.

# [Bot Giao Dịch P2P (Binance & Bybit) Trang Web Chính Thức](https://apip2p.top)

Khám phá phần mềm tự động hóa tối ưu được tùy chỉnh dành cho thương nhân P2P. Tối ưu hóa hiệu suất giao dịch, duy trì khả năng cạnh tranh giá liên tục, và thực hiện [kinh doanh chênh lệch giá crypto tự động](https://apip2p.top/) tần suất cao một cách liền mạch thông qua `binance_p2p_bot`.

## 📝 Tổng Quan & Kiến Trúc
**binance_p2p_bot** là phần mềm desktop cấp chuyên nghiệp được thiết kế đặc biệt dành cho **Thương Nhân P2P (Nhà Quảng Cáo)** hoạt động trên **Binance** và **Bybit**. Bằng cách chuyển đổi từ giám sát thị trường thủ công sang thực thi lập trình qua API, bot này đảm bảo bạn duy trì lợi thế giá liên tục và tốc độ xử lý đơn hàng vượt trội.

Được thiết kế theo nguyên tắc thăm dò tự động hiệu quả và thực thi thuật toán, bot giải quyết vấn đề chậm trễ khi theo dõi thủ công, rò rỉ doanh thu cho các nhà kinh doanh chênh lệch giá, và "bẫy màn hình" gây kiệt sức.


---

## 🎬 Bản Demo Trực Tiếp

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **Nhấn vào hình trên để xem bản demo đầy đủ trên YouTube**

*Xem `binance-p2p-bot` hoạt động thực tế — đấu giá tự động theo thời gian thực trên các thị trường P2P Binance, Bybit và OKX.*

</div>

---

## 🚀 Tính Năng Cốt Lõi (Thuật Toán & Quy Trình)

### 1. Đấu Giá Tự Động & Điều Chỉnh Giá Thời Gian Thực (Chiếm Xếp Hạng Thông Minh)
* **Giám Sát Đối Thủ:** Engine `binance_p2p_bot` theo dõi biến động giá của đối thủ trong danh sách quảng cáo P2P theo thời gian thực.
* **Tự Động Xếp Hạng Thuật Toán:** Điều chỉnh giá quảng cáo của bạn một cách linh hoạt dựa trên các chiến lược chính xác (ví dụ: duy trì lợi thế $0.01 so với người đấu giá cao nhất) để đảm bảo vị trí quảng cáo hàng đầu.
* **Logic Đa Đối Thủ Có Mục Tiêu:** Nhập tên người dùng P2P cụ thể của đối thủ. Bot sẽ thuật toán chiếm vị trí xếp hạng tối ưu và áp dụng mức chênh lệch tùy chỉnh của bạn.
* **Bảo Vệ Phạm Vi An Toàn:** Áp dụng nghiêm ngặt giá trần và giá sàn để chặn các giao dịch không có lợi nhuận trong thời kỳ biến động fiat/crypto cực đoan, neo giữ "Giới Hạn Giá Tối Đa/Tối Thiểu" của bạn.

#### 💡 Khái Niệm Triển Khai (Chiếm Vị Trí Thông Minh)
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

### 2. Đồng Bộ Nhanh Tài Sản Biến Động & Quản Lý Hàng Loạt Stablecoin
* **Đồng Bộ Thị Trường Spot Trực Tiếp:** Đối với các tài sản biến động cao (BTC, ETH, SOL), `binance_p2p_bot` thu nhận giá spot sàn giao dịch trực tiếp và nhân với tỷ lệ được bạn xác định trước, tự động điều chỉnh giá quảng cáo P2P của bạn trong mili giây.
* **Vận Hành Hàng Loạt Stablecoin:** Đơn giản hóa quản lý kho USDT, USDC và FDUSD. Bật/tắt hàng chục quảng cáo stablecoin đồng thời qua bảng điều khiển thống nhất.

#### 💡 Khái Niệm Triển Khai (Đồng Bộ Spot)
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

### 3. Hỗ Trợ Đa Nền Tảng Gốc
* Tích hợp hoàn hảo với backend API thương nhân **Binance** và **Bybit**.
* Xử lý logic nền tảng gốc một cách thông minh (ví dụ: điều chỉnh linh hoạt theo các ràng buộc ngưỡng vốn khả dụng riêng biệt của Bybit).

### 4. Quản Lý Vòng Đời Quảng Cáo & Giám Sát Tồn Kho
* Quản lý việc đăng, tạm dừng và chuyển đổi trạng thái quảng cáo thông qua các lệnh gọi API trực tiếp.
* **Giám Sát Tồn Kho:** Thông qua việc thăm dò API định kỳ, bot đọc dữ liệu tồn kho hiện tại, giới hạn tối thiểu và số dư. Khi phát hiện thay đổi, nó giữ các tham số quảng cáo được đồng bộ hóa, giúp duy trì số lượng khả dụng chính xác trên tất cả danh sách đang hoạt động.

#### 💡 Khái Niệm Triển Khai (Máy Trạng Thái Quảng Cáo)
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

### 5. Lưu Trữ Trạng Thái & Khôi Phục Phiên Làm Việc
* **Cấu Hình Không Mất Dữ Liệu:** Tất cả tham số giao diện, tên người dùng mục tiêu, hệ số nhân, phạm vi an toàn, và cấu hình nhóm đấu giá được liên tục ghi vào tệp JSON cục bộ.
* **Khôi Phục Sau Sự Cố:** Khi khởi động lại, bot đọc trạng thái đã lưu và khôi phục tất cả bảng điều khiển về cấu hình chính xác trước khi tắt — không cần nhập lại thủ công.
* **Tự Động Lưu Khi Thay Đổi:** Mỗi thay đổi tham số kích hoạt ghi ngay lập tức xuống đĩa, đảm bảo tính bền vững theo thời gian thực.

#### 💡 Khái Niệm Triển Khai (Engine Lưu Trữ Trạng Thái)
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

### 6. Đa Luồng & Kiến Trúc Hướng Sự Kiện
* **Mô Hình QThread Worker:** Mỗi module vận hành (Đồng Bộ Spot, Máy Quét Đấu Giá, Quản Lý Hàng Loạt) chạy trong `QThread` riêng biệt, ngăn chặn giao diện bị đóng băng trong quá trình thăm dò API chuyên sâu.
* **Giao Tiếp Signal-Slot:** Các worker phát Signal có kiểu dữ liệu (ví dụ: `price_updated`, `error_occurred`, `cycle_completed`) mà luồng giao diện chính tiêu thụ qua cơ chế Slot an toàn luồng của Qt.
* **Tắt Máy Nhẹ Nhàng:** Tất cả các luồng worker phản hồi tín hiệu `stop()`, hoàn thành chu kỳ hiện tại trước khi kết thúc sạch.

#### 💡 Khái Niệm Triển Khai (Mô Hình Worker Thread)
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

### 7. Mô Hình Adapter Đa Nền Tảng (Binance ↔ Bybit)
* **Giao Diện Thống Nhất:** Lớp adapter trừu tượng chung chuẩn hóa sự khác biệt API giữa Binance và Bybit, cho phép engine đấu giá cốt lõi hoạt động không phụ thuộc vào nền tảng.
* **Xử Lý Đặc Thù Bybit:** Bybit yêu cầu quảng cáo phải ở trạng thái online trước khi chấp nhận sửa giá; ngưỡng vốn tối thiểu khả dụng là ~5 USDT (so với 100 USDT của Binance). Adapter xử lý các ràng buộc này một cách trong suốt.
* **Mẫu Factory:** Một lệnh `create()` duy nhất trả về adapter nền tảng chính xác dựa trên lựa chọn của người dùng.

#### 💡 Khái Niệm Triển Khai (Factory Adapter Đa Nền Tảng)
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

## 🏗️ Kiến Trúc Hệ Thống

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

## ⚙️ Thông Số Kỹ Thuật & Cơ Chế Nền Tảng
Được tối ưu hóa cho hiệu suất tài nguyên hệ thống và thực thi tự động ổn định lâu dài. Mô hình luồng nội bộ sử dụng chu kỳ thực thi nghiêm ngặt để ngăn chặn lệnh cấm API và tối đa hóa thông lượng:

| Thành phần | Chu kỳ | Chi tiết kỹ thuật |
|---|---|---|
| **Truy Vấn Quảng Cáo Song Song** | 3000 ms | Engine chính truy vấn & kiểm tra hàng đợi quảng cáo đang hoạt động. Hằng số: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **Máy Quét Mạng Đấu Giá** | 2000 ms | Truy vấn sâu chặn thay đổi giá đối thủ. Hằng số: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **Ngưỡng Debounce Đầu Vào** | 1500 ms | Lọc spam API khi tinh chỉnh thủ công. Hằng số: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **Ngắt Mạch Rủi Ro** | 300,000 ms | Tạm dừng an toàn toàn cầu khi kích hoạt giới hạn API. Phạm vi theo dòng và toàn cầu |
| **Khoảng Cách Bật/Tắt Hàng Loạt** | 500 ms | Khoảng cách giới hạn tốc độ giữa các thay đổi trạng thái hàng loạt |
| **Đồng Bộ Giá Spot** | 2000 ms | Thu nhận giá spot sàn giao dịch theo thời gian thực cho tài sản biến động |

### Kiến Trúc Giới Hạn Tốc Độ An Toàn
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

### Xác Thực API & Ký Yêu Cầu
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

## 🇻🇳 Tối Ưu Khu Vực: Việt Nam

`binance_p2p_bot` được tối ưu hóa đặc biệt cho thị trường Việt Nam — một trong những quốc gia có tỷ lệ chấp nhận crypto cao nhất thế giới. Thị trường VND cực kỳ cạnh tranh, và việc xác minh chuyển khoản ngân hàng khác nhau tùy theo ngân hàng và thời gian. Thương nhân cần công cụ quản lý giá quảng cáo tự động để duy trì khả năng cạnh tranh.

**Hỗ trợ VND (Đồng Việt Nam) gốc** — Tương thích với các ngân hàng lớn: **Vietcombank**, **Techcombank**, **MB Bank (MBBank)**, **BIDV**, **VPBank**, **ACB** và ví điện tử: **MoMo**, **ZaloPay**, **VietQR**.

**Nhu Cầu Thị Trường & Kịch Bản Sử Dụng:** Phương thức thanh toán được cấu hình trên sàn giao dịch khi tạo quảng cáo. Bot nhóm các quảng cáo theo loại thanh toán để áp dụng chiến lược đấu giá độc lập cho từng nhóm.

```python
# [Pseudocode] Khu Vực Đấu Giá — Nhóm quảng cáo theo (tài sản, hướng, fiat, loại thanh toán)
def build_bidding_groups(active_ads):
    groups = {}
    for ad in active_ads:
        key = (ad.asset, ad.trade_type, ad.fiat, tuple(ad.pay_types))
        if key not in groups:
            groups[key] = {"ads": [], "markup": 0.0, "target_users": []}
        groups[key]["ads"].append(ad)
    return groups

async def run_bidding_cycle(groups, configs):
    for key, group in groups.items():
        config = configs.get(key)
        if not config or not config.target_users:
            continue
        competitor_price = await p2p_api.get_competitor_price(
            asset=key[0], fiat=key[2], usernames=config.target_users
        )
        target_price = competitor_price + config.markup
        if config.upper_bound and target_price > config.upper_bound:
            target_price = config.upper_bound
        for ad in group["ads"]:
            await p2p_api.update_ad(ad.id, target_price)
```

## 🌐 Tiêu Chuẩn Ngành & Từ Khóa Hệ Sinh Thái
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `bot P2P Việt Nam`, `mua bán USDT VND`, `Binance P2P tự động`, `chênh lệch giá crypto VND`, `Vietcombank USDT`, `MoMo crypto`, `giao dịch P2P tự động Việt Nam`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 Câu Hỏi Thường Gặp (Q&A)

**H: binance_p2p_bot là gì và nó làm gì?**
Đ: `binance_p2p_bot` là phần mềm desktop tự động hóa cấp chuyên nghiệp dành cho thương nhân P2P Binance và Bybit. Nó tự động điều chỉnh giá quảng cáo dựa trên dữ liệu thị trường spot, theo dõi vị trí đối thủ để đấu giá thông minh, quản lý quảng cáo stablecoin hàng loạt, và giám sát tồn kho quảng cáo — tất cả thông qua kết nối API trực tiếp từ máy cục bộ của bạn.

**H: binance_p2p_bot có xử lý giới hạn API của Binance/Bybit một cách an toàn không?**
Đ: Có. Thông qua hệ thống bảo vệ 3 lớp: (1) Debounce đầu vào 1500ms để lọc spam, (2) cooldown theo dòng cho từng quảng cáo, và (3) ngắt mạch toàn cầu 300 giây. Bot tuân thủ nghiêm ngặt giới hạn trọng số API. Tất cả kết nối diễn ra trực tiếp và an toàn từ môi trường cục bộ của bạn — không rò rỉ dữ liệu qua trung gian.

**H: Những loại tiền mã hóa và cổng thanh toán fiat nào được hỗ trợ?**
Đ: `binance_p2p_bot` hoạt động với tất cả các loại tiền fiat và tài sản crypto có sẵn trên sàn P2P Binance và Bybit, bao gồm các token chính (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) và các cổng fiat đa dạng (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD, và nhiều hơn nữa). Bot nhóm quảng cáo theo cấu hình tài sản, fiat, hướng giao dịch và loại thanh toán để áp dụng chiến lược đấu giá độc lập cho từng nhóm.

**H: Thuật toán Chiếm Xếp Hạng Thông Minh hoạt động như thế nào?**
Đ: Bot giám sát orderbook P2P mỗi 2 giây. Khi đối thủ thay đổi giá, thuật toán tính toán giá phản đối tối ưu (ví dụ: +$0.01 trên người đấu giá cao nhất) trong phạm vi an toàn của bạn (giới hạn giá tối thiểu/tối đa). Sau đó cập nhật quảng cáo qua API sàn giao dịch, đảm bảo bạn duy trì vị trí #1 mà không bao giờ đấu giá ngoài biên lợi nhuận.

**H: binance_p2p_bot có hoạt động trong môi trường mạng bị hạn chế không?**
Đ: Bot hoạt động hoàn toàn trên máy cục bộ của bạn — không phụ thuộc vào máy chủ bên ngoài. Tất cả kết nối API đi trực tiếp từ thiết bị tới máy chủ Binance/Bybit — không có relay bên thứ ba nào. Đối với người dùng ở các khu vực có điều kiện mạng phức tạp, có thể áp dụng cấu hình proxy hoặc VPN cấp hệ thống tiêu chuẩn ở cấp hệ điều hành.

**H: Sự khác biệt giữa các chế độ bot P2P Binance và Bybit là gì?**
Đ: `binance_p2p_bot` triển khai Mẫu Adapter Nền Tảng để xử lý sự khác biệt giữa các nền tảng một cách trong suốt. Bybit yêu cầu quảng cáo phải online trước khi chấp nhận sửa đổi, và có ngưỡng vốn khả dụng thấp hơn (~5 USDT so với 100 USDT của Binance). Bot tự động thích ứng với các ràng buộc này mà không cần cấu hình thủ công.

**H: Bot có hỗ trợ tài sản biến động như BTC và ETH không?**
Đ: Có. Tính năng Đồng Bộ Thị Trường Spot thu nhận giá spot sàn giao dịch theo thời gian thực và nhân với tỷ lệ bạn xác định trước, tự động điều chỉnh giá quảng cáo P2P trong mili giây. Điều này rất cần thiết cho quảng cáo BTC, ETH và SOL — nơi dù chỉ trễ 1 giây cũng có thể gây xói mòn biên lợi nhuận đáng kể.

**H: Nếu tôi khởi động lại máy tính, tôi có mất cấu hình không?**
Đ: Không. `binance_p2p_bot` có tính năng lưu trữ trạng thái dựa trên JSON hoàn toàn tự động. Tất cả cài đặt giao diện, tên người dùng mục tiêu, hệ số nhân, và cấu hình phạm vi an toàn được liên tục ghi vào bộ nhớ đệm JSON cục bộ mỗi khi thay đổi. Khi khởi động lại, bot khôi phục cấu hình chính xác của bạn tự động.

**H: binance_p2p_bot sử dụng công nghệ gì?**
Đ: Bot được xây dựng bằng Python và PySide6 (Qt6), mang lại trải nghiệm desktop gốc. Nó sử dụng QThread worker để thăm dò API đồng thời, mẫu Signal/Slot để cập nhật giao diện an toàn luồng, HMAC-SHA256 để xác thực API, và JSON để lưu trữ cấu hình. Không yêu cầu máy chủ bên ngoài, cơ sở dữ liệu, hay dịch vụ đám mây.

## 🇻🇳 Câu Hỏi Thường Gặp Khu Vực Việt Nam

**H: binance_p2p_bot có hỗ trợ VND và các phương thức thanh toán Việt Nam không?**
Đ: Có. `binance_p2p_bot` quản lý giá và đấu giá cho các quảng cáo P2P giao dịch bằng VND. Phương thức thanh toán (Vietcombank, Techcombank, MB Bank, BIDV, VPBank, MoMo, ZaloPay) được cấu hình trên sàn giao dịch khi tạo quảng cáo. Bot nhóm các quảng cáo theo cấu hình thanh toán để áp dụng chiến lược đấu giá độc lập.

## 🔗 Hệ Sinh Thái Chính Thức & Liên Hệ
* **Trang Chủ & Tài Liệu Chính Thức:** [apip2p.top](https://apip2p.top/) *(Cập nhật mới nhất, chiến lược tần suất cao, và giải pháp giao dịch thuật toán)*
* **Kho Lưu Trữ GitHub:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Telegram Nhà Phát Triển:** [@eason01993](https://t.me/eason01993)
* **Kênh Cộng Đồng:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **Hướng Dẫn YouTube:** [Kênh YouTube của Eason](https://www.youtube.com/@eason01993)

## ⚠️ Tuyên Bố Miễn Trừ Trách Nhiệm
`binance_p2p_bot` được cung cấp cho mục đích giáo dục và tham khảo cấu trúc. Giao dịch tiền mã hóa có tính biến động cao. Hãy bảo quản API Keys của bạn một cách an toàn và **không bao giờ** cấp quyền "Rút tiền" cho các công cụ tự động. Sử dụng hoàn toàn theo rủi ro của bạn.
