<div align="center">

**🌐 Select Language / 选择语言**

[English](README.md) | **中文** | [Español](README_ES.md) | [Русский](README_RU.md) | [Bahasa Indonesia](README_ID.md) | [Türkçe](README_TR.md) | [Tiếng Việt](README_VN.md) | [ภาษาไทย](README_TH.md) | [हिन्दी](README_HI.md) | [اردو](README_UR.md)

</div>

# binance_p2p_bot: 高级 Binance & Bybit 自动化 P2P 交易机器人
面向 Binance 和 Bybit 商户的自动化 P2P 交易、加密货币套利和自动竞价机器人。

# [P2P 交易机器人 (Binance & Bybit) 官方网站](https://apip2p.top)

发现专为 P2P 商户定制的终极自动化软件。通过 `binance_p2p_bot` 优化您的交易效率、保持持续的价格竞争力，并无缝执行高频[自动化加密货币套利](https://apip2p.top/)。

## 📝 概述与架构
**binance_p2p_bot** 是一款专为在 **Binance** 和 **Bybit** 上运营的 **P2P 商户（广告商）** 量身打造的专业级桌面客户端。通过从手动市场监控转向 API 驱动的程序化执行，该机器人确保您始终保持价格优势和无与伦比的订单处理速度。

基于高效自动化轮询和算法化执行原理设计，解决了手动跟踪延迟、收益被套利者侵蚀以及令人精疲力竭的“盯盘陷阱”等问题。

## 🚀 核心功能（算法与工作流程）

### 1. 自动竞价与实时价格调整（智能抢排名）
* **竞争对手监控：** `binance_p2p_bot` 引擎实时追踪 P2P 广告列表中竞争对手的价格波动。
* **算法自动排名：** 基于精确策略动态调整广告定价（例如，保持比最高出价者高 $0.01 的优势），确保广告处于优先展示位。
* **多竞争对手定向逻辑：** 输入指定竞争对手的 P2P 用户名，机器人将通过算法抢占最优排名位置，并应用您的自定义加价幅度。
* **安全范围保护：** 强制执行严格的价格上限和下限，在法币/加密货币剧烈波动期间阻止亏损交易，锚定您的"最高/最低价格限制"。

#### 💡 实现概念（智能抢排名）
```python
# [伪代码示例] 自动排名机制
async def snipe_top_position(ad_id, target_merchant, offset_amount=0.01, min_price=1.00):
    # Fetch real-time ladder data
    orderbook = await p2p_api.get_competitor_ladder(target_merchant)
    
    # Calculate absolute supremacy price
    new_competitive_price = orderbook.top_price + offset_amount
    
    # Execute within strict risk boundaries
    if new_competitive_price >= min_price:
        await p2p_api.update_ad(ad_id, new_competitive_price)
```

### 2. 波动资产快速同步与稳定币批量管理
* **实时现货市场同步：** 对于高波动性资产（BTC、ETH、SOL），`binance_p2p_bot` 实时获取交易所现货价格，并乘以您预设的比例，在毫秒内自动校正您的 P2P 广告价格。
* **稳定币批量操作：** 简化 USDT、USDC 和 FDUSD 库存管理。通过统一面板同时上线/下线数十个稳定币广告。

#### 💡 实现概念（现货同步）
```javascript
// [伪代码示例] P2P 广告与现货价格自动同步
async function runSpotMarketSync(symbol, your_multiplier) {
    // 1. Fetch real-time spot price
    const spotData = await exchange.api.fetchSpotTicker(symbol); // e.g., "BTC/USDT"
    
    // 2. Compute dynamic markup value
    const p2pTargetPrice = spotData.lastPrice * your_multiplier;
    
    // 3. Throttle and broadcast new prices safely
    await p2pManager.debounceUpdateAdsPrice(symbol, p2pTargetPrice);
}
```

### 3. 原生多平台支持
* 与 **Binance** 和 **Bybit** 商户 API 后端无缝集成。
* 智能处理各平台原生逻辑差异（例如，动态适配 Bybit 独特的可用资金阈值限制）。

### 4. 广告生命周期管理与库存监控
* 通过直接 API 调用管理广告的发布、暂停和状态转换。
* **库存监控：** 通过定期 API 轮询，机器人读取您广告的当前库存、最小限额和余额数据。当检测到变化时，保持广告参数同步，帮助您在所有活跃广告中维护准确的可用数量。

#### 💡 实现概念（广告状态机）
```python
# [伪代码] 广告生命周期状态机 — 管理 ONLINE/OFFLINE 状态转换
class AdLifecycleManager:
    VALID_STATES = ["OFFLINE", "ONLINE", "FROZEN"]
    
    async def transition_ad(self, ad_id: str, target_state: str):
        current = await self.api.get_ad_status(ad_id)
        if current == target_state:
            return  # 已在目标状态，无需操作
        
        if target_state == "ONLINE":
            await self.api.update_ad_status(ad_id, online=True)
        elif target_state == "OFFLINE":
            await self.api.update_ad_status(ad_id, online=False)
        
        self.state_cache[ad_id] = target_state
        logger.info(f"广告 {ad_id}: {current} → {target_state}")
    
    async def bulk_toggle(self, ad_ids: list, online: bool):
        """批量切换多个广告，带频率限制间隔"""
        for ad_id in ad_ids:
            target = "ONLINE" if online else "OFFLINE"
            await self.transition_ad(ad_id, target)
            await asyncio.sleep(0.5)  # 500ms 间隔防止 API 突发
```

### 5. 状态持久化与会话恢复
* **零丢失配置：** 所有 UI 参数、目标用户名、乘数、安全范围和竞价组配置持续写入本地 JSON 文件。
* **崩溃恢复：** 重启时，机器人读取持久化状态并将所有面板恢复到关闭前的精确配置 — 无需手动重新输入。
* **变更即保存：** 每次参数修改都会立即触发磁盘写入，确保实时持久性。

#### 💡 实现概念（状态持久化引擎）
```python
# [伪代码] 基于 JSON 的状态持久化 — 每次 UI 变更自动保存
import json, os, time

class StatePersistence:
    CONFIG_FILE = "bot_state.json"
    
    def save_state(self, ui_state: dict):
        """将完整 UI 状态序列化到磁盘"""
        data = {
            "api_keys_encrypted": ui_state.get("encrypted_keys"),
            "target_usernames": ui_state.get("targets", []),
            "multipliers": ui_state.get("multipliers", {}),
            "safe_ranges": ui_state.get("price_bounds", {}),
            "active_groups": ui_state.get("bidding_groups", {}),
            "exchange_platform": ui_state.get("platform", "binance"),
            "language": ui_state.get("language", "zh"),
            "last_saved": time.time()
        }
        with open(self.CONFIG_FILE, 'w', encoding='utf-8') as f:
            json.dump(data, f, indent=2, ensure_ascii=False)
    
    def load_state(self) -> dict:
        """从磁盘恢复状态，回退到默认配置"""
        if not os.path.exists(self.CONFIG_FILE):
            return self._default_config()
        with open(self.CONFIG_FILE, 'r', encoding='utf-8') as f:
            return json.load(f)
    
    def auto_save_on_change(self, field: str, value):
        """由 PySide6 Signal 在任意参数变更时触发"""
        state = self.load_state()
        state[field] = value
        state["last_saved"] = time.time()
        self.save_state(state)
```

### 6. 线程并发与事件驱动架构
* **QThread 工作线程模型：** 每个功能模块（现货同步、竞价扫描、批量管理）运行在独立的 `QThread` 中，防止密集 API 轮询导致 UI 冻结。
* **Signal-Slot 通信：** 工作线程发射类型化 Signal（如 `price_updated`、`error_occurred`、`cycle_completed`），主 UI 线程通过 Qt 的线程安全 Slot 机制消费。
* **优雅关闭：** 所有工作线程响应 `stop()` 信号，完成当前周期后干净退出。

#### 💡 实现概念（工作线程模型）
```python
# [伪代码] PySide6 QThread 工作线程 — 竞价扫描器的 Signal/Slot 模式
from PySide6.QtCore import QThread, Signal

class BiddingWorkerThread(QThread):
    # 类型化信号，用于线程安全的 UI 通信
    price_updated = Signal(str, float)      # (ad_id, new_price)
    error_occurred = Signal(str, str)        # (ad_id, error_message)
    cycle_completed = Signal(int)            # (cycle_count)
    
    def __init__(self, api_client, config):
        super().__init__()
        self._running = False
        self._api = api_client
        self._config = config
        self._scan_interval_ms = 2000  # 2 秒扫描周期
    
    def run(self):
        """主工作循环 — 在后台线程中执行"""
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
                self.msleep(300_000)  # 300 秒熔断
            
            self.msleep(self._scan_interval_ms)
    
    def stop(self):
        """优雅关闭 — 完成当前周期后退出"""
        self._running = False
```

### 7. 平台适配器模式（Binance ↔ Bybit）
* **统一接口：** 通用适配器抽象层规范化 Binance 和 Bybit 之间的 API 差异，使核心竞价引擎可以平台无关地运行。
* **Bybit 特殊处理：** Bybit 要求广告在线才能接受价格编辑；其最低资金阈值约 5 USDT（Binance 为 100 USDT）。适配器透明处理这些约束。
* **工厂模式：** 单次 `create()` 调用根据用户选择返回正确的平台适配器。

#### 💡 实现概念（平台适配器工厂）
```python
# [伪代码] 跨平台适配器工厂 — Binance & Bybit 统一接口
class PlatformAdapterFactory:
    @staticmethod
    def create(platform: str, api_key: str, api_secret: str):
        if platform == "binance":
            return BinanceP2PAdapter(api_key, api_secret)
        elif platform == "bybit":
            return BybitP2PAdapter(api_key, api_secret)
        raise ValueError(f"不支持的平台: {platform}")

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
    MIN_FUNDING_THRESHOLD = 5  # USDT (Binance 为 100)
    
    async def update_ad_price(self, item_id: str, price: float):
        """Bybit: 编辑价格前需要广告在线"""
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

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────────┐
│                       PySide6 桌面 UI                            │
│  ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌─────────────┐  │
│  │   波动资产   │ │  稳定币批量  │ │   竞价区    │ │   设置面板   │  │
│  │    Tab     │ │    Tab     │ │    Tab    │ │            │  │
│  └──────┬─────┘ └──────┬─────┘ └──────┬─────┘ └──────┬──────┘  │
│         │              │              │               │          │
│  ┌──────▼──────────────▼──────────────▼───────────────▼──────┐  │
│  │              Signal / Slot 事件总线                         │  │
│  └──────┬──────────────┬──────────────┬───────────────┬──────┘  │
│         │              │              │               │          │
│  ┌──────▼──────┐ ┌─────▼──────┐ ┌────▼───────┐ ┌────▼───────┐  │
│  │  现货同步    │ │  批量管理   │ │  竞价扫描   │ │   状态持久   │  │
│  │   Worker   │ │   Worker   │ │   Worker  │ │  化(JSON)  │  │
│  │ (3s 周期)  │ │  (按需)    │ │ (2s 周期) │ │            │  │
│  └──────┬──────┘ └──────┬─────┘ └──────┬─────┘ └────────────┘  │
│         │              │              │                          │
│  ┌──────▼──────────────▼──────────────▼──────────────────────┐  │
│  │           频率限制器 & 风控熔断器                              │  │
│  │  ┌──────────────┐ ┌───────────┐ ┌───────────────────────┐ │  │
│  │  │ 输入防抖      │ │ 行级锁    │ │ 全局 300s 熔断器       │ │  │
│  │  │  (1500 ms)   │ │ (per-ad)  │ │ (API 限制守卫)        │ │  │
│  │  └──────────────┘ └───────────┘ └───────────────────────┘ │  │
│  └──────────────────────────┬────────────────────────────────┘  │
└─────────────────────────────┼───────────────────────────────────┘
                              │
                 ┌────────────▼────────────────┐
                 │    平台适配器层               │
                 │  ┌──────────┐ ┌───────────┐ │
                 │  │ Binance  │ │   Bybit   │ │
                 │  │ C2C API  │ │  C2C API  │ │
                 │  └────┬─────┘ └─────┬─────┘ │
                 └───────┼─────────────┼───────┘
                         │             │
                ┌────────▼────┐ ┌──────▼──────┐
                │ Binance API │ │  Bybit API  │
                │   Server   │ │   Server    │
                └─────────────┘ └─────────────┘
```

---

## ⚙️ 技术规格与底层机制
针对系统资源效率和长时间稳定运行进行优化。内部线程模型采用严格的执行周期以防止 API 封禁并最大化吞吐量：

| 组件 | 时间间隔 | 技术细节 |
|---|---|---|
| **并行广告轮询** | 3000 ms | 主引擎查询并审计活跃广告队列。常量: `_AUTO_POLL_INTERVAL_MS = 3_000` |
| **竞价网络扫描器** | 2000 ms | 深度查询拦截竞争对手价格变化。常量: `_SPOT_SCAN_INTERVAL_S = 2.0` |
| **输入防抖阈值** | 1500 ms | 过滤手动调参期间的 API 垃圾请求。常量: `_PRICE_INPUT_DELAY_MS = 1_500` |
| **风控熔断器** | 300,000 ms | API 限制触发时的全局安全暂停。行级+全局双重范围 |
| **批量切换间隔** | 500 ms | 批量状态变更之间的频率限制间距 |
| **现货价格同步** | 2000 ms | 波动资产的实时交易所现货价格摄入 |

### 安全频率限制架构
```python
# [伪代码] 多层频率限制 & 风控熔断器
class RateLimitGuard:
    def __init__(self):
        self.row_cooldowns = {}        # 单广告冷却追踪
        self.global_breaker = False    # 全局熔断器状态
        self.breaker_duration = 300    # 300 秒安全暂停
        self.debounce_ms = 1500        # 输入防抖阈值
        self._last_input_time = {}
    
    def should_debounce(self, ad_id: str) -> bool:
        """第 0 层: 输入防抖 — 拒绝快速重复输入"""
        now = time.time() * 1000
        last = self._last_input_time.get(ad_id, 0)
        if now - last < self.debounce_ms:
            return True  # 间隔太短，跳过
        self._last_input_time[ad_id] = now
        return False
    
    async def execute_with_guard(self, ad_id: str, operation):
        # 第 1 层: 检查全局熔断器
        if self.global_breaker:
            raise CircuitBreakerActive("全局 300 秒冷却生效中")
        
        # 第 2 层: 检查单广告行级冷却
        if ad_id in self.row_cooldowns:
            remaining = self.row_cooldowns[ad_id] - time.time()
            raise RowCooldownActive(f"广告 {ad_id} 冷却中 ({remaining:.0f}s)")
        
        # 第 3 层: 带异常处理的执行
        try:
            result = await operation()
            return result
        except APIRateLimitError:
            self.row_cooldowns[ad_id] = time.time() + self.breaker_duration
            self.global_breaker = True
            logger.critical(f"API 频率限制 — 熔断器启动 {self.breaker_duration}s")
            await asyncio.sleep(self.breaker_duration)
            self.global_breaker = False
            del self.row_cooldowns[ad_id]
```

### API 认证与请求签名
```python
# [伪代码] HMAC-SHA256 请求签名 — 保障 API 通信安全
import hashlib, hmac, time, urllib.parse

class APIAuthenticator:
    def __init__(self, api_key: str, api_secret: str):
        self.api_key = api_key
        self.api_secret = api_secret.encode('utf-8')
    
    def sign_request(self, params: dict) -> dict:
        """为交易所 API 生成 HMAC-SHA256 签名"""
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

## 🌍 区域适配：大中华及东亚市场
`binance_p2p_bot` 适用于大中华地区及东亚市场的 P2P 广告管理。软件负责广告定价、竞价和状态管理，支付结算由交易所原生基础设施完成。以下为该地区常见的法币和平台支持的支付方式：

* **常见法币：** CNY（人民币）、HKD（港币）、TWD（新台币）、KRW（韩元）、JPY（日元）
* **平台支持的支付方式：** 支付宝、微信支付、银行卡转账、香港 FPS（转数快）、台湾银行转账等（具体方式在交易所创建广告时配置）
* **用户需求与应用场景：**
  - 大量 P2P 商户在亚太区竞争激烈，手动盯盘难以维持价格优势
  - `binance_p2p_bot` 的 2 秒扫描周期在手动交易者反应之前捕捉价格变化
  - 机器人按照广告配置的资产、法币、交易方向和支付方式组合进行分组竞价
  - 全本地运行架构，零外部服务器依赖，保障 API 密钥安全

#### 💡 实现概念（多组竞价架构）
```python
# [伪代码] 竞价区 — 按 (资产, 交易方向, 法币, 支付组合) 分组竞价
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

## 🌐 行业标准与生态关键词
`binance_p2p_bot`, `Binance merchant tools`, `crypto arbitrage bot`, `Bybit P2P bot`, `USDT automated trading`, `spot market sync`, `order tracking`, `API order workflow`, `P2P rank sniping`, `automated asset management`, `Cross-border P2P fiat automation`, `P2P 自动交易`, `加密货币套利机器人`, `USDT 自动买卖`, `Binance P2P 竞价`, `币安 P2P 机器人`, `数字货币 OTC 自动化`, `P2P 抢排名`, `自动化做市`.
*![3](https://github.com/user-attachments/assets/c275a696-b20f-4f96-9f27-b8085d18cd43)
![2](https://github.com/user-attachments/assets/6207b2c8-37c6-4b46-a56b-483aa63d7fa4)

## 💡 常见问题（Q&A）

**问：binance_p2p_bot 是什么？有什么功能？**
答：`binance_p2p_bot` 是一款专为 Binance 和 Bybit P2P 商户打造的专业级桌面自动化客户端。它能自动根据现货市场数据调整广告价格、追踪竞争对手位置进行智能竞价、批量管理稳定币广告、监控广告库存 — 所有操作均通过本地机器直连交易所 API 完成。

**问：binance_p2p_bot 能安全处理 Binance/Bybit 的 API 限制吗？**
答：可以。通过 3 层保护体系：(1) 1500ms 输入防抖过滤垃圾请求，(2) 单广告行级冷却，(3) 300 秒全局风控熔断器。机器人严格遵守 API 权重限制。所有连接均从本地环境直接安全发起，零中间人数据泄露。

**问：支持哪些加密货币和法币通道？**
答：`binance_p2p_bot` 可与 Binance 和 Bybit P2P 市场上所有可用的法币和加密资产配合使用，包括主流代币（BTC、ETH、SOL、BNB、USDT、USDC、FDUSD）及各种法币网关（ARS、VES、RUB、INR、IDR、VND、TRY、THB、PKR、EUR、USD 等）。机器人按照您广告配置的资产、法币、交易方向和支付方式组合进行分组，实现每组独立的竞价策略。

**问：智能抢排名算法是如何工作的？**
答：机器人每 2 秒监控 P2P 挂单簿。当竞争对手变更价格时，算法立即在您设定的安全范围（最高/最低价格边界）内计算最优反击价格（如比第一名高 $0.01）。然后通过交易所 API 更新您的广告，确保始终维持第一名位置且不超出利润边界。

**问：binance_p2p_bot 在网络受限环境下能工作吗？**
答：机器人完全在本地机器运行，零外部服务器依赖。所有 API 连接直接从您的设备发往 Binance/Bybit 服务器 — 无第三方中继。对于网络条件复杂的地区用户，可在操作系统层面配置标准系统代理或 VPN。

**问：Binance 和 Bybit P2P 模式有什么区别？**
答：`binance_p2p_bot` 实现了平台适配器模式以透明处理平台差异。例如：Bybit 要求广告在线后才能编辑，且可用资金阈值更低（~5 USDT，Binance 为 100 USDT）。机器人自动适配这些约束，无需手动配置。

**问：支持 BTC、ETH 等波动资产吗？**
答：支持。实时现货同步功能摄入交易所现货价格，乘以您预设的比例系数，在毫秒内自动校正 P2P 广告价格。对于 BTC、ETH、SOL 广告，即使 1 秒延迟也可能导致显著的利润侵蚀。

**问：重启电脑会丢失配置吗？**
答：不会。`binance_p2p_bot` 具有完全自动化的 JSON 状态持久化。所有 UI 设置、目标用户名、乘数和安全范围配置在每次变更时持续写入本地 JSON 缓存。重启后机器人自动恢复您的精确配置。

**问：binance_p2p_bot 使用什么技术栈？**
答：机器人基于 Python 和 PySide6（Qt6）构建，提供原生桌面体验。使用 QThread 工作线程实现并发 API 轮询，Signal/Slot 模式实现线程安全的 UI 更新，HMAC-SHA256 实现 API 认证，JSON 实现配置持久化。不需要任何外部服务器、数据库或云服务。

**问：binance_p2p_bot 支持人民币（CNY）及国内市场吗？**
答：是的。`binance_p2p_bot` 可以管理任何在 Binance/Bybit P2P 平台上创建的 CNY 广告。软件负责广告的定价、竞价和状态管理（自动改价、抢排名、批量上下架），支付方式（如支付宝、微信支付、银行卡转账等）由您在交易所平台创建广告时配置。机器人会根据广告的支付方式组合进行分组竞价，全本地运行架构保障数据安全。

## 🔗 官方生态与联系方式
* **官方主页与文档：** [apip2p.top](https://apip2p.top/) *（最新更新、高频策略和算法交易解决方案）*
* **GitHub 仓库：** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **开发者 Telegram：** [@eason01993](https://t.me/eason01993)
* **社区频道：** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube 教程：** [Eason 的 YouTube 频道](https://www.youtube.com/@eason01993)

## ⚠️ 免责声明
`binance_p2p_bot` 仅供教育和结构参考之用。加密货币交易具有高度波动性。请安全保管您的 API 密钥，**切勿**向自动化工具分配"提现"权限。使用风险完全由您自行承担。
