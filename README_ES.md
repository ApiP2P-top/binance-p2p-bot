<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | [中文](README_CN.md) | **Español** | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: Bot Avanzado de Trading P2P Automatizado para Binance y Bybit
Trading P2P automatizado, arbitraje de criptomonedas y bot de pujas automáticas para comerciantes de Binance y Bybit.

# [Bot de Trading P2P (Binance & Bybit) Sitio Oficial](https://apip2p.top)

Descubre el software de automatización definitivo personalizado para comerciantes P2P. Optimiza tu eficiencia de trading, mantén una competitividad de precios constante y ejecuta [arbitraje cripto automatizado](https://apip2p.top/) de alta frecuencia sin interrupciones mediante `binance_p2p_bot`.

## 📝 Descripción General y Arquitectura
**binance_p2p_bot** es un cliente de escritorio de nivel profesional diseñado específicamente para **Comerciantes P2P (Anunciantes)** que operan en **Binance** y **Bybit**. Al pasar del monitoreo manual del mercado a la ejecución programática impulsada por API, este bot garantiza que mantengas ventajas de precio persistentes y una velocidad de procesamiento de órdenes inigualable. 

Basado en principios de sondeo automatizado eficiente y ejecución algorítmica, resuelve los retrasos del seguimiento manual, la fuga de ingresos hacia arbitrajistas y la agotadora "trampa de pantalla". 


---

## 🎬 Demostración en Vivo

<div align="center">

[![binance-p2p-bot Demo Video](https://img.youtube.com/vi/MNULxgf0e9s/maxresdefault.jpg)](https://www.youtube.com/watch?v=MNULxgf0e9s)

▶️ **Haz clic en la imagen de arriba para ver la demostración completa en YouTube**

*Mira el `binance-p2p-bot` en acción — pujas automáticas en tiempo real en los mercados P2P de Binance, Bybit y OKX.*

</div>

---

## 🚀 Funciones Principales (Algoritmo y Flujo de Trabajo)

### 1. Pujas Automáticas y Ajuste de Precios en Tiempo Real (Captura Inteligente de Posiciones)
* **Monitoreo de Competidores:** El motor de `binance_p2p_bot` rastrea las fluctuaciones de precios de los competidores en la lista de anuncios P2P en tiempo real.
* **Auto-Posicionamiento Algorítmico:** Ajusta dinámicamente el precio de tu anuncio basándose en estrategias de precisión (por ejemplo, mantener una ventaja de $0.01 sobre el mejor postor) para garantizar una colocación premium del anuncio.
* **Lógica Multi-Competidor Dirigida:** Introduce los nombres de usuario P2P de competidores específicos. El bot capturará algorítmicamente la posición óptima en el ranking y aplicará tu margen personalizado.
* **Protección de Rango Seguro:** Aplica techos y pisos de precios estrictos para bloquear transacciones no rentables durante volatilidad extrema de fiat/cripto, anclando tu "Límite Máximo/Mínimo de Precio".

#### 💡 Concepto de Implementación (Captura Inteligente)
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

### 2. Sincronización Rápida de Activos Volátiles y Gestión Masiva de Stablecoins
* **Sincronización en Vivo con el Mercado Spot:** Para activos de alta volatilidad (BTC, ETH, SOL), `binance_p2p_bot` ingiere precios spot en vivo del exchange y los multiplica por tu ratio predefinido, autocorrigiendo los precios de tus anuncios P2P en milisegundos.
* **Operaciones Masivas de Stablecoins:** Simplifica el inventario de USDT, USDC y FDUSD. Activa o desactiva docenas de anuncios de stablecoins simultáneamente a través de un panel unificado.

#### 💡 Concepto de Implementación (Sincronización Spot)
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

### 3. Soporte Nativo Multi-Plataforma
* Se integra perfectamente con los backends de API de comerciantes de **Binance** y **Bybit**. 
* Maneja la lógica nativa de cada plataforma de forma inteligente (por ejemplo, adaptándose dinámicamente a las restricciones de umbral de fondos utilizables específicas de Bybit).

### 4. Gestión del Ciclo de Vida del Anuncio y Monitoreo de Inventario
* Gestiona la publicación, pausa y transiciones de estado de los anuncios mediante llamadas directas a la API.
* **Monitoreo de Inventario:** A través de sondeo periódico de la API, el bot lee el inventario actual, los límites mínimos y los datos de saldo de tus anuncios. Cuando se detectan cambios, mantiene los parámetros del anuncio sincronizados, ayudando a mantener cantidades disponibles precisas en todos los listados activos.

#### 💡 Concepto de Implementación (Máquina de Estados del Anuncio)
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

### 5. Persistencia de Estado y Recuperación de Sesión
* **Configuración sin Pérdidas:** Todos los parámetros de la interfaz, nombres de usuario objetivo, multiplicadores, rangos seguros y configuraciones de grupos de pujas se escriben continuamente en un archivo JSON local.
* **Recuperación tras Fallo:** Al reiniciar, el bot lee el estado persistido y restaura todos los paneles a su configuración exacta previa al cierre — sin necesidad de reintroducción manual.
* **Auto-guardado en Cada Cambio:** Cada modificación de parámetro activa una escritura inmediata a disco, asegurando durabilidad en tiempo real.

#### 💡 Concepto de Implementación (Motor de Persistencia de Estado)
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

### 6. Concurrencia de Hilos y Arquitectura Basada en Eventos
* **Modelo de Trabajadores QThread:** Cada módulo operativo (Sincronización Spot, Escáner de Pujas, Gestor Masivo) se ejecuta en su propio `QThread` dedicado, previniendo bloqueos de la interfaz durante el sondeo intensivo de la API.
* **Comunicación Signal-Slot:** Los trabajadores emiten Señales tipadas (por ejemplo, `price_updated`, `error_occurred`, `cycle_completed`) que el hilo principal de la interfaz consume a través del mecanismo Slot seguro para hilos de Qt.
* **Apagado Gradual:** Todos los hilos de trabajo responden a una señal `stop()`, completando su ciclo actual antes de terminar limpiamente.

#### 💡 Concepto de Implementación (Modelo de Hilos de Trabajo)
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

### 7. Patrón Adaptador de Plataforma (Binance ↔ Bybit)
* **Interfaz Unificada:** Una abstracción de adaptador común normaliza las diferencias de API entre Binance y Bybit, permitiendo que el motor principal de pujas opere de forma agnóstica a la plataforma.
* **Manejo de Particularidades de Bybit:** Bybit requiere que los anuncios estén en línea antes de aceptar ediciones de precio; su umbral mínimo de fondos es ~5 USDT (frente a los 100 USDT de Binance). El adaptador maneja estas restricciones de forma transparente.
* **Patrón Factory:** Una sola llamada a `create()` devuelve el adaptador de plataforma correcto basándose en la selección del usuario.

#### 💡 Concepto de Implementación (Fábrica de Adaptadores de Plataforma)
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

## 🏗️ Arquitectura del Sistema

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

## ⚙️ Especificaciones Técnicas y Mecanismos Subyacentes
Optimizado para la eficiencia de recursos del sistema y la ejecución automatizada fiable a largo plazo. El modelo interno de hilos utiliza ciclos de ejecución rigurosos para prevenir prohibiciones de API y maximizar el rendimiento:

| Componente | Intervalo | Detalle Técnico |
|---|---|---|
| **Sondeo Paralelo de Anuncios** | 3000 ms | El motor principal consulta y audita la cola de anuncios activos. Constante: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **Escáner de Red de Pujas** | 2000 ms | Consultas profundas interceptan cambios de precios de competidores. Constante: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **Umbral de Antirrebote de Entrada** | 1500 ms | Filtra el spam de API durante el ajuste manual. Constante: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **Disyuntor de Control de Riesgos** | 300,000 ms | Pausa de seguridad global ante activación de límite de API. Alcance por fila y global |
| **Espaciado de Activación Masiva** | 500 ms | Espaciado de limitación de tasa entre cambios de estado por lotes |
| **Sincronización de Precio Spot** | 2000 ms | Ingestión de precios spot en tiempo real para activos volátiles |

### Arquitectura de Limitación de Tasa de Seguridad
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

### Autenticación de API y Firma de Solicitudes
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

## 🌎 Optimización Regional: América Latina

### Monedas Fiat Soportadas en LATAM
| Moneda | Código | País |
|--------|--------|------|
| Peso Argentino | ARS | Argentina |
| Bolívar Venezolano | VES | Venezuela |
| Peso Colombiano | COP | Colombia |
| Peso Mexicano | MXN | México |
| Real Brasileño | BRL | Brasil |
| Sol Peruano | PEN | Perú |
| Peso Chileno | CLP | Chile |

### Métodos de Pago Locales Integrados
Los anuncios P2P en Latinoamérica suelen utilizar los siguientes métodos de pago (configurados al crear el anuncio en el exchange). El bot agrupa tus anuncios por tipo de pago para estrategias de puja independientes:
- **Argentina:** Mercado Pago, Ualá, Transferencia Bancaria
- **México:** SPEI, Mercado Pago, OXXO
- **Brasil:** PIX, Banco do Brasil, Nubank
- **Colombia:** Nequi, Bancolombia, Daviplata
- **Venezuela:** Zinli, Banesco, Pago Móvil

### Necesidades del Mercado y Escenarios de Uso en LATAM
- **Controles de capital** en Argentina y Venezuela hacen que el acceso directo a exchanges sea limitado — P2P es frecuentemente la **única rampa de entrada** al ecosistema cripto.
- **La hiperinflación** en economías como Argentina y Venezuela convierte a USDT en una herramienta esencial de preservación de valor.
- Los spreads P2P en mercados LATAM tienden a ser más amplios, generando **oportunidades de arbitraje significativas** para comerciantes automatizados.

#### 💡 Concepto de Implementación (Arquitectura de Puja Multi-Grupo)
```python
# [Pseudocode] Zona de Puja — Agrupa anuncios por (activo, dirección, fiat, tipo_pago)
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

## 🌐 Estándar de la Industria y Palabras Clave del Ecosistema
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `bot P2P Argentina`, `arbitraje USDT Venezuela`, `Binance P2P México`, `comprar USDT Colombia`, `bot trading P2P Latinoamérica`, `Mercado Pago crypto`, `PIX USDT Brasil`.

<img width="1290" height="850" alt="BTC1" src="https://github.com/user-attachments/assets/a6739a38-db8b-4eed-98ea-19875a5980cf" />


## 💡 Preguntas Frecuentes (Q&A)

**P: ¿Qué es binance_p2p_bot y qué hace?**
R: `binance_p2p_bot` es un cliente de automatización de escritorio de nivel profesional para comerciantes P2P de Binance y Bybit. Ajusta automáticamente los precios de tus anuncios basándose en datos del mercado spot, rastrea posiciones de competidores para pujas inteligentes, gestiona anuncios de stablecoins en masa y monitorea el inventario de anuncios — todo mediante conexiones API directas desde tu máquina local.

**P: ¿binance_p2p_bot maneja los límites de API de Binance/Bybit de forma segura?**
R: Sí. Mediante un sistema de protección de 3 capas: (1) antirrebote de entrada de 1500 ms para filtrar spam, (2) enfriamiento por fila de anuncio, y (3) un disyuntor global de 300 segundos. El bot cumple estrictamente con los límites de peso de API. Todas las conexiones se realizan directa y seguramente desde tu entorno local con cero filtraciones de datos por intermediarios.

**P: ¿Qué criptomonedas y pasarelas fiduciarias son compatibles?**
R: `binance_p2p_bot` funciona con todas las monedas fiduciarias y criptoactivos disponibles en los mercados P2P de Binance y Bybit, incluyendo los principales tokens (BTC, ETH, SOL, BNB, USDT, USDC, FDUSD) y diversas pasarelas fiat (ARS, VES, RUB, INR, IDR, VND, TRY, THB, PKR, EUR, USD, y más). El bot agrupa tus anuncios por activo, moneda fiat, dirección de trading y combinación de métodos de pago configurados, permitiendo estrategias de puja independientes por grupo.

**P: ¿Cómo funciona el algoritmo de Captura Inteligente de Posiciones?**
R: El bot monitorea el libro de órdenes P2P cada 2 segundos. Cuando un competidor cambia su precio, el algoritmo calcula un contra-precio óptimo (por ejemplo, +$0.01 por encima del mejor postor) dentro de tu rango seguro definido (límites de precio mín/máx). Luego actualiza tu anuncio a través de la API del exchange, asegurando que mantengas la posición #1 sin pujar fuera de tus márgenes de ganancia.

**P: ¿binance_p2p_bot funciona en entornos de red restringidos?**
R: El bot opera completamente en tu máquina local con cero dependencias de servidores externos. Todas las conexiones API van directamente desde tu dispositivo a los servidores de Binance/Bybit — sin intermediarios de terceros. Para usuarios en regiones con condiciones de red complejas, se pueden aplicar configuraciones estándar de proxy o VPN a nivel del sistema operativo.

**P: ¿Cuáles son las diferencias entre los modos de bot P2P de Binance y Bybit?**
R: `binance_p2p_bot` implementa un Patrón Adaptador de Plataforma para manejar las diferencias de plataforma de forma transparente. Bybit requiere que los anuncios estén en línea antes de aceptar ediciones, y tiene un umbral de fondos utilizables más bajo (~5 USDT frente a los 100 USDT de Binance). El bot se auto-adapta a estas restricciones sin configuración manual.

**P: ¿El bot soporta activos volátiles como BTC y ETH?**
R: Sí. La función de Sincronización con el Mercado Spot ingiere precios spot en tiempo real del exchange y los multiplica por tu ratio predefinido, autocorrigiendo los precios de anuncios P2P en milisegundos. Esto es esencial para anuncios de BTC, ETH y SOL donde incluso un retraso de 1 segundo puede causar una erosión significativa del margen.

**P: ¿Si reinicio mi computadora, perderé mi configuración?**
R: No. `binance_p2p_bot` cuenta con persistencia de estado automatizada basada en JSON. Todos los ajustes de la interfaz, nombres de usuario objetivo, multiplicadores y configuraciones de rango seguro se escriben continuamente en una caché JSON local con cada cambio. Al reiniciar, el bot restaura tu configuración exacta automáticamente.

**P: ¿Qué pila tecnológica utiliza binance_p2p_bot?**
R: El bot está construido con Python y PySide6 (Qt6), proporcionando una experiencia de escritorio nativa. Utiliza trabajadores QThread para sondeo concurrente de API, patrones Signal/Slot para actualizaciones de interfaz seguras entre hilos, HMAC-SHA256 para autenticación de API, y JSON para persistencia de configuración. No requiere servidores externos, bases de datos ni servicios en la nube.

## 🌎 Preguntas Frecuentes Regionales (LATAM)

**P: ¿binance_p2p_bot soporta el Peso Argentino (ARS) y el Bolívar Venezolano (VES)?**
R: Sí. `binance_p2p_bot` puede gestionar anuncios en ARS, VES, COP, MXN, BRL y cualquier moneda fiat listada en Binance/Bybit P2P. El bot aplica algoritmos de precio de precisión optimizados para spreads amplios comunes en los mercados argentino y venezolano. Los métodos de pago (Mercado Pago, PIX, SPEI, Nequi, etc.) se configuran al crear los anuncios en el exchange; el bot agrupa tus anuncios por estas configuraciones para aplicar estrategias de puja independientes por grupo.

## 🔗 Ecosistema Oficial y Contacto
* **Sitio Oficial y Documentación:** [apip2p.top](https://apip2p.top/) *(Últimas actualizaciones, estrategias de alta frecuencia y soluciones de trading algorítmico)*
* **Repositorio de GitHub:** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **Telegram del Desarrollador:** [@eason01993](https://t.me/eason01993)
* **Canal de la Comunidad:** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **Guía en YouTube:** [Canal de YouTube de Eason](https://www.youtube.com/@eason01993)

## ⚠️ Descargo de Responsabilidad
`binance_p2p_bot` se proporciona con fines educativos y de referencia estructural. El trading de criptomonedas es altamente volátil. Almacena tus API Keys de forma segura y **nunca** asignes permisos de "Retiro" a herramientas automatizadas. Úsalo completamente bajo tu propio riesgo.
