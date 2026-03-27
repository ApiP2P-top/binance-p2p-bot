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

## ⚙️ 技术规格与底层机制
针对系统资源效率和长时间稳定运行进行优化。内部线程模型采用严格的执行周期以防止 API 封禁并最大化吞吐量：

* **并行广告轮询（3000 ms）：** 主引擎每 3 秒查询和审计活跃广告队列。
* **竞价网络扫描器（2000 ms）：** 底层扫描器每 2 秒执行深度查询，即时拦截竞争对手的市场变化。
* **输入防抖阈值（1500 ms）：** 内置 1.5 秒防抖机制，在手动参数调整期间过滤无意义的 API 载荷垃圾。
* **安全频率限制与风控熔断：** 执行本地多任务锁队列。如果交易所全局 API 流量限制被触发，机器人将强制执行严格的 **300 秒风控熔断机制**，以保护账户状态并防止被列入黑名单。

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

**问：binance_p2p_bot 能安全处理 Binance/Bybit 的 API 限制吗？**
答：可以。通过输入防抖逻辑和 300 秒全局熔断机制，机器人严格遵守 API 权重限制。所有连接均直接从您的本地环境安全发起（零中间人数据泄露）。

**问：支持哪些加密货币和法币通道？**
答：`binance_p2p_bot` 可与 Binance 和 Bybit P2P 市场上所有可用的法币和加密资产配合使用，包括主流代币（BTC、ETH、SOL、BNB、USDT、USDC、FDUSD）及各种法币网关。机器人按照您广告配置的资产、法币、交易方向和支付方式组合进行分组，实现每组独立的竞价策略。

**问：binance_p2p_bot 支持人民币（CNY）及国内市场吗？**
答：是的。`binance_p2p_bot` 可以管理任何在 Binance/Bybit P2P 平台上创建的 CNY 广告。软件负责的是广告的定价、竞价和状态管理（自动改价、抢排名、批量上下架），支付方式（如支付宝、微信支付、银行卡转账等）由您在交易所平台创建广告时配置。机器人会根据广告的支付方式组合进行分组竞价，全本地运行架构保障数据安全。

## 🔗 官方生态与联系方式
* **官方主页与文档：** [apip2p.top](https://apip2p.top/) *（最新更新、高频策略和算法交易解决方案）*
* **GitHub 仓库：** [ApiP2P-top/binance-p2p-bot](https://github.com/ApiP2P-top/binance-p2p-bot)
* **开发者 Telegram：** [@eason01993](https://t.me/eason01993)
* **社区频道：** [t.me/eason01993_p2p](https://t.me/eason01993_p2p)
* **YouTube 教程：** [Eason 的 YouTube 频道](https://www.youtube.com/@eason01993)

## ⚠️ 免责声明
`binance_p2p_bot` 仅供教育和结构参考之用。加密货币交易具有高度波动性。请安全保管您的 API 密钥，**切勿**向自动化工具分配"提现"权限。使用风险完全由您自行承担。
