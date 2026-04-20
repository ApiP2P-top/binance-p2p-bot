<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | **اردو**

</div>

# binance_p2p_bot: ایڈوانسڈ Binance اور Bybit خودکار P2P ٹریڈنگ بوٹ
Binance اور Bybit تاجروں کے لیے خودکار P2P ٹریڈنگ، کرپٹو آربٹراج، اور آٹو بِڈنگ بوٹ۔

# [P2P ٹریڈنگ بوٹ (Binance اور Bybit) آفیشل سائٹ](https://apip2p.top)

P2P تاجروں کے لیے خاص طور پر تیار کردہ حتمی آٹومیشن سافٹ ویئر دریافت کریں۔ اپنی ٹریڈنگ کارکردگی کو بہتر بنائیں، مسلسل قیمتوں کی مسابقت برقرار رکھیں، اور `binance_p2p_bot` کے ذریعے ہائی فریکوئنسی [خودکار کرپٹو آربٹراج](https://apip2p.top/) کو بغیر کسی رکاوٹ کے انجام دیں۔

## 📝 جائزہ اور فن تعمیر
**binance_p2p_bot** ایک پیشہ ورانہ درجے کا ڈیسک ٹاپ کلائنٹ ہے جو خاص طور پر **Binance** اور **Bybit** پر کام کرنے والے **P2P تاجروں (مشتہرین)** کے لیے انجینئر کیا گیا ہے۔ دستی مارکیٹ نگرانی سے API پر مبنی پروگرامیٹک عمل درآمد میں منتقلی کر کے، یہ بوٹ یقینی بناتا ہے کہ آپ مستقل قیمت کے فوائد اور بے مثال آرڈر پروسیسنگ رفتار برقرار رکھیں۔

مؤثر خودکار پولنگ اور الگورتھمک عملدرآمد کے اصولوں پر تعمیر کیا گیا، یہ دستی ٹریکنگ میں تاخیر، آربٹراجرز کو آمدنی کے نقصان، اور تھکا دینے والے "اسکرین ٹریپ" کو حل کرتا ہے۔


---

## 🎬 لائیو ڈیمو

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **مکمل ڈیمو دیکھنے کے لیے اوپر کی تصویر پر کلک کریں (YouTube)**

*`binance-p2p-bot` کو عمل میں دیکھیں — Binance، Bybit، اور OKX P2P مارکیٹوں میں ریئل ٹائم آٹو بِڈنگ۔*

</div>

---

## 🚀 بنیادی خصوصیات (الگورتھم اور ورک فلو)

### 1. آٹو بِڈنگ اور ریئل ٹائم قیمت ایڈجسٹمنٹ (سمارٹ رینک سنائپنگ)
* **حریف نگرانی:** `binance_p2p_bot` انجن P2P اشتہار کی فہرست میں حریف قیمتوں کے اتار چڑھاؤ کو ریئل ٹائم میں ٹریک کرتا ہے۔
* **الگورتھمک آٹو رینکنگ:** پریمیم اشتہار کی جگہ بندی کی ضمانت کے لیے درست حکمت عملیوں (مثلاً سب سے اوپر بولی لگانے والے پر $0.01 کی برتری برقرار رکھنا) کی بنیاد پر آپ کے اشتہار کی قیمت کو متحرک طور پر ایڈجسٹ کرتا ہے۔
* **ٹارگٹڈ ملٹی کمپیٹیٹر لاجک:** مخصوص حریفوں کے P2P صارف نام درج کریں۔ بوٹ الگورتھمک طور پر بہترین رینکنگ سلاٹ کو سنائپ کرے گا اور آپ کا حسب ضرورت مارک اپ لاگو کرے گا۔
* **محفوظ رینج پروٹیکشن:** انتہائی فیاٹ/کرپٹو اتار چڑھاؤ کے دوران غیر منافع بخش لین دین کو روکنے کے لیے سخت قیمت کی حدیں اور فلورز نافذ کرتا ہے، آپ کی "زیادہ سے زیادہ/کم سے کم قیمت کی حد" کو مستحکم رکھتا ہے۔

#### 💡 عمل درآمد کا تصور (سمارٹ سنائپنگ)
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

### 2. غیر مستحکم اثاثوں کی فاسٹ سنک اور سٹیبل کوائن بلک انتظام
* **لائیو اسپاٹ مارکیٹ سنک:** زیادہ اتار چڑھاؤ والے اثاثوں (BTC, ETH, SOL) کے لیے، `binance_p2p_bot` لائیو ایکسچینج اسپاٹ قیمتیں حاصل کرتا ہے اور انہیں آپ کے پہلے سے طے شدہ تناسب سے ضرب دیتا ہے، ملی سیکنڈز میں آپ کے P2P اشتہار کی قیمتوں کو خود بخود درست کرتا ہے۔
* **سٹیبل کوائن بلک آپریشنز:** USDT, USDC, اور FDUSD انوینٹری کو آسان بناتا ہے۔ ایک متحد ڈیش بورڈ کے ذریعے بیک وقت درجنوں سٹیبل کوائن اشتہارات کو آن لائن/آف لائن ٹوگل کریں۔

#### 💡 عمل درآمد کا تصور (اسپاٹ سنک)
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

### 3. مقامی ملٹی پلیٹ فارم سپورٹ
* **Binance** اور **Bybit** مرچنٹ API بیک اینڈز کے ساتھ بغیر کسی رکاوٹ کے مربوط ہوتا ہے۔
* مقامی پلیٹ فارم لاجک کو ذہانت سے سنبھالتا ہے (مثلاً Bybit کی مخصوص قابل استعمال فنڈنگ تھریشولڈ رکاوٹوں کے مطابق متحرک ایڈجسٹمنٹ)۔

### 4. اشتہار لائف سائیکل مینجمنٹ اور انوینٹری مانیٹرنگ
* براہ راست API کالز کے ذریعے اشتہار کی اشاعت، معطلی، اور حیثیت کی منتقلی کا انتظام کرتا ہے۔
* **انوینٹری مانیٹرنگ:** باقاعدہ API پولنگ کے ذریعے، بوٹ آپ کے اشتہارات کی موجودہ انوینٹری، کم از کم حدود اور بیلنس ڈیٹا پڑھتا ہے۔ جب تبدیلیاں پائی جاتی ہیں، تو یہ آپ کے اشتہار کے پیرامیٹرز کو مطابقت میں رکھتا ہے، تمام فعال لسٹنگز میں درست دستیاب مقداروں کو برقرار رکھنے میں مدد کرتا ہے۔

#### 💡 عمل درآمد کا تصور (اشتہار اسٹیٹ مشین)
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

### 5. اسٹیٹ پرسسٹنس اور سیشن ریکوری
* **صفر نقصان کنفیگریشن:** تمام UI پیرامیٹرز، ٹارگٹ صارف نام، ملٹی پلائرز، محفوظ رینجز، اور بِڈنگ گروپ کنفیگریشنز مسلسل مقامی JSON فائل میں لکھے جاتے ہیں۔
* **کریش ریکوری:** ری اسٹارٹ پر، بوٹ محفوظ شدہ اسٹیٹ پڑھتا ہے اور تمام پینلز کو ان کی بالکل پہلے والی شٹ ڈاؤن کنفیگریشن میں بحال کرتا ہے — کسی دستی دوبارہ اندراج کی ضرورت نہیں۔
* **تبدیلی پر آٹو سیو:** ہر پیرامیٹر میں تبدیلی فوری رائٹ تھرو ٹرگر کرتی ہے، ریئل ٹائم پائیداری کو یقینی بناتی ہے۔

#### 💡 عمل درآمد کا تصور (اسٹیٹ پرسسٹنس انجن)
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

### 6. تھریڈ کنکرنسی اور ایونٹ سے چلنے والا فن تعمیر
* **QThread ورکر ماڈل:** ہر آپریشنل ماڈیول (Spot Sync, Bidding Scanner, Bulk Manager) اپنے مخصوص `QThread` میں چلتا ہے، جو گہری API پولنگ کے دوران UI فریز ہونے سے روکتا ہے۔
* **سگنل سلاٹ مواصلات:** ورکرز ٹائپڈ سگنلز (مثلاً `price_updated`, `error_occurred`, `cycle_completed`) خارج کرتے ہیں جنہیں مین UI تھریڈ Qt کے تھریڈ سیف سلاٹ میکانزم کے ذریعے استعمال کرتا ہے۔
* **خوش اسلوبی سے بندش:** تمام ورکر تھریڈز `stop()` سگنل کا جواب دیتے ہیں، صاف طریقے سے ختم ہونے سے پہلے اپنا موجودہ چکر مکمل کرتے ہیں۔

#### 💡 عمل درآمد کا تصور (ورکر تھریڈ ماڈل)
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

### 7. پلیٹ فارم اڈاپٹر پیٹرن (Binance ↔ Bybit)
* **متحد انٹرفیس:** ایک مشترکہ اڈاپٹر تجرید Binance اور Bybit کے درمیان API فرق کو نارملائز کرتی ہے، جس سے کور بِڈنگ انجن پلیٹ فارم سے آزادانہ طور پر کام کر سکتا ہے۔
* **Bybit خصوصیات کی ہینڈلنگ:** Bybit میں قیمت کی ترمیم قبول کرنے سے پہلے اشتہار آن لائن ہونا ضروری ہے؛ اس کی کم از کم فنڈنگ تھریشولڈ ~5 USDT ہے (بمقابلہ Binance کی 100 USDT)۔ اڈاپٹر ان رکاوٹوں کو شفاف طریقے سے سنبھالتا ہے۔
* **فیکٹری پیٹرن:** ایک واحد `create()` کال صارف کے انتخاب کی بنیاد پر درست پلیٹ فارم اڈاپٹر واپس کرتی ہے۔

#### 💡 عمل درآمد کا تصور (پلیٹ فارم اڈاپٹر فیکٹری)
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

## 🏗️ سسٹم آرکیٹیکچر

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

## ⚙️ تکنیکی تفصیلات اور بنیادی میکانزم
سسٹم وسائل کی کارکردگی اور قابل اعتماد طویل مدتی خودکار عملدرآمد کے لیے بہتر بنایا گیا۔ اندرونی تھریڈ ماڈل API پابندیوں کو روکنے اور تھرو پٹ کو زیادہ سے زیادہ کرنے کے لیے سخت عملداری چکروں کا استعمال کرتا ہے:

| جزو | وقفہ | تکنیکی تفصیل |
|---|---|---|
| **متوازی اشتہار پولنگ** | 3000 ms | ماسٹر انجن فعال اشتہار قطار کو استفسار اور آڈٹ کرتا ہے۔ ثابت: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **بِڈنگ نیٹ ورک اسکینر** | 2000 ms | گہرے استفسارات حریف قیمت کی تبدیلیوں کو روکتے ہیں۔ ثابت: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **ان پٹ ڈیباؤنس تھریشولڈ** | 1500 ms | دستی ٹیوننگ کے دوران API سپیم فلٹر کرتا ہے۔ ثابت: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **رسک سرکٹ بریکر** | 300,000 ms | API ریٹ لمٹ ٹرگر پر عالمی حفاظتی وقفہ۔ فی قطار اور عالمی دونوں دائرہ کار |
| **بلک ٹوگل اسپیسنگ** | 500 ms | بیچ حیثیت کی تبدیلیوں کے درمیان ریٹ لمٹ اسپیسنگ |
| **اسپاٹ پرائس سنک** | 2000 ms | غیر مستحکم اثاثوں کے لیے ریئل ٹائم ایکسچینج اسپاٹ قیمت حاصل کرنا |

### سیفٹی ریٹ لِمٹنگ آرکیٹیکچر
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

### API تصدیق اور درخواست پر دستخط
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

## 🇵🇰 علاقائی اصلاح: پاکستان

`binance_p2p_bot` پاکستانی P2P مارکیٹ کے لیے مکمل طور پر بہتر بنایا گیا ہے، جس میں **PKR (پاکستانی روپے)** کی مقامی سپورٹ شامل ہے۔

### سپورٹ شدہ ادائیگی کے طریقے
* **JazzCash** — پاکستان کا سب سے زیادہ استعمال ہونے والا موبائل والیٹ
* **Easypaisa** — وسیع پیمانے پر استعمال ہونے والا موبائل ادائیگی پلیٹ فارم
* **HBL (Habib Bank)** — پاکستان کا سب سے بڑا نجی بینک
* **UBL (United Bank)** — بڑے لین دین کے لیے قابل اعتماد
* **Meezan Bank** — اسلامی بینکاری کے لیے سرکردہ
* **Bank Al Falah, Allied Bank** — اضافی بینکنگ اختیارات

### مارکیٹ ضروریات اور استعمال کے منظرنامے
محدود بینکنگ انفراسٹرکچر موبائل والیٹس (JazzCash، Easypaisa) کو انتہائی اہم بناتا ہے۔ PKR کے اتار چڑھاؤ اور سرمائے کے کنٹرول کی وجہ سے، P2P کرپٹو میں داخلے کا بنیادی ذریعہ ہے۔ محفوظ مقامی ٹولز کی ضرورت ہے جو بیرونی سرورز کے بغیر چلیں۔ ادائیگی کے طریقے (JazzCash، Easypaisa وغیرہ) ایکسچینج میں ترتیب دیے جاتے ہیں؛ بوٹ آزاد بِڈنگ حکمت عملیوں کے لیے اشتہارات کو ادائیگی کی قسم کے مطابق گروپ کرتا ہے۔

#### 💡 عمل درآمد کا تصور (پاکستان موبائل والیٹ اور بینکنگ انضمام)
```python
# [Pseudocode] Bidding Zone — Group ads by (asset, trade_type, fiat, pay_type)
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

## 🌐 صنعتی معیار اور ایکو سسٹم کلیدی الفاظ
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `P2P بوٹ پاکستان`, `کرپٹو آربٹراج PKR`, `USDT خرید و فروخت`, `Binance P2P خودکار پاکستان`, `JazzCash کرپٹو`, `Easypaisa USDT`, `خودکار P2P ٹریڈنگ پاکستان`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />

## 💡 اکثر پوچھے جانے والے سوالات (Q&A)

**سوال: binance_p2p_bot کیا ہے اور یہ کیا کرتا ہے؟**
جواب: `binance_p2p_bot` Binance اور Bybit P2P تاجروں کے لیے ایک پیشہ ورانہ درجے کا ڈیسک ٹاپ آٹومیشن کلائنٹ ہے۔ یہ اسپاٹ مارکیٹ ڈیٹا کی بنیاد پر آپ کے اشتہار کی قیمتوں کو خودکار طور پر ایڈجسٹ کرتا ہے، سمارٹ بِڈنگ کے لیے حریف پوزیشنز کو ٹریک کرتا ہے، سٹیبل کوائن اشتہارات کو بلک میں منظم کرتا ہے، اور اشتہار انوینٹری کی نگرانی کرتا ہے — یہ سب آپ کی مقامی مشین سے براہ راست API کنکشنز کے ذریعے۔

**سوال: کیا binance_p2p_bot Binance/Bybit API حدود کو محفوظ طریقے سے سنبھالتا ہے؟**
جواب: جی ہاں۔ 3 سطحی تحفظ کے نظام کے ذریعے: (1) سپیم فلٹر کرنے کے لیے 1500ms ان پٹ ڈیباؤنس، (2) فی اشتہار قطار کولڈاؤنز، اور (3) 300 سیکنڈ عالمی سرکٹ بریکر۔ بوٹ API ویٹ لِمٹس کی سختی سے پابندی کرتا ہے۔ تمام کنکشن براہ راست اور محفوظ طریقے سے آپ کے مقامی ماحول سے ہوتے ہیں (صفر درمیانی ڈیٹا لیکیج)۔

**سوال: کون سی کرپٹو کرنسیز اور فیاٹ گیٹ ویز سپورٹ ہیں؟**
جواب: `binance_p2p_bot` Binance اور Bybit P2P مارکیٹ پلیسز پر دستیاب تمام فیاٹ کرنسیوں اور کرپٹو اثاثوں کے ساتھ کام کرتا ہے، بشمول بڑے ٹوکنز (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) اور متنوع فیاٹ گیٹ ویز (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD، اور مزید)۔ بوٹ آزاد بِڈنگ حکمت عملیوں کے لیے اشتہارات کو ان کے ترتیب شدہ اثاثے، فیاٹ، تجارت کی سمت، اور ادائیگی کی قسم کے مجموعے کے مطابق گروپ کرتا ہے۔

**سوال: سمارٹ رینک سنائپنگ الگورتھم کیسے کام کرتا ہے؟**
جواب: بوٹ ہر 2 سیکنڈ میں P2P آرڈر بک کی نگرانی کرتا ہے۔ جب کوئی حریف اپنی قیمت تبدیل کرتا ہے، تو الگورتھم آپ کی مقرر کردہ محفوظ رینج (کم از کم/زیادہ سے زیادہ قیمت کی حدود) کے اندر ایک بہترین جوابی قیمت (مثلاً سب سے اوپر بولی لگانے والے سے +$0.01 اوپر) کا حساب لگاتا ہے۔ پھر یہ ایکسچینج API کے ذریعے آپ کا اشتہار اپ ڈیٹ کرتا ہے، یہ یقینی بناتے ہوئے کہ آپ اپنے منافع کے مارجن سے باہر بولی لگائے بغیر #1 پوزیشن برقرار رکھیں۔

**سوال: کیا binance_p2p_bot محدود نیٹ ورک ماحول میں کام کرتا ہے؟**
جواب: بوٹ مکمل طور پر آپ کی مقامی مشین پر صفر بیرونی سرور انحصار کے ساتھ کام کرتا ہے۔ تمام API کنکشن آپ کے آلے سے براہ راست Binance/Bybit سرورز پر جاتے ہیں — کوئی تھرڈ پارٹی ریلے شامل نہیں۔ پیچیدہ نیٹ ورک حالات والے خطوں میں صارفین کے لیے، معیاری سسٹم لیول پراکسی یا VPN کنفیگریشنز OS سطح پر لاگو کی جا سکتی ہیں۔

**سوال: Binance اور Bybit P2P بوٹ موڈز میں کیا فرق ہے؟**
جواب: `binance_p2p_bot` پلیٹ فارم کے فرق کو شفاف طریقے سے سنبھالنے کے لیے پلیٹ فارم اڈاپٹر پیٹرن لاگو کرتا ہے۔ Bybit میں ترمیم قبول کرنے سے پہلے اشتہار آن لائن ہونا ضروری ہے، اور اس کی قابل استعمال فنڈنگ تھریشولڈ کم ہے (~5 USDT بمقابلہ Binance کی 100 USDT)۔ بوٹ دستی کنفیگریشن کے بغیر ان رکاوٹوں کے مطابق خودکار طور پر ڈھل جاتا ہے۔

**سوال: کیا بوٹ BTC اور ETH جیسے غیر مستحکم اثاثوں کو سپورٹ کرتا ہے؟**
جواب: جی ہاں۔ اسپاٹ مارکیٹ سنک فیچر ریئل ٹائم ایکسچینج اسپاٹ قیمتیں حاصل کرتا ہے اور انہیں آپ کے پہلے سے طے شدہ تناسب سے ضرب دیتا ہے، ملی سیکنڈز میں P2P اشتہار کی قیمتوں کو خود بخود درست کرتا ہے۔ یہ BTC, ETH, اور SOL اشتہارات کے لیے ضروری ہے جہاں 1 سیکنڈ کی تاخیر بھی نمایاں مارجن کٹاؤ کا سبب بن سکتی ہے۔

**سوال: اگر میں اپنا کمپیوٹر دوبارہ شروع کروں، تو کیا میری کنفیگریشن ضائع ہو جائے گی؟**
جواب: نہیں۔ `binance_p2p_bot` میں مکمل خودکار JSON پر مبنی اسٹیٹ پرسسٹنس ہے۔ تمام UI سیٹنگز، ٹارگٹ صارف نام، ملٹی پلائرز، اور محفوظ رینج کنفیگریشنز ہر تبدیلی پر مسلسل مقامی JSON کیش میں لکھی جاتی ہیں۔ ری اسٹارٹ پر، بوٹ خودکار طور پر آپ کی عین مطابق کنفیگریشن بحال کرتا ہے۔

**سوال: binance_p2p_bot کون سا ٹیکنالوجی اسٹیک استعمال کرتا ہے؟**
جواب: بوٹ Python اور PySide6 (Qt6) کے ساتھ بنایا گیا ہے، جو ایک مقامی ڈیسک ٹاپ تجربہ فراہم کرتا ہے۔ یہ متوازی API پولنگ کے لیے QThread ورکرز، تھریڈ سیف UI اپ ڈیٹس کے لیے Signal/Slot پیٹرنز، API تصدیق کے لیے HMAC-SHA256، اور کنفیگریشن پرسسٹنس کے لیے JSON استعمال کرتا ہے۔ کسی بیرونی سرور، ڈیٹابیس، یا کلاؤڈ سروسز کی ضرورت نہیں ہے۔

## 🇵🇰 پاکستان کے مخصوص اکثر پوچھے جانے والے سوالات

**سوال: کیا binance_p2p_bot PKR اور پاکستانی ادائیگی کے طریقوں کے ساتھ کام کرتا ہے؟**
جواب: بوٹ قیمت/بِڈنگ کا انتظام کرتا ہے۔ ادائیگی کے طریقے (JazzCash، Easypaisa وغیرہ) ایکسچینج میں ترتیب دیے جاتے ہیں۔ بوٹ آزاد بِڈنگ حکمت عملیوں کے لیے اشتہارات کو ادائیگی کی ترتیب کے مطابق گروپ کرتا ہے۔

## 🔗 آفیشل ایکو سسٹم اور رابطہ
* **آفیشل ہوم اور دستاویزات:** [apip2p.top](https://apip2p.top/) *(تازہ ترین اپ ڈیٹس، ہائی فریکوئنسی حکمت عملیاں، اور الگورتھمک ٹریڈنگ حل)*
* **GitHub ریپوزٹری:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **ڈویلپر Telegram:** [@eason01993](https://t.me/eason01993)
* **کمیونٹی چینل:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube رہنمائی:** [Eason کا YouTube چینل](https://www.youtube.com/@eason01993)

## ⚠️ دستبرداری
`binance_p2p_bot` تعلیمی اور ساختی حوالے کے لیے فراہم کیا گیا ہے۔ کرپٹو کرنسی ٹریڈنگ انتہائی غیر مستحکم ہے۔ اپنی API Keys کو محفوظ طریقے سے محفوظ کریں اور خودکار ٹولنگ کو **کبھی بھی** "نکلوانے" کی اجازت نہ دیں۔ مکمل طور پر اپنے خطرے پر استعمال کریں۔
