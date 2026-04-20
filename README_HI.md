<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | **हिन्दी** | [اردو](README_UR.md)

</div>

# binance_p2p_bot: उन्नत Binance और Bybit स्वचालित P2P ट्रेडिंग बोट
Binance और Bybit व्यापारियों के लिए स्वचालित P2P ट्रेडिंग, क्रिप्टो आर्बिट्राज, और ऑटो-बिडिंग बोट।

# [P2P ट्रेडिंग बोट (Binance और Bybit) आधिकारिक साइट](https://apip2p.top)

P2P व्यापारियों के लिए अनुकूलित अंतिम ऑटोमेशन सॉफ्टवेयर की खोज करें। अपनी ट्रेडिंग दक्षता अनुकूलित करें, निरंतर मूल्य प्रतिस्पर्धात्मकता बनाए रखें, और `binance_p2p_bot` के माध्यम से उच्च-आवृत्ति [स्वचालित क्रिप्टो आर्बिट्राज](https://apip2p.top/) को निर्बाध रूप से निष्पादित करें।

## 📝 अवलोकन और आर्किटेक्चर
**binance_p2p_bot** एक पेशेवर-ग्रेड डेस्कटॉप क्लाइंट है जो विशेष रूप से **Binance** और **Bybit** पर संचालित **P2P व्यापारियों (विज्ञापनदाताओं)** के लिए इंजीनियर किया गया है। मैन्युअल बाजार निगरानी से API-संचालित प्रोग्रामेटिक निष्पादन में संक्रमण करके, यह बोट सुनिश्चित करता है कि आप स्थायी मूल्य लाभ और अद्वितीय ऑर्डर प्रोसेसिंग गति बनाए रखें।

कुशल स्वचालित पोलिंग और एल्गोरिदमिक निष्पादन सिद्धांतों पर निर्मित, यह मैन्युअल ट्रैकिंग में देरी, आर्बिट्राजर्स को राजस्व रिसाव, और थकाऊ "स्क्रीन ट्रैप" का समाधान करता है।


---

## 🎬 लाइव डेमो

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **पूर्ण डेमो देखने के लिए ऊपर की छवि पर क्लिक करें (YouTube)**

*`binance-p2p-bot` को एक्शन में देखें — Binance, Bybit, और OKX P2P बाजारों में रियल-टाइम ऑटो-बिडिंग।*

</div>

---

## 🚀 मुख्य विशेषताएँ (एल्गोरिदम और वर्कफ़्लो)

### 1. ऑटो-बिडिंग और रियल-टाइम मूल्य समायोजन (स्मार्ट रैंक स्नाइपिंग)
* **प्रतिस्पर्धी निगरानी:** `binance_p2p_bot` इंजन P2P विज्ञापन सूची में प्रतिस्पर्धी मूल्य उतार-चढ़ाव को रियल टाइम में ट्रैक करता है।
* **एल्गोरिदमिक ऑटो-रैंकिंग:** सटीक रणनीतियों (जैसे, शीर्ष बोलीदाता पर $0.01 की बढ़त बनाए रखना) के आधार पर आपके विज्ञापन मूल्य निर्धारण को गतिशील रूप से समायोजित करता है ताकि प्रीमियम विज्ञापन प्लेसमेंट की गारंटी हो।
* **लक्षित बहु-प्रतिस्पर्धी लॉजिक:** विशिष्ट प्रतिस्पर्धियों के P2P यूज़रनेम दर्ज करें। बोट एल्गोरिदमिक रूप से इष्टतम रैंकिंग स्लॉट को स्नाइप करेगा और आपका कस्टम मार्कअप लागू करेगा।
* **सुरक्षित सीमा संरक्षण:** चरम फिएट/क्रिप्टो अस्थिरता के दौरान लाभहीन लेनदेन को रोकने के लिए सख्त मूल्य सीमाएँ और फ्लोर लागू करता है, आपकी "अधिकतम/न्यूनतम मूल्य सीमा" को स्थिर रखता है।

#### 💡 कार्यान्वयन अवधारणा (स्मार्ट स्नाइपिंग)
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

### 2. अस्थिर संपत्ति फास्ट सिंक और स्टेबलकॉइन बल्क प्रबंधन
* **लाइव स्पॉट मार्केट सिंक:** उच्च-अस्थिरता संपत्तियों (BTC, ETH, SOL) के लिए, `binance_p2p_bot` लाइव एक्सचेंज स्पॉट मूल्यों को ग्रहण करता है और उन्हें आपके पूर्वनिर्धारित अनुपात से गुणा करता है, मिलीसेकंड में आपके P2P विज्ञापन मूल्यों को स्वचालित रूप से सही करता है।
* **स्टेबलकॉइन बल्क ऑपरेशंस:** USDT, USDC, और FDUSD इन्वेंटरी को सरल बनाता है। एकीकृत डैशबोर्ड के माध्यम से दर्जनों स्टेबलकॉइन विज्ञापनों को एक साथ ऑनलाइन/ऑफलाइन टॉगल करें।

#### 💡 कार्यान्वयन अवधारणा (स्पॉट सिंक)
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

### 3. नेटिव मल्टी-प्लेटफ़ॉर्म सपोर्ट
* **Binance** और **Bybit** मर्चेंट API बैकएंड के साथ निर्बाध रूप से एकीकृत होता है।
* नेटिव प्लेटफ़ॉर्म लॉजिक को बुद्धिमानी से संभालता है (जैसे, Bybit की विशिष्ट उपयोग योग्य फंडिंग थ्रेशोल्ड बाधाओं के अनुसार गतिशील रूप से समायोजन)।

### 4. विज्ञापन जीवनचक्र प्रबंधन और इन्वेंटरी निगरानी
* सीधे API कॉल के माध्यम से विज्ञापन प्रकाशन, विराम, और स्थिति संक्रमणों का प्रबंधन करता है।
* **इन्वेंटरी निगरानी:** नियमित API पोलिंग के माध्यम से, बोट आपके विज्ञापनों की वर्तमान इन्वेंटरी, न्यूनतम सीमाएँ और बैलेंस डेटा पढ़ता है। जब परिवर्तन पाए जाते हैं, तो यह आपके विज्ञापन पैरामीटर को सिंक्रनाइज़ रखता है, सभी सक्रिय लिस्टिंग में सटीक उपलब्ध मात्रा बनाए रखने में मदद करता है।

#### 💡 कार्यान्वयन अवधारणा (विज्ञापन स्टेट मशीन)
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

### 5. स्टेट पर्सिस्टेंस और सेशन रिकवरी
* **शून्य-हानि कॉन्फ़िगरेशन:** सभी UI पैरामीटर, लक्ष्य यूज़रनेम, गुणक, सुरक्षित सीमाएँ, और बिडिंग समूह कॉन्फ़िगरेशन लगातार स्थानीय JSON फ़ाइल में लिखे जाते हैं।
* **क्रैश रिकवरी:** पुनरारंभ पर, बोट पर्सिस्टेड स्टेट पढ़ता है और सभी पैनलों को उनके ठीक पूर्व-शटडाउन कॉन्फ़िगरेशन में पुनर्स्थापित करता है — कोई मैन्युअल पुनः प्रविष्टि आवश्यक नहीं।
* **परिवर्तन पर ऑटो-सेव:** प्रत्येक पैरामीटर संशोधन एक तत्काल राइट-थ्रू ट्रिगर करता है, रियल-टाइम स्थायित्व सुनिश्चित करता है।

#### 💡 कार्यान्वयन अवधारणा (स्टेट पर्सिस्टेंस इंजन)
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

### 6. थ्रेड कन्करेंसी और इवेंट-ड्रिवन आर्किटेक्चर
* **QThread वर्कर मॉडल:** प्रत्येक ऑपरेशनल मॉड्यूल (Spot Sync, Bidding Scanner, Bulk Manager) अपने समर्पित `QThread` में चलता है, जो गहन API पोलिंग के दौरान UI फ्रीज़ को रोकता है।
* **सिग्नल-स्लॉट संचार:** वर्कर्स टाइप्ड सिग्नल (जैसे, `price_updated`, `error_occurred`, `cycle_completed`) उत्सर्जित करते हैं जिन्हें मुख्य UI थ्रेड Qt के थ्रेड-सेफ स्लॉट तंत्र के माध्यम से उपभोग करता है।
* **ग्रेसफुल शटडाउन:** सभी वर्कर थ्रेड एक `stop()` सिग्नल का जवाब देते हैं, क्लीन टर्मिनेशन से पहले अपना वर्तमान चक्र पूरा करते हैं।

#### 💡 कार्यान्वयन अवधारणा (वर्कर थ्रेड मॉडल)
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

### 7. प्लेटफ़ॉर्म एडाप्टर पैटर्न (Binance ↔ Bybit)
* **एकीकृत इंटरफ़ेस:** एक सामान्य एडाप्टर एब्स्ट्रैक्शन Binance और Bybit के बीच API अंतरों को सामान्य करता है, जिससे कोर बिडिंग इंजन प्लेटफ़ॉर्म-अज्ञेयवादी रूप से संचालित हो सकता है।
* **Bybit विशेषताएँ संभालना:** Bybit को मूल्य संपादन स्वीकार करने से पहले विज्ञापन ऑनलाइन होना आवश्यक है; इसकी न्यूनतम फंडिंग थ्रेशोल्ड ~5 USDT है (बनाम Binance की 100 USDT)। एडाप्टर इन बाधाओं को पारदर्शी रूप से संभालता है।
* **फैक्ट्री पैटर्न:** एक एकल `create()` कॉल उपयोगकर्ता चयन के आधार पर सही प्लेटफ़ॉर्म एडाप्टर लौटाता है।

#### 💡 कार्यान्वयन अवधारणा (प्लेटफ़ॉर्म एडाप्टर फैक्ट्री)
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

## 🏗️ सिस्टम आर्किटेक्चर

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

## ⚙️ तकनीकी विनिर्देश और अंतर्निहित तंत्र
सिस्टम संसाधन दक्षता और विश्वसनीय दीर्घकालिक स्वचालित निष्पादन के लिए अनुकूलित। आंतरिक थ्रेड मॉडल API प्रतिबंधों को रोकने और थ्रूपुट अधिकतम करने के लिए कठोर निष्पादन चक्रों का उपयोग करता है:

| घटक | अंतराल | तकनीकी विवरण |
|---|---|---|
| **समानांतर विज्ञापन पोलिंग** | 3000 ms | मास्टर इंजन सक्रिय विज्ञापन कतार को क्वेरी और ऑडिट करता है। स्थिरांक: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **बिडिंग नेटवर्क स्कैनर** | 2000 ms | गहन क्वेरी प्रतिस्पर्धी मूल्य परिवर्तनों को इंटरसेप्ट करती है। स्थिरांक: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **इनपुट डीबाउंस थ्रेशोल्ड** | 1500 ms | मैन्युअल ट्यूनिंग के दौरान API स्पैम फ़िल्टर करता है। स्थिरांक: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **जोखिम सर्किट ब्रेकर** | 300,000 ms | API रेट-लिमिट ट्रिगर पर वैश्विक सुरक्षा विराम। प्रति-पंक्ति और वैश्विक दोनों स्कोप |
| **बल्क टॉगल स्पेसिंग** | 500 ms | बैच स्थिति परिवर्तनों के बीच रेट-लिमिट स्पेसिंग |
| **स्पॉट प्राइस सिंक** | 2000 ms | अस्थिर संपत्तियों के लिए रियल-टाइम एक्सचेंज स्पॉट मूल्य ग्रहण |

### सुरक्षा दर सीमित आर्किटेक्चर
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

### API प्रमाणीकरण और अनुरोध हस्ताक्षर
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

## 🇮🇳 क्षेत्रीय अनुकूलन: भारत

`binance_p2p_bot` भारतीय P2P बाजार के लिए पूर्ण रूप से अनुकूलित है, जिसमें **INR (भारतीय रुपया)** का मूल समर्थन शामिल है।

### समर्थित भुगतान विधियाँ
* **UPI (Unified Payments Interface)** — भारत में सबसे प्रमुख भुगतान विधि, 24/7 तत्काल ट्रांसफर
* **PhonePe, Google Pay (GPay), Paytm** — सबसे लोकप्रिय UPI ऐप्स
* **IMPS** — तत्काल अंतर-बैंक मोबाइल भुगतान
* **NEFT / RTGS** — बड़े लेनदेन के लिए बैंक ट्रांसफर

### बाज़ार आवश्यकताएँ और उपयोग परिदृश्य
भारत विश्व स्तर पर **सबसे अधिक क्रिप्टो अपनाने वाला** देश है। UPI प्रमुख भुगतान विधि है जो तत्काल ट्रांसफर सक्षम करती है, जिससे P2P व्यापारियों के बीच भारी प्रतिस्पर्धा होती है। नियामक अनिश्चितता के कारण उपयोगकर्ता स्थानीय-निष्पादन उपकरणों (कोई बाहरी सर्वर नहीं) को महत्व देते हैं। भुगतान विधियाँ (UPI, बैंक ट्रांसफर आदि) एक्सचेंज में कॉन्फ़िगर की जाती हैं; बोट स्वतंत्र बिडिंग रणनीतियों के लिए विज्ञापनों को भुगतान प्रकार के अनुसार समूहित करता है।

#### 💡 कार्यान्वयन अवधारणा (भारत UPI और भुगतान अनुकूलन)
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

## 🌐 उद्योग मानक और पारिस्थितिकी तंत्र कीवर्ड
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `P2P बॉट इंडिया`, `क्रिप्टो आर्बिट्राज INR`, `USDT खरीदें बेचें`, `Binance P2P ऑटोमेशन इंडिया`, `UPI क्रिप्टो ट्रेडिंग`, `PhonePe USDT`, `ऑटोमेटेड P2P ट्रेडिंग इंडिया`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />

## 💡 अक्सर पूछे जाने वाले प्रश्न (Q&A)

**प्र: binance_p2p_bot क्या है और यह क्या करता है?**
उ: `binance_p2p_bot` Binance और Bybit P2P व्यापारियों के लिए एक पेशेवर-ग्रेड डेस्कटॉप ऑटोमेशन क्लाइंट है। यह स्पॉट मार्केट डेटा के आधार पर आपके विज्ञापन मूल्यों को स्वचालित रूप से समायोजित करता है, स्मार्ट बिडिंग के लिए प्रतिस्पर्धी स्थितियों को ट्रैक करता है, स्टेबलकॉइन विज्ञापनों को बल्क में प्रबंधित करता है, और विज्ञापन इन्वेंटरी की निगरानी करता है — यह सब आपकी स्थानीय मशीन से सीधे API कनेक्शन के माध्यम से।

**प्र: क्या binance_p2p_bot Binance/Bybit API सीमाओं को सुरक्षित रूप से संभालता है?**
उ: हाँ। 3-स्तरीय सुरक्षा प्रणाली के माध्यम से: (1) स्पैम फ़िल्टर करने के लिए 1500ms इनपुट डीबाउंस, (2) प्रति-विज्ञापन पंक्ति कूलडाउन, और (3) 300-सेकंड वैश्विक सर्किट ब्रेकर। बोट API वेट लिमिट का सख्ती से पालन करता है। सभी कनेक्शन सीधे और सुरक्षित रूप से आपके स्थानीय वातावरण से होते हैं (शून्य मध्यस्थ डेटा रिसाव)।

**प्र: कौन सी क्रिप्टोकरेंसी और फिएट गेटवे समर्थित हैं?**
उ: `binance_p2p_bot` Binance और Bybit P2P मार्केटप्लेस पर उपलब्ध सभी फिएट मुद्राओं और क्रिप्टो संपत्तियों के साथ काम करता है, जिसमें प्रमुख टोकन (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) और विविध फिएट गेटवे (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD, और अन्य) शामिल हैं। बोट स्वतंत्र बिडिंग रणनीतियों के लिए विज्ञापनों को उनकी कॉन्फ़िगर संपत्ति, फिएट, ट्रेड दिशा, और भुगतान प्रकार संयोजन के अनुसार समूहित करता है।

**प्र: स्मार्ट रैंक स्नाइपिंग एल्गोरिदम कैसे काम करता है?**
उ: बोट हर 2 सेकंड में P2P ऑर्डरबुक की निगरानी करता है। जब कोई प्रतिस्पर्धी अपनी कीमत बदलता है, तो एल्गोरिदम आपकी परिभाषित सुरक्षित सीमा (न्यूनतम/अधिकतम मूल्य सीमाओं) के भीतर एक इष्टतम काउंटर-प्राइस (जैसे, शीर्ष बोलीदाता से +$0.01 ऊपर) की गणना करता है। फिर यह एक्सचेंज API के माध्यम से आपके विज्ञापन को अपडेट करता है, यह सुनिश्चित करते हुए कि आप अपने लाभ मार्जिन से बाहर बोली लगाए बिना #1 स्थिति बनाए रखें।

**प्र: क्या binance_p2p_bot प्रतिबंधित नेटवर्क वातावरण में काम करता है?**
उ: बोट पूरी तरह से आपकी स्थानीय मशीन पर शून्य बाहरी सर्वर निर्भरता के साथ संचालित होता है। सभी API कनेक्शन आपके डिवाइस से सीधे Binance/Bybit सर्वर पर जाते हैं — कोई तृतीय-पक्ष रिले शामिल नहीं। जटिल नेटवर्क स्थितियों वाले क्षेत्रों में उपयोगकर्ताओं के लिए, OS स्तर पर मानक सिस्टम-स्तरीय प्रॉक्सी या VPN कॉन्फ़िगरेशन लागू किए जा सकते हैं।

**प्र: Binance और Bybit P2P बोट मोड के बीच क्या अंतर हैं?**
उ: `binance_p2p_bot` प्लेटफ़ॉर्म अंतरों को पारदर्शी रूप से संभालने के लिए प्लेटफ़ॉर्म एडाप्टर पैटर्न लागू करता है। Bybit को संपादन स्वीकार करने से पहले विज्ञापन ऑनलाइन होना आवश्यक है, और इसकी उपयोग योग्य फंडिंग थ्रेशोल्ड कम है (~5 USDT बनाम Binance की 100 USDT)। बोट मैन्युअल कॉन्फ़िगरेशन के बिना इन बाधाओं के अनुकूल स्वचालित रूप से हो जाता है।

**प्र: क्या बोट BTC और ETH जैसी अस्थिर संपत्तियों का समर्थन करता है?**
उ: हाँ। स्पॉट मार्केट सिंक सुविधा रियल-टाइम एक्सचेंज स्पॉट मूल्यों को ग्रहण करती है और उन्हें आपके पूर्वनिर्धारित अनुपात से गुणा करती है, मिलीसेकंड में P2P विज्ञापन मूल्यों को स्वचालित रूप से सही करती है। यह BTC, ETH, और SOL विज्ञापनों के लिए आवश्यक है जहाँ 1-सेकंड की देरी भी महत्वपूर्ण मार्जिन क्षरण का कारण बन सकती है।

**प्र: यदि मैं अपना कंप्यूटर पुनरारंभ करता हूँ, तो क्या मेरा कॉन्फ़िगरेशन खो जाएगा?**
उ: नहीं। `binance_p2p_bot` में पूर्ण स्वचालित JSON-आधारित स्टेट पर्सिस्टेंस है। सभी UI सेटिंग्स, लक्ष्य यूज़रनेम, गुणक, और सुरक्षित सीमा कॉन्फ़िगरेशन हर परिवर्तन पर लगातार स्थानीय JSON कैश में लिखे जाते हैं। पुनरारंभ पर, बोट स्वचालित रूप से आपका सटीक कॉन्फ़िगरेशन पुनर्स्थापित करता है।

**प्र: binance_p2p_bot किस तकनीकी स्टैक का उपयोग करता है?**
उ: बोट Python और PySide6 (Qt6) के साथ बनाया गया है, जो एक नेटिव डेस्कटॉप अनुभव प्रदान करता है। यह समवर्ती API पोलिंग के लिए QThread वर्कर्स, थ्रेड-सेफ UI अपडेट के लिए Signal/Slot पैटर्न, API प्रमाणीकरण के लिए HMAC-SHA256, और कॉन्फ़िगरेशन पर्सिस्टेंस के लिए JSON का उपयोग करता है। किसी बाहरी सर्वर, डेटाबेस, या क्लाउड सेवाओं की आवश्यकता नहीं है।

## 🇮🇳 भारत-विशिष्ट अक्सर पूछे जाने वाले प्रश्न

**प्र: क्या binance_p2p_bot INR और UPI के साथ काम करता है?**
उ: बोट मूल्य निर्धारण/बिडिंग प्रबंधित करता है। भुगतान विधियाँ (UPI, PhonePe, Google Pay, Paytm, IMPS, NEFT आदि) एक्सचेंज में कॉन्फ़िगर की जाती हैं। बोट स्वतंत्र बिडिंग रणनीतियों के लिए विज्ञापनों को भुगतान कॉन्फ़िगरेशन के अनुसार समूहित करता है।

## 🔗 आधिकारिक पारिस्थितिकी तंत्र और संपर्क
* **आधिकारिक होम और दस्तावेज़ीकरण:** [apip2p.top](https://apip2p.top/) *(नवीनतम अपडेट, उच्च-आवृत्ति रणनीतियाँ, और एल्गोरिदमिक ट्रेडिंग समाधान)*
* **GitHub रिपॉज़िटरी:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **डेवलपर Telegram:** [@eason01993](https://t.me/eason01993)
* **कम्युनिटी चैनल:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube मार्गदर्शन:** [Eason का YouTube चैनल](https://www.youtube.com/@eason01993)

## ⚠️ अस्वीकरण
`binance_p2p_bot` शैक्षिक और संरचनात्मक संदर्भ के लिए प्रदान किया गया है। क्रिप्टोकरेंसी ट्रेडिंग अत्यधिक अस्थिर है। अपनी API Keys को सुरक्षित रूप से संग्रहीत करें और स्वचालित टूलिंग को **कभी भी** "निकासी" अनुमतियाँ न दें। पूरी तरह अपने जोखिम पर उपयोग करें।
