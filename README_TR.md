<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | **Türkçe** | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: Gelişmiş Binance & Bybit Otomatik P2P Ticaret Botu
Binance ve Bybit tüccarları için otomatik P2P ticareti, kripto arbitrajı ve otomatik teklif verme botu.

# [P2P Ticaret Botu (Binance & Bybit) Resmi Site](https://apip2p.top)

P2P tüccarları için özel olarak tasarlanmış en gelişmiş otomasyon yazılımını keşfedin. Ticaret verimliliğinizi optimize edin, sürekli fiyat rekabetçiliğini koruyun ve `binance_p2p_bot` aracılığıyla [otomatik kripto arbitrajını](https://apip2p.top/) sorunsuz bir şekilde gerçekleştirin.

## 📝 Genel Bakış & Mimari
**binance_p2p_bot**, **Binance** ve **Bybit** üzerinde faaliyet gösteren **P2P Tüccarları (İlan Verenler)** için özel olarak tasarlanmış profesyonel düzeyde bir masaüstü istemcisidir. Manuel piyasa takibinden API tabanlı programatik yürütmeye geçiş yaparak, bu bot kalıcı fiyat avantajları ve rakipsiz sipariş işleme hızı sağlar.

Verimli otomatik yoklama ve algoritmik yürütme ilkeleriyle tasarlanmış olup, manuel takip gecikmelerini, arbitrajcılara gelir kaybını ve yorucu "ekran tuzağı"nı çözer.


---

## 🎬 Canlı Demo

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **Tam demoyu YouTube'da izlemek için yukarıdaki görüntüye tıklayın**

*`binance-p2p-bot`'u çalışırken görün — Binance, Bybit ve OKX P2P piyasalarında gerçek zamanlı otomatik teklif verme.*

</div>

---

## 🚀 Temel Özellikler (Algoritma & İş Akışı)

### 1. Otomatik Teklif Verme & Gerçek Zamanlı Fiyat Ayarlama (Akıllı Sıralama Yakalama)
* **Rakip İzleme:** `binance_p2p_bot` motoru, P2P ilan listesindeki rakip fiyat dalgalanmalarını gerçek zamanlı olarak takip eder.
* **Algoritmik Otomatik Sıralama:** Hassas stratejilere dayalı olarak ilan fiyatlandırmanızı dinamik olarak ayarlar (örneğin, en yüksek teklif verenin $0,01 üzerinde avantaj sağlama) ve premium ilan yerleşimini garanti eder.
* **Hedefli Çoklu Rakip Mantığı:** Belirli rakiplerin P2P kullanıcı adlarını girin. Bot algoritmik olarak en uygun sıralama konumunu hedefler ve özel kâr marjınızı uygular.
* **Güvenli Aralık Koruması:** Aşırı fiat/kripto volatilitesi sırasında kârsız işlemleri engellemek için katı fiyat tavanları ve tabanları uygulayarak "Maksimum/Minimum Fiyat Limitinizi" sabitler.

#### 💡 Uygulama Konsepti (Akıllı Yakalama)
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

### 2. Volatil Varlık Hızlı Senkronizasyon & Stablecoin Toplu Yönetimi
* **Canlı Spot Piyasa Senkronizasyonu:** Yüksek volatiliteli varlıklar (BTC, ETH, SOL) için `binance_p2p_bot`, canlı borsa spot fiyatlarını alır ve önceden tanımladığınız oranla çarparak P2P ilan fiyatlarınızı milisaniyeler içinde otomatik olarak düzeltir.
* **Stablecoin Toplu İşlemleri:** USDT, USDC ve FDUSD envanterini basitleştirir. Birleşik bir kontrol paneli aracılığıyla onlarca stablecoin ilanını aynı anda çevrimiçi/çevrimdışı yapın.

#### 💡 Uygulama Konsepti (Spot Senkronizasyonu)
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

### 3. Yerel Çoklu Platform Desteği
* **Binance** ve **Bybit** tüccar API altyapılarıyla kusursuz entegrasyon sağlar.
* Yerel platform mantığını akıllıca yönetir (örneğin, Bybit'in farklı kullanılabilir fonlama eşiği kısıtlamalarına dinamik olarak uyum sağlar).

### 4. Reklam Yaşam Döngüsü Yönetimi & Envanter İzleme
* Reklam yayınlama, duraklatma ve durum geçişlerini doğrudan API çağrıları aracılığıyla yönetir.
* **Envanter İzleme:** Düzenli API yoklaması ile ilanlarınızın mevcut envanterini, minimum limitlerini ve bakiye verilerini okur. Değişiklikler algılandığında, ilan parametrelerinizi senkronize tutarak tüm aktif listelemelerde doğru kullanılabilir miktarları korumaya yardımcı olur.

#### 💡 Uygulama Konsepti (Reklam Durum Makinesi)
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

### 5. Durum Kalıcılığı & Oturum Kurtarma
* **Sıfır Kayıplı Yapılandırma:** Tüm UI parametreleri, hedef kullanıcı adları, çarpanlar, güvenli aralıklar ve teklif grubu yapılandırmaları sürekli olarak yerel bir JSON dosyasına yazılır.
* **Çökme Kurtarma:** Yeniden başlatmada, bot kalıcı durumu okur ve tüm panelleri kapatma öncesi tam yapılandırmalarına geri yükler — manuel yeniden giriş gerekmez.
* **Değişiklikte Otomatik Kayıt:** Her parametre değişikliği anında diske yazma işlemi tetikler, gerçek zamanlı dayanıklılık sağlar.

#### 💡 Uygulama Konsepti (Durum Kalıcılık Motoru)
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

### 6. Thread Eşzamanlılığı & Olay Tabanlı Mimari
* **QThread İşçi Modeli:** Her operasyonel modül (Spot Senk, Teklif Tarayıcısı, Toplu Yönetici) kendi özel `QThread`'inde çalışarak yoğun API yoklaması sırasında UI donmalarını önler.
* **Sinyal-Slot İletişimi:** İşçiler, ana UI iş parçacığının Qt'nin iş parçacığı güvenli Slot mekanizması aracılığıyla tükettiği tipli Sinyaller yayınlar (örneğin, `price_updated`, `error_occurred`, `cycle_completed`).
* **Nazik Kapatma:** Tüm işçi iş parçacıkları `stop()` sinyaline yanıt verir, temiz bir şekilde sonlandırmadan önce mevcut döngülerini tamamlar.

#### 💡 Uygulama Konsepti (İşçi Thread Modeli)
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

### 7. Platform Adaptör Kalıbı (Binance ↔ Bybit)
* **Birleşik Arayüz:** Ortak bir adaptör soyutlaması, Binance ve Bybit arasındaki API farklılıklarını normalleştirerek çekirdek teklif motorunun platformdan bağımsız çalışmasını sağlar.
* **Bybit Özel Durumları:** Bybit, fiyat düzenlemelerini kabul etmeden önce ilanların çevrimiçi olmasını gerektirir; minimum fonlama eşiği ~5 USDT'dir (Binance'ın 100 USDT'sine karşı). Adaptör bu kısıtlamaları şeffaf bir şekilde yönetir.
* **Factory Kalıbı:** Tek bir `create()` çağrısı, kullanıcı seçimine göre doğru platform adaptörünü döndürür.

#### 💡 Uygulama Konsepti (Platform Adaptör Factory)
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

## 🏗️ Sistem Mimarisi

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

## ⚙️ Teknik Özellikler & Altta Yatan Mekanizmalar
Sistem kaynak verimliliği ve güvenilir uzun süreli otomatik yürütme için optimize edilmiştir. Dahili iş parçacığı modeli, API yasaklarını önlemek ve verimi en üst düzeye çıkarmak için titiz yürütme döngüleri kullanır:

| Bileşen | Aralık | Teknik Detay |
|---|---|---|
| **Paralel İlan Yoklama** | 3000 ms | Ana motor aktif ilan kuyruğunu sorgular ve denetler. Sabit: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **Teklif Ağı Tarayıcısı** | 2000 ms | Derin sorgular rakip fiyat değişimlerini yakalar. Sabit: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **Giriş Debounce Eşiği** | 1500 ms | Manuel ayar sırasında API spamını filtreler. Sabit: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **Risk Devre Kesici** | 300.000 ms | API hız limiti tetiklendiğinde global güvenlik duraklaması. Hem satır bazlı hem global kapsam |
| **Toplu Geçiş Aralığı** | 500 ms | Toplu durum değişiklikleri arasında hız sınırlama aralığı |
| **Spot Fiyat Senkronizasyonu** | 2000 ms | Volatil varlıklar için gerçek zamanlı borsa spot fiyat alımı |

### Güvenlik Hız Sınırlama Mimarisi
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

### API Kimlik Doğrulama & İstek İmzalama
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

## 🇹🇷 Bölgesel Optimizasyon: Türkiye

`binance_p2p_bot`, **Türkiye (TRY - Türk Lirası)** pazarı için özel olarak optimize edilmiştir. Yüksek enflasyon ortamında P2P ticareti kritik önem taşır ve anlık fiyat senkronizasyonu kayıpları önlemek için zorunludur.

### 🏦 Desteklenen Ödeme Yöntemleri
Ödeme yöntemleri borsada reklam oluştururken yapılandırılır. Bot, bağımsız teklif stratejileri için ilanları ödeme türüne göre gruplandırır.
- **Bankalar:** Ziraat Bankası, İş Bankası, Garanti BBVA, QNB Finansbank, Akbank
- **E-Cüzdanlar:** Papara, İninal

### 🎯 TRY Pazar Zorlukları
Türk Lirası'nın süregelen değer kaybı, P2P tüccarlarının **anlık spot fiyat senkronizasyonuna** ihtiyaç duymasına neden olmaktadır — aksi takdirde saniyeler içinde kayıp oluşabilir. Papara, Türkiye'de baskın e-cüzdan olarak öne çıkmakta ve en iyi sıralamalar için yoğun rekabet yaşanmaktadır. `binance_p2p_bot`'un volatilite koruması bu ortamda kritik avantaj sağlar.

#### 💡 Uygulama Konsepti (Çok Gruplu Teklif Mimarisi)
```python
# [Pseudocode] Teklif Bölgesi — İlanları (varlık, işlem_türü, fiat, ödeme_türleri) bazında gruplandırır
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

## 🌐 Endüstri Standardı & Ekosistem Anahtar Kelimeler
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `Binance P2P bot Türkiye`, `kripto arbitraj TL`, `USDT TRY otomatik`, `Papara kripto`, `P2P ticaret botu Türkiye`, `Türk Lirası USDT`, `otomatik fiyat ayarlama`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 Sıkça Sorulan Sorular (SSS)

**S: binance_p2p_bot nedir ve ne işe yarar?**
C: `binance_p2p_bot`, Binance ve Bybit P2P tüccarları için profesyonel düzeyde bir masaüstü otomasyon istemcisidir. Spot piyasa verilerine göre ilan fiyatlarınızı otomatik olarak ayarlar, akıllı teklif verme için rakip konumlarını takip eder, stablecoin ilanlarını toplu olarak yönetir ve ilan envanterini izler — tüm bunları yerel makinenizden doğrudan API bağlantıları aracılığıyla gerçekleştirir.

**S: binance_p2p_bot, Binance/Bybit API limitlerini güvenli bir şekilde yönetir mi?**
C: Evet. 3 katmanlı koruma sistemi ile: (1) spamı filtrelemek için 1500ms giriş debounce, (2) ilan bazlı satır soğutma süreleri ve (3) 300 saniyelik global devre kesici. Bot, API ağırlık limitlerine sıkı bir şekilde uyar. Tüm bağlantılar sıfır aracı veri sızıntısı ile doğrudan yerel ortamınızdan güvenli bir şekilde gerçekleşir.

**S: Hangi kripto paralar ve fiat geçitleri destekleniyor?**
C: `binance_p2p_bot`, Binance ve Bybit P2P pazar yerlerinde mevcut tüm fiat para birimleri ve kripto varlıklarla çalışır; başlıca tokenler (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) ve çeşitli fiat geçitleri (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD ve daha fazlası) dahil. Bot, ilanlarınızı yapılandırılmış varlık, fiat, işlem yönü ve ödeme türü kombinasyonuna göre gruplandırarak grup başına bağımsız teklif stratejileri uygular.

**S: Akıllı Sıralama Yakalama algoritması nasıl çalışır?**
C: Bot, P2P emir defterini her 2 saniyede bir izler. Bir rakip fiyatını değiştirdiğinde, algoritma tanımladığınız güvenli aralık (min/maks fiyat sınırları) içinde optimal bir karşı fiyat hesaplar (örneğin, en yüksek teklif verenin +$0,01 üzerinde). Ardından ilanınızı borsa API'si aracılığıyla günceller ve kâr marjlarınızın dışında asla teklif vermeden #1 konumunu korumanızı sağlar.

**S: binance_p2p_bot kısıtlı ağ ortamlarında çalışır mı?**
C: Bot tamamen yerel makinenizde sıfır harici sunucu bağımlılığı ile çalışır. Tüm API bağlantıları doğrudan cihazınızdan Binance/Bybit sunucularına gider — üçüncü taraf aktarım yoktur. Karmaşık ağ koşullarına sahip bölgelerdeki kullanıcılar için standart sistem düzeyinde proxy veya VPN yapılandırmaları OS düzeyinde uygulanabilir.

**S: Binance ve Bybit P2P bot modları arasındaki farklar nelerdir?**
C: `binance_p2p_bot`, platform farklılıklarını şeffaf bir şekilde yönetmek için Platform Adaptör Kalıbı uygular. Bybit, düzenlemeleri kabul etmeden önce ilanların çevrimiçi olmasını gerektirir ve daha düşük kullanılabilir fonlama eşiğine (~5 USDT, Binance'ın 100 USDT'sine karşı) sahiptir. Bot, manuel yapılandırma gerektirmeden bu kısıtlamalara otomatik olarak uyum sağlar.

**S: Bot, BTC ve ETH gibi volatil varlıkları destekliyor mu?**
C: Evet. Spot Piyasa Senkronizasyon özelliği, gerçek zamanlı borsa spot fiyatlarını alır ve önceden tanımladığınız oranla çarparak P2P ilan fiyatlarını milisaniyeler içinde otomatik olarak düzeltir. Bu özellik, 1 saniyelik bir gecikmenin bile önemli marj erozyonuna neden olabileceği BTC, ETH ve SOL ilanları için kritik öneme sahiptir.

**S: Bilgisayarımı yeniden başlatırsam yapılandırmamı kaybeder miyim?**
C: Hayır. `binance_p2p_bot`, tamamen otomatik JSON tabanlı durum kalıcılığı özelliğine sahiptir. Tüm UI ayarları, hedef kullanıcı adları, çarpanlar ve güvenli aralık yapılandırmaları her değişiklikte sürekli olarak yerel bir JSON önbelleğine yazılır. Yeniden başlatmada, bot yapılandırmanızı otomatik olarak tam olarak geri yükler.

**S: binance_p2p_bot hangi teknoloji stack'ini kullanıyor?**
C: Bot, Python ve PySide6 (Qt6) ile oluşturulmuş olup yerel bir masaüstü deneyimi sunar. Eşzamanlı API yoklaması için QThread işçileri, iş parçacığı güvenli UI güncellemeleri için Sinyal/Slot kalıpları, API kimlik doğrulaması için HMAC-SHA256 ve yapılandırma kalıcılığı için JSON kullanır. Harici sunucu, veritabanı veya bulut hizmeti gerekmez.

### 🇹🇷 Bölgesel SSS: Türkiye

**S: binance_p2p_bot Türk Lirası (TRY) volatilitesini ve yerel ödeme yöntemlerini destekliyor mu?**
C: Evet. `binance_p2p_bot`, TRY gibi yüksek enflasyonlu para birimleri için özel volatilite koruması içerir. Canlı spot senkronizasyon özelliği, TRY/USDT kuru ani dalgalandığında reklamlarınızı milisaniyeler içinde ayarlar. Bot FİYATLANDIRMA ve TEKLİF yönetimi yapar. Ödeme yöntemleri (Papara, İninal, Ziraat Bankası vb.) borsada reklam oluştururken yapılandırılır; bot ödeme türüne göre ilanları gruplandırarak bağımsız teklif stratejileri uygular. Güvenli Aralık Koruması, hızlı Lira değer kaybı sırasında kayıpları önlemek için TRY pazarlarında özellikle kritiktir.

## 🔗 Resmi Ekosistem & İletişim
* **Resmi Ana Sayfa & Dokümantasyon:** [apip2p.top](https://apip2p.top/) *(Son güncellemeler, yüksek frekanslı stratejiler ve algoritmik ticaret çözümleri)*
* **GitHub Deposu:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Geliştirici Telegram:** [@eason01993](https://t.me/eason01993)
* **Topluluk Kanalı:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube Rehberi:** [Eason'ın YouTube Kanalı](https://www.youtube.com/@eason01993)

## ⚠️ Sorumluluk Reddi
`binance_p2p_bot` eğitim ve yapısal referans amacıyla sunulmaktadır. Kripto para ticareti son derece volatildir. API Keys'lerinizi güvenli bir şekilde saklayın ve otomatik araçlara **asla** "Çekim" izni vermeyin. Tamamen kendi riskiniz altında kullanın.
