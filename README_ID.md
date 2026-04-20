<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | [Español](README_ES.md) | [Русский](README_RU.md) | **Bahasa Indonesia** | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: Bot Perdagangan P2P Otomatis Canggih untuk Binance & Bybit
Perdagangan P2P otomatis, arbitrase kripto, dan bot penawaran otomatis untuk merchant Binance dan Bybit.

# [Bot Perdagangan P2P (Binance & Bybit) Situs Resmi](https://apip2p.top)

Temukan perangkat lunak otomasi terbaik yang dirancang khusus untuk merchant P2P. Optimalkan efisiensi perdagangan Anda, pertahankan daya saing harga secara konstan, dan jalankan [arbitrase kripto otomatis](https://apip2p.top/) secara mulus melalui `binance_p2p_bot`.

## 📝 Gambaran Umum & Arsitektur
**binance_p2p_bot** adalah klien desktop kelas profesional yang dirancang khusus untuk **Merchant P2P (Pemasang Iklan)** yang beroperasi di **Binance** dan **Bybit**. Dengan beralih dari pemantauan pasar manual ke eksekusi terprogram berbasis API, bot ini memastikan Anda mempertahankan keunggulan harga yang persisten dan kecepatan pemrosesan pesanan yang tak tertandingi.

Dirancang dengan prinsip polling otomatis yang efisien dan eksekusi algoritmik, bot ini mengatasi keterlambatan pelacakan manual, kebocoran pendapatan ke arbitraser, dan "jebakan layar" yang melelahkan.


---

## 🎬 Demo Langsung

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **Klik gambar di atas untuk menonton demo lengkap di YouTube**

*Lihat `binance-p2p-bot` beraksi — auto-bidding real-time di pasar P2P Binance, Bybit, dan OKX.*

</div>

---

## 🚀 Fitur Utama (Algoritma & Alur Kerja)

### 1. Penawaran Otomatis & Penyesuaian Harga Real-time (Sniping Peringkat Cerdas)
* **Pemantauan Pesaing:** Mesin `binance_p2p_bot` melacak fluktuasi harga pesaing dalam daftar iklan P2P secara real-time.
* **Pemeringkatan Otomatis Algoritmis:** Menyesuaikan harga iklan Anda secara dinamis berdasarkan strategi presisi (misalnya, mempertahankan keunggulan $0,01 di atas penawar tertinggi) untuk menjamin penempatan iklan premium.
* **Logika Multi-Pesaing Bertarget:** Masukkan nama pengguna P2P pesaing tertentu. Bot akan secara algoritmis menembak slot peringkat optimal dan menerapkan markup kustom Anda.
* **Perlindungan Rentang Aman:** Memberlakukan batas harga atas dan bawah yang ketat untuk memblokir transaksi tidak menguntungkan selama volatilitas fiat/kripto ekstrem, mengunci "Batas Harga Maksimum/Minimum" Anda.

#### 💡 Konsep Implementasi (Sniping Cerdas)
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

### 2. Sinkronisasi Cepat Aset Volatil & Manajemen Massal Stablecoin
* **Sinkronisasi Pasar Spot Langsung:** Untuk aset dengan volatilitas tinggi (BTC, ETH, SOL), `binance_p2p_bot` menyerap harga spot bursa secara langsung dan mengalikannya dengan rasio yang telah Anda tentukan, mengoreksi harga iklan P2P Anda secara otomatis dalam hitungan milidetik.
* **Operasi Massal Stablecoin:** Menyederhanakan inventaris USDT, USDC, dan FDUSD. Aktifkan/nonaktifkan puluhan iklan stablecoin secara bersamaan melalui dasbor terpadu.

#### 💡 Konsep Implementasi (Sinkronisasi Spot)
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

### 3. Dukungan Multi-Platform Native
* Terintegrasi dengan mulus ke backend API merchant **Binance** dan **Bybit**.
* Menangani logika platform native secara cerdas (misalnya, menyesuaikan secara dinamis terhadap batasan ambang pendanaan yang dapat digunakan Bybit yang berbeda).

### 4. Manajemen Siklus Hidup Iklan & Pemantauan Inventaris
* Mengelola penerbitan iklan, penjedaan, dan transisi status melalui panggilan API langsung.
* **Pemantauan Inventaris:** Melalui polling API berkala, bot membaca inventaris iklan Anda saat ini, batas minimum, dan data saldo. Ketika perubahan terdeteksi, bot menjaga parameter iklan Anda tetap tersinkronisasi, membantu mempertahankan kuantitas yang tersedia secara akurat di semua listing aktif.

#### 💡 Konsep Implementasi (Mesin Status Iklan)
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

### 5. Persistensi Status & Pemulihan Sesi
* **Konfigurasi Tanpa Kehilangan:** Semua parameter UI, nama pengguna target, pengali, rentang aman, dan konfigurasi grup penawaran secara terus-menerus ditulis ke file JSON lokal.
* **Pemulihan dari Crash:** Saat restart, bot membaca status yang disimpan dan memulihkan semua panel ke konfigurasi persis sebelum shutdown — tidak perlu input ulang manual.
* **Simpan Otomatis saat Berubah:** Setiap modifikasi parameter memicu penulisan langsung ke disk, memastikan durabilitas real-time.

#### 💡 Konsep Implementasi (Mesin Persistensi Status)
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

### 6. Konkurensi Thread & Arsitektur Berbasis Event
* **Model Worker QThread:** Setiap modul operasional (Sinkronisasi Spot, Scanner Penawaran, Manager Massal) berjalan di `QThread` khusus masing-masing, mencegah pembekuan UI selama polling API intensif.
* **Komunikasi Signal-Slot:** Worker memancarkan Signal yang diketik (misalnya, `price_updated`, `error_occurred`, `cycle_completed`) yang dikonsumsi thread UI utama melalui mekanisme Slot thread-safe Qt.
* **Shutdown Anggun:** Semua thread worker merespons sinyal `stop()`, menyelesaikan siklus saat ini sebelum berhenti dengan bersih.

#### 💡 Konsep Implementasi (Model Thread Worker)
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

### 7. Pola Adapter Platform (Binance ↔ Bybit)
* **Antarmuka Terpadu:** Abstraksi adapter umum menormalisasi perbedaan API antara Binance dan Bybit, memungkinkan mesin penawaran inti beroperasi secara platform-agnostik.
* **Penanganan Keunikan Bybit:** Bybit mengharuskan iklan online sebelum menerima edit harga; ambang pendanaan minimumnya ~5 USDT (vs. 100 USDT Binance). Adapter menangani batasan ini secara transparan.
* **Pola Factory:** Satu panggilan `create()` mengembalikan adapter platform yang benar berdasarkan pilihan pengguna.

#### 💡 Konsep Implementasi (Factory Adapter Platform)
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

## 🏗️ Arsitektur Sistem

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

## ⚙️ Spesifikasi Teknis & Mekanisme Dasar
Dioptimalkan untuk efisiensi sumber daya sistem dan eksekusi otomatis jangka panjang yang andal. Model thread internal menggunakan siklus eksekusi yang ketat untuk mencegah pemblokiran API dan memaksimalkan throughput:

| Komponen | Interval | Detail Teknis |
|---|---|---|
| **Polling Iklan Paralel** | 3000 ms | Mesin utama mengueri & mengaudit antrian iklan aktif. Konstanta: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **Pemindai Jaringan Penawaran** | 2000 ms | Kueri mendalam menangkap pergeseran harga pesaing. Konstanta: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **Ambang Debounce Input** | 1500 ms | Memfilter spam API selama penyesuaian manual. Konstanta: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **Pemutus Sirkuit Risiko** | 300.000 ms | Jeda keamanan global saat batas laju API terpicu. Cakupan per-baris dan global |
| **Jarak Toggle Massal** | 500 ms | Jarak pembatasan laju antar perubahan status batch |
| **Sinkronisasi Harga Spot** | 2000 ms | Penyerapan harga spot bursa real-time untuk aset volatil |

### Arsitektur Pembatasan Laju Keamanan
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

### Autentikasi API & Penandatanganan Permintaan
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

## 🇮🇩 Optimasi Regional: Indonesia

`binance_p2p_bot` dioptimalkan secara penuh untuk pasar **Indonesia (IDR - Rupiah Indonesia)**. Metode pembayaran dikonfigurasi saat membuat iklan di bursa; bot mengelompokkan iklan berdasarkan jenis pembayaran untuk strategi penawaran independen.

### 🏦 Bank & E-Wallet yang Didukung
- **Bank Utama:** BCA (Bank Central Asia), Mandiri, BNI, BRI, CIMB Niaga
- **E-Wallet:** GoPay, OVO, DANA, ShopeePay, QRIS

### 🎯 Tantangan Pasar IDR
Pasar P2P Indonesia sangat kompetitif dengan jumlah merchant yang sangat banyak, margin keuntungan yang ketat, dan kecepatan transfer antarbank yang bervariasi. E-wallet semakin populer sebagai metode pembayaran pilihan. Dalam kondisi ini, **auto-bidding menjadi sangat esensial** — pemindai 2 detik `binance_p2p_bot` menangkap perubahan pasar sebelum trader manual dapat bereaksi.

#### 💡 Konsep Implementasi (Arsitektur Penawaran Multi-Grup)
```python
# [Pseudocode] Zona Penawaran — Mengelompokkan iklan berdasarkan (aset, jenis_perdagangan, fiat, jenis_pembayaran)
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

## 🌐 Standar Industri & Kata Kunci Ekosistem
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `bot P2P Indonesia`, `arbitrase kripto IDR`, `jual beli USDT Rupiah`, `Binance P2P otomatis`, `bot trading P2P Indonesia`, `BCA USDT`, `GoPay crypto`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 Pertanyaan yang Sering Diajukan (FAQ)

**T: Apa itu binance_p2p_bot dan apa fungsinya?**
J: `binance_p2p_bot` adalah klien otomasi desktop kelas profesional untuk merchant P2P Binance dan Bybit. Bot ini secara otomatis menyesuaikan harga iklan Anda berdasarkan data pasar spot, melacak posisi pesaing untuk penawaran cerdas, mengelola iklan stablecoin secara massal, dan memantau inventaris iklan — semuanya melalui koneksi API langsung dari mesin lokal Anda.

**T: Apakah binance_p2p_bot menangani batas API Binance/Bybit dengan aman?**
J: Ya. Melalui sistem perlindungan 3 lapisan: (1) debounce input 1500ms untuk memfilter spam, (2) cooldown per-baris per-iklan, dan (3) pemutus sirkuit global 300 detik. Bot secara ketat mematuhi batas bobot API. Semua koneksi terjadi langsung dan aman dari lingkungan lokal Anda tanpa kebocoran data perantara.

**T: Mata uang kripto dan gateway fiat apa yang didukung?**
J: `binance_p2p_bot` bekerja dengan semua mata uang fiat dan aset kripto yang tersedia di pasar P2P Binance dan Bybit, termasuk token utama (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) dan beragam gateway fiat (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD, dan lainnya). Bot mengelompokkan iklan Anda berdasarkan kombinasi aset, fiat, arah perdagangan, dan jenis pembayaran yang dikonfigurasi untuk strategi penawaran independen per grup.

**T: Bagaimana cara kerja algoritma Sniping Peringkat Cerdas?**
J: Bot memantau orderbook P2P setiap 2 detik. Ketika pesaing mengubah harga mereka, algoritma menghitung harga konter optimal (misalnya, +$0,01 di atas penawar tertinggi) dalam rentang aman yang Anda tentukan (batas harga min/maks). Kemudian memperbarui iklan Anda melalui API bursa, memastikan Anda mempertahankan posisi #1 tanpa pernah menawar di luar margin keuntungan Anda.

**T: Apakah binance_p2p_bot berfungsi di lingkungan jaringan terbatas?**
J: Bot beroperasi sepenuhnya di mesin lokal Anda tanpa ketergantungan server eksternal. Semua koneksi API langsung dari perangkat Anda ke server Binance/Bybit — tidak ada relay pihak ketiga. Untuk pengguna di wilayah dengan kondisi jaringan kompleks, konfigurasi proxy atau VPN tingkat sistem standar dapat diterapkan di level OS.

**T: Apa perbedaan antara mode bot Binance dan Bybit P2P?**
J: `binance_p2p_bot` mengimplementasikan Pola Adapter Platform untuk menangani perbedaan platform secara transparan. Bybit mengharuskan iklan online sebelum menerima edit, dan memiliki ambang pendanaan minimum yang lebih rendah (~5 USDT vs. 100 USDT Binance). Bot menyesuaikan secara otomatis terhadap batasan ini tanpa konfigurasi manual.

**T: Apakah bot mendukung aset volatil seperti BTC dan ETH?**
J: Ya. Fitur Sinkronisasi Pasar Spot menyerap harga spot bursa real-time dan mengalikannya dengan rasio yang telah Anda tentukan, mengoreksi harga iklan P2P secara otomatis dalam hitungan milidetik. Ini sangat penting untuk iklan BTC, ETH, dan SOL di mana keterlambatan bahkan 1 detik dapat menyebabkan erosi margin yang signifikan.

**T: Jika saya restart komputer, apakah konfigurasi saya akan hilang?**
J: Tidak. `binance_p2p_bot` memiliki persistensi status berbasis JSON yang sepenuhnya otomatis. Semua pengaturan UI, nama pengguna target, pengali, dan konfigurasi rentang aman secara terus-menerus ditulis ke cache JSON lokal pada setiap perubahan. Saat restart, bot memulihkan konfigurasi Anda secara otomatis dengan tepat.

**T: Stack teknologi apa yang digunakan binance_p2p_bot?**
J: Bot ini dibangun dengan Python dan PySide6 (Qt6), memberikan pengalaman desktop native. Menggunakan worker QThread untuk polling API konkuren, pola Signal/Slot untuk pembaruan UI thread-safe, HMAC-SHA256 untuk autentikasi API, dan JSON untuk persistensi konfigurasi. Tidak diperlukan server eksternal, database, atau layanan cloud.

### 🇮🇩 FAQ Regional: Indonesia

**T: Apakah binance_p2p_bot mendukung Rupiah Indonesia (IDR) dan metode pembayaran lokal?**
J: Ya. `binance_p2p_bot` sepenuhnya mendukung pasangan perdagangan IDR. Bot mengelola HARGA dan PENAWARAN untuk iklan Anda. Metode pembayaran (BCA, Mandiri, BNI, BRI, GoPay, OVO, DANA, QRIS) dikonfigurasi saat membuat iklan di bursa. Bot mengelompokkan iklan berdasarkan jenis pembayaran untuk menjalankan strategi penawaran independen.

## 🔗 Ekosistem Resmi & Kontak
* **Beranda & Dokumentasi Resmi:** [apip2p.top](https://apip2p.top/) *(Pembaruan terbaru, strategi frekuensi tinggi, dan solusi perdagangan algoritmis)*
* **Repositori GitHub:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Telegram Pengembang:** [@eason01993](https://t.me/eason01993)
* **Saluran Komunitas:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **Panduan YouTube:** [Channel YouTube Eason](https://www.youtube.com/@eason01993)

## ⚠️ Penafian
`binance_p2p_bot` disediakan untuk tujuan edukasi dan referensi struktural. Perdagangan mata uang kripto sangat volatil. Simpan API Keys Anda dengan aman dan **jangan pernah** memberikan izin "Penarikan" pada alat otomatis. Gunakan sepenuhnya atas risiko Anda sendiri.
