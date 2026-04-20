<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | **ภาษาไทย** | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: บอทซื้อขาย P2P อัตโนมัติขั้นสูงสำหรับ Binance & Bybit
ซื้อขาย P2P อัตโนมัติ, อาร์บิทราจคริปโต, และบอทประมูลอัตโนมัติสำหรับผู้ค้า Binance และ Bybit

# [บอทซื้อขาย P2P (Binance & Bybit) เว็บไซต์ทางการ](https://apip2p.top)

ค้นพบซอฟต์แวร์ระบบอัตโนมัติที่ปรับแต่งมาโดยเฉพาะสำหรับผู้ค้า P2P เพิ่มประสิทธิภาพการซื้อขาย รักษาความสามารถในการแข่งขันด้านราคาอย่างต่อเนื่อง และดำเนิน[อาร์บิทราจคริปโตอัตโนมัติ](https://apip2p.top/)ความถี่สูงได้อย่างราบรื่นผ่าน `binance_p2p_bot`

## 📝 ภาพรวม & สถาปัตยกรรม
**binance_p2p_bot** เป็นซอฟต์แวร์เดสก์ท็อประดับมืออาชีพที่ออกแบบมาโดยเฉพาะสำหรับ**ผู้ค้า P2P (ผู้ลงโฆษณา)** ที่ดำเนินงานบน **Binance** และ **Bybit** ด้วยการเปลี่ยนจากการติดตามตลาดด้วยตนเองไปสู่การดำเนินการเชิงโปรแกรมผ่าน API บอทนี้รับประกันว่าคุณจะรักษาข้อได้เปรียบด้านราคาอย่างต่อเนื่องและความเร็วในการประมวลผลคำสั่งซื้อที่ไม่มีใครเทียบได้

ออกแบบตามหลักการสำรวจอัตโนมัติที่มีประสิทธิภาพและการดำเนินการเชิงอัลกอริทึม แก้ปัญหาความล่าช้าในการติดตามด้วยตนเอง การรั่วไหลของรายได้ให้กับนักอาร์บิทราจ และ "กับดักหน้าจอ" ที่ทำให้เหนื่อยล้า


---

## 🎬 สาธิตการใช้งานจริง

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **คลิกที่รูปด้านบนเพื่อดูการสาธิตเต็มรูปแบบบน YouTube**

*ดู `binance-p2p-bot` ทำงานจริง — การประมูลอัตโนมัติแบบเรียลไทม์บนตลาด P2P ของ Binance, Bybit และ OKX*

</div>

---

## 🚀 คุณสมบัติหลัก (อัลกอริทึม & เวิร์กโฟลว์)

### 1. ประมูลอัตโนมัติ & ปรับราคาแบบเรียลไทม์ (การยิงจัดอันดับอัจฉริยะ)
* **การเฝ้าติดตามคู่แข่ง:** เอนจิน `binance_p2p_bot` ติดตามความผันผวนของราคาคู่แข่งในรายการโฆษณา P2P แบบเรียลไทม์
* **การจัดอันดับอัตโนมัติด้วยอัลกอริทึม:** ปรับราคาโฆษณาของคุณอย่างไดนามิกตามกลยุทธ์ที่แม่นยำ (เช่น รักษาข้อได้เปรียบ $0.01 เหนือผู้เสนอราคาสูงสุด) เพื่อรับประกันตำแหน่งโฆษณาระดับพรีเมียม
* **ลอจิกมัลติคู่แข่งแบบกำหนดเป้าหมาย:** ป้อนชื่อผู้ใช้ P2P เฉพาะของคู่แข่ง บอทจะใช้อัลกอริทึมยิงตำแหน่งจัดอันดับที่เหมาะสมที่สุดและใช้มาร์กอัปที่คุณกำหนดเอง
* **การป้องกันช่วงปลอดภัย:** บังคับใช้ราคาเพดานและราคาพื้นอย่างเคร่งครัดเพื่อบล็อกธุรกรรมที่ไม่ทำกำไรในช่วงที่ fiat/คริปโตผันผวนรุนแรง ยึดมั่นใน "ขีดจำกัดราคาสูงสุด/ต่ำสุด" ของคุณ

#### 💡 แนวคิดการนำไปใช้ (การยิงตำแหน่งอัจฉริยะ)
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

### 2. ซิงค์สินทรัพย์ผันผวนแบบเร็ว & จัดการ Stablecoin แบบเป็นชุด
* **ซิงค์ตลาด Spot แบบสด:** สำหรับสินทรัพย์ที่มีความผันผวนสูง (BTC, ETH, SOL) `binance_p2p_bot` รับราคา spot ของตลาดแบบเรียลไทม์และคูณกับอัตราส่วนที่คุณกำหนดไว้ล่วงหน้า แก้ไขราคาโฆษณา P2P ของคุณโดยอัตโนมัติภายในมิลลิวินาที
* **การดำเนินการ Stablecoin แบบเป็นชุด:** ลดความซับซ้อนในการจัดการสินค้าคงคลัง USDT, USDC และ FDUSD สลับโฆษณา stablecoin หลายสิบรายการออนไลน์/ออฟไลน์พร้อมกันผ่านแดชบอร์ดรวม

#### 💡 แนวคิดการนำไปใช้ (ซิงค์ Spot)
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

### 3. รองรับหลายแพลตฟอร์มแบบเนทีฟ
* ผสานรวมอย่างไร้รอยต่อกับ backend API ผู้ค้าของ **Binance** และ **Bybit**
* จัดการลอจิกแพลตฟอร์มเนทีฟอย่างชาญฉลาด (เช่น ปรับตัวอย่างไดนามิกตามข้อจำกัดขีดจำกัดเงินทุนที่ใช้ได้ของ Bybit)

### 4. การจัดการวงจรชีวิตโฆษณา & การติดตามสินค้าคงคลัง
* จัดการการเผยแพร่ หยุดชั่วคราว และการเปลี่ยนสถานะโฆษณาผ่านการเรียก API โดยตรง
* **การติดตามสินค้าคงคลัง:** ผ่านการสำรวจ API เป็นระยะ บอทอ่านข้อมูลสินค้าคงคลังปัจจุบัน ขีดจำกัดขั้นต่ำ และข้อมูลยอดคงเหลือ เมื่อตรวจพบการเปลี่ยนแปลง จะรักษาพารามิเตอร์โฆษณาให้ซิงโครไนซ์ ช่วยรักษาจำนวนที่พร้อมใช้งานอย่างถูกต้องในทุกรายการที่เปิดใช้งาน

#### 💡 แนวคิดการนำไปใช้ (เครื่องสถานะโฆษณา)
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

### 5. การเก็บรักษาสถานะ & การกู้คืนเซสชัน
* **การกำหนดค่าไม่สูญหาย:** พารามิเตอร์ UI ทั้งหมด, ชื่อผู้ใช้เป้าหมาย, ตัวคูณ, ช่วงปลอดภัย, และการกำหนดค่ากลุ่มการเสนอราคาจะถูกเขียนอย่างต่อเนื่องไปยังไฟล์ JSON ในเครื่อง
* **การกู้คืนหลังข้อขัดข้อง:** เมื่อรีสตาร์ท บอทจะอ่านสถานะที่บันทึกไว้และกู้คืนแผงทั้งหมดให้กลับสู่การกำหนดค่าที่แน่นอนก่อนปิดเครื่อง — ไม่ต้องป้อนข้อมูลใหม่ด้วยตนเอง
* **บันทึกอัตโนมัติเมื่อเปลี่ยนแปลง:** ทุกการแก้ไขพารามิเตอร์จะทริกเกอร์การเขียนลงดิสก์ทันที เพื่อรับประกันความทนทานแบบเรียลไทม์

#### 💡 แนวคิดการนำไปใช้ (เอนจินเก็บรักษาสถานะ)
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

### 6. การทำงานพร้อมกันแบบมัลติเธรด & สถาปัตยกรรมขับเคลื่อนด้วยเหตุการณ์
* **โมเดล QThread Worker:** แต่ละโมดูลการทำงาน (ซิงค์ Spot, สแกนเนอร์การเสนอราคา, ตัวจัดการแบบเป็นชุด) ทำงานใน `QThread` เฉพาะของตัวเอง ป้องกันไม่ให้ UI ค้างระหว่างการสำรวจ API อย่างเข้มข้น
* **การสื่อสาร Signal-Slot:** Worker ปล่อย Signal ที่มีชนิดข้อมูล (เช่น `price_updated`, `error_occurred`, `cycle_completed`) ที่เธรด UI หลักรับผ่านกลไก Slot ที่ปลอดภัยต่อเธรดของ Qt
* **การปิดระบบอย่างสุภาพ:** เธรด worker ทั้งหมดตอบสนองต่อสัญญาณ `stop()` ทำรอบปัจจุบันให้เสร็จก่อนจะยุติอย่างสะอาด

#### 💡 แนวคิดการนำไปใช้ (โมเดล Worker Thread)
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

### 7. รูปแบบ Platform Adapter (Binance ↔ Bybit)
* **อินเทอร์เฟซรวม:** ชั้น adapter นามธรรมร่วมทำให้ความแตกต่างของ API ระหว่าง Binance และ Bybit เป็นมาตรฐาน ช่วยให้เอนจินการเสนอราคาหลักทำงานโดยไม่ขึ้นกับแพลตฟอร์ม
* **การจัดการความเฉพาะของ Bybit:** Bybit ต้องการให้โฆษณาออนไลน์ก่อนจึงจะรับการแก้ไขราคาได้; เกณฑ์ขั้นต่ำของเงินทุนที่ใช้ได้คือ ~5 USDT (เปรียบเทียบกับ 100 USDT ของ Binance) Adapter จัดการข้อจำกัดเหล่านี้อย่างโปร่งใส
* **รูปแบบ Factory:** การเรียก `create()` เพียงครั้งเดียวจะส่งคืน adapter แพลตฟอร์มที่ถูกต้องตามการเลือกของผู้ใช้

#### 💡 แนวคิดการนำไปใช้ (Factory Adapter ข้ามแพลตฟอร์ม)
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

## 🏗️ สถาปัตยกรรมระบบ

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

## ⚙️ ข้อกำหนดทางเทคนิค & กลไกพื้นฐาน
เพิ่มประสิทธิภาพสำหรับประสิทธิภาพทรัพยากรระบบและการดำเนินการอัตโนมัติที่เสถียรในระยะยาว โมเดลเธรดภายในใช้รอบการดำเนินการที่เข้มงวดเพื่อป้องกันการถูกแบน API และเพิ่มปริมาณงานให้สูงสุด:

| ส่วนประกอบ | ช่วงเวลา | รายละเอียดทางเทคนิค |
|---|---|---|
| **การสำรวจโฆษณาแบบขนาน** | 3000 ms | เอนจินหลักสอบถาม & ตรวจสอบคิวโฆษณาที่เปิดใช้งาน ค่าคงที่: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **สแกนเนอร์เครือข่ายการประมูล** | 2000 ms | การสอบถามเชิงลึกสกัดกั้นการเปลี่ยนแปลงราคาคู่แข่ง ค่าคงที่: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **เกณฑ์ Debounce อินพุต** | 1500 ms | กรองสแปม API ระหว่างการปรับแต่งด้วยตนเอง ค่าคงที่: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **เซอร์กิตเบรกเกอร์ความเสี่ยง** | 300,000 ms | หยุดชั่วคราวเพื่อความปลอดภัยทั่วโลกเมื่อถูกจำกัด API ทั้งขอบเขตต่อแถวและทั่วโลก |
| **ระยะห่างการสลับแบบเป็นชุด** | 500 ms | ระยะห่างจำกัดอัตราระหว่างการเปลี่ยนสถานะแบบเป็นชุด |
| **ซิงค์ราคา Spot** | 2000 ms | รับราคา spot ของตลาดแบบเรียลไทม์สำหรับสินทรัพย์ผันผวน |

### สถาปัตยกรรมการจำกัดอัตราเพื่อความปลอดภัย
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

### การยืนยันตัวตน API & การเซ็นคำขอ
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

## 🇹🇭 การเพิ่มประสิทธิภาพภูมิภาค: ประเทศไทย

`binance_p2p_bot` ได้รับการปรับแต่งสำหรับตลาดคริปโตของประเทศไทยซึ่งมีการกำกับดูแลที่ชัดเจน ผู้ค้าให้ความสำคัญกับเครื่องมือที่เชื่อถือได้ PromptPay เป็นระบบการชำระเงินทันทีเริ่มต้น และการจัดการสเปรด USDT/THB มีความสำคัญอย่างยิ่ง

**รองรับ THB (บาทไทย) แบบเนทีฟ** — ผสานรวมกับธนาคารหลัก: **KBank (กสิกรไทย)**, **SCB (ไทยพาณิชย์)**, **Bangkok Bank (กรุงเทพ)**, **Krungthai Bank (กรุงไทย)** และช่องทางชำระเงิน: **PromptPay (พร้อมเพย์)**, **TrueMoney Wallet**

**ความต้องการของตลาดและสถานการณ์การใช้งาน:** วิธีการชำระเงิน (PromptPay, KBank, SCB ฯลฯ) ถูกกำหนดค่าบนตลาดแลกเปลี่ยนเมื่อสร้างโฆษณา บอทจัดกลุ่มโฆษณาตามประเภทการชำระเงินเพื่อใช้กลยุทธ์การเสนอราคาอิสระสำหรับแต่ละกลุ่ม

```python
# [Pseudocode] สถาปัตยกรรมการเสนอราคาหลายกลุ่ม — จัดกลุ่มโฆษณาตาม (สินทรัพย์, ทิศทาง, fiat, ประเภทการชำระเงิน)
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

## 🌐 มาตรฐานอุตสาหกรรม & คีย์เวิร์ดระบบนิเวศ
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `บอท P2P ไทย`, `ซื้อขาย USDT บาท`, `Binance P2P อัตโนมัติ`, `อาร์บิทราจคริปโต THB`, `PromptPay crypto`, `KBank USDT`, `เทรด P2P อัตโนมัติ ไทย`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 คำถามที่พบบ่อย (Q&A)

**ถ: binance_p2p_bot คืออะไรและทำอะไรได้บ้าง?**
ต: `binance_p2p_bot` เป็นซอฟต์แวร์เดสก์ท็อปอัตโนมัติระดับมืออาชีพสำหรับผู้ค้า P2P ของ Binance และ Bybit โดยจะปรับราคาโฆษณาของคุณโดยอัตโนมัติตามข้อมูลตลาด spot ติดตามตำแหน่งคู่แข่งเพื่อการเสนอราคาอัจฉริยะ จัดการโฆษณา stablecoin แบบเป็นชุด และตรวจสอบสินค้าคงคลังโฆษณา — ทั้งหมดผ่านการเชื่อมต่อ API โดยตรงจากเครื่องในระบบของคุณ

**ถ: binance_p2p_bot จัดการกับขีดจำกัด API ของ Binance/Bybit ได้อย่างปลอดภัยหรือไม่?**
ต: ได้ ผ่านระบบป้องกัน 3 ชั้น: (1) debounce อินพุต 1500ms เพื่อกรองสแปม, (2) cooldown ต่อแถวสำหรับแต่ละโฆษณา, และ (3) เซอร์กิตเบรกเกอร์ทั่วโลก 300 วินาที บอทปฏิบัติตามขีดจำกัดน้ำหนัก API อย่างเคร่งครัด การเชื่อมต่อทั้งหมดเกิดขึ้นโดยตรงและปลอดภัยจากสภาพแวดล้อมในเครื่องของคุณ — ไม่มีการรั่วไหลของข้อมูลผ่านตัวกลาง

**ถ: รองรับสกุลเงินดิจิทัลและช่องทางชำระเงิน fiat ใดบ้าง?**
ต: `binance_p2p_bot` ทำงานกับสกุลเงิน fiat และสินทรัพย์คริปโตทั้งหมดที่มีบนตลาด P2P ของ Binance และ Bybit รวมถึงโทเค็นหลัก (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) และช่องทาง fiat ที่หลากหลาย (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD และอื่นๆ) บอทจัดกลุ่มโฆษณาตามการกำหนดค่าสินทรัพย์, fiat, ทิศทางการซื้อขาย และประเภทการชำระเงิน สำหรับกลยุทธ์การเสนอราคาอิสระต่อกลุ่ม

**ถ: อัลกอริทึมการยิงจัดอันดับอัจฉริยะทำงานอย่างไร?**
ต: บอทตรวจสอบ orderbook P2P ทุก 2 วินาที เมื่อคู่แข่งเปลี่ยนราคา อัลกอริทึมจะคำนวณราคาตอบโต้ที่เหมาะสม (เช่น +$0.01 เหนือผู้เสนอราคาสูงสุด) ภายในช่วงปลอดภัยที่คุณกำหนด (ขอบเขตราคาต่ำสุด/สูงสุด) จากนั้นอัปเดตโฆษณาของคุณผ่าน API ของตลาด รับประกันว่าคุณจะรักษาตำแหน่ง #1 โดยไม่เคยเสนอราคาเกินขอบเขตกำไร

**ถ: binance_p2p_bot ทำงานในสภาพแวดล้อมเครือข่ายที่ถูกจำกัดได้หรือไม่?**
ต: บอททำงานบนเครื่องในระบบของคุณทั้งหมด — ไม่พึ่งพาเซิร์ฟเวอร์ภายนอก การเชื่อมต่อ API ทั้งหมดไปจากอุปกรณ์ของคุณไปยังเซิร์ฟเวอร์ Binance/Bybit โดยตรง — ไม่มีตัวกลางรีเลย์ สำหรับผู้ใช้ในภูมิภาคที่มีสภาพเครือข่ายซับซ้อน สามารถกำหนดค่า proxy หรือ VPN ระดับระบบมาตรฐานได้ที่ระดับ OS

**ถ: ความแตกต่างระหว่างโหมดบอท P2P ของ Binance และ Bybit คืออะไร?**
ต: `binance_p2p_bot` ใช้รูปแบบ Platform Adapter เพื่อจัดการความแตกต่างของแพลตฟอร์มอย่างโปร่งใส Bybit ต้องการให้โฆษณาออนไลน์ก่อนจึงจะรับการแก้ไขได้ และมีเกณฑ์ขั้นต่ำของเงินทุนที่ใช้ได้ต่ำกว่า (~5 USDT เทียบกับ 100 USDT ของ Binance) บอทปรับตัวตามข้อจำกัดเหล่านี้โดยอัตโนมัติ ไม่ต้องกำหนดค่าด้วยตนเอง

**ถ: บอทรองรับสินทรัพย์ผันผวนเช่น BTC และ ETH หรือไม่?**
ต: รองรับ คุณสมบัติซิงค์ตลาด Spot รับราคา spot ของตลาดแบบเรียลไทม์และคูณกับอัตราส่วนที่คุณกำหนดไว้ล่วงหน้า แก้ไขราคาโฆษณา P2P โดยอัตโนมัติภายในมิลลิวินาที นี่เป็นสิ่งจำเป็นสำหรับโฆษณา BTC, ETH และ SOL ที่แม้แต่ความล่าช้า 1 วินาทีก็อาจทำให้เกิดการสูญเสียอัตรากำไรอย่างมีนัยสำคัญ

**ถ: ถ้าฉันรีสตาร์ทคอมพิวเตอร์ จะสูญเสียการกำหนดค่าหรือไม่?**
ต: ไม่ `binance_p2p_bot` มีคุณสมบัติการเก็บรักษาสถานะแบบ JSON อัตโนมัติเต็มรูปแบบ การตั้งค่า UI ทั้งหมด ชื่อผู้ใช้เป้าหมาย ตัวคูณ และการกำหนดค่าช่วงปลอดภัยจะถูกเขียนลงแคช JSON ในเครื่องอย่างต่อเนื่องทุกครั้งที่เปลี่ยนแปลง เมื่อรีสตาร์ท บอทจะกู้คืนการกำหนดค่าที่แน่นอนของคุณโดยอัตโนมัติ

**ถ: binance_p2p_bot ใช้เทคโนโลยีอะไรบ้าง?**
ต: บอทสร้างด้วย Python และ PySide6 (Qt6) ให้ประสบการณ์เดสก์ท็อปแบบเนทีฟ ใช้ QThread worker สำหรับการสำรวจ API พร้อมกัน, รูปแบบ Signal/Slot สำหรับการอัปเดต UI ที่ปลอดภัยต่อเธรด, HMAC-SHA256 สำหรับการยืนยัน API และ JSON สำหรับการเก็บรักษาการกำหนดค่า ไม่ต้องการเซิร์ฟเวอร์ภายนอก ฐานข้อมูล หรือบริการคลาวด์

## 🇹🇭 คำถามที่พบบ่อยสำหรับภูมิภาคไทย

**ถ: binance_p2p_bot รองรับบาทไทย (THB) และวิธีการชำระเงินของไทยหรือไม่?**
ต: ใช่ `binance_p2p_bot` จัดการราคาและการเสนอราคาสำหรับโฆษณา P2P ที่ซื้อขายด้วย THB วิธีการชำระเงิน (PromptPay, KBank, SCB, Bangkok Bank, Krungthai) ถูกกำหนดค่าบนตลาดแลกเปลี่ยนเมื่อสร้างโฆษณา บอทจัดกลุ่มโฆษณาตามการกำหนดค่าการชำระเงินเพื่อใช้กลยุทธ์การเสนอราคาอิสระ

## 🔗 ระบบนิเวศทางการ & ช่องทางติดต่อ
* **หน้าแรก & เอกสารทางการ:** [apip2p.top](https://apip2p.top/) *(อัปเดตล่าสุด, กลยุทธ์ความถี่สูง, และโซลูชันการซื้อขายแบบอัลกอริทึม)*
* **คลัง GitHub:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Telegram นักพัฒนา:** [@eason01993](https://t.me/eason01993)
* **ช่องทางชุมชน:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **คำแนะนำ YouTube:** [ช่อง YouTube ของ Eason](https://www.youtube.com/@eason01993)

## ⚠️ ข้อจำกัดความรับผิดชอบ
`binance_p2p_bot` จัดทำขึ้นเพื่อวัตถุประสงค์ทางการศึกษาและเป็นข้อมูลอ้างอิงเชิงโครงสร้าง การซื้อขายสกุลเงินดิจิทัลมีความผันผวนสูง โปรดเก็บรักษา API Keys ของคุณอย่างปลอดภัยและ**อย่า**ให้สิทธิ์ "ถอนเงิน" แก่เครื่องมืออัตโนมัติ ใช้งานด้วยความเสี่ยงของคุณเองทั้งหมด
