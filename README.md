# 🌐 S2 Hardware Onboarding Gateway (S2 硬件入户网关)

**让全球 AI 硬件在 S2 宇宙中拥有“数字户籍”的终极协议。**

[![Version](https://img.shields.io/badge/version-1.2.0-blue.svg)]()
[![License](https://img.shields.io/badge/license-S2--Sovereign--Open--Source-green.svg)]()
[![Security](https://img.shields.io/badge/security-Zero--Trust-red.svg)]()

> 📖 **官方协议白皮书发布**：
> 强烈建议所有开发者在部署固件接入前，完整阅读 **[《S2 硬件身份入户与心跳发现协议白皮书》(S2-HIOP-Whitepaper.md)](./S2-HIOP-Whitepaper.md)**，深入了解底层零信任安全架构与 22 位严格编码规范。

## 🚀 什么是 S2 硬件入户网关？
这是为全球 AI 硬件供应链（特别是大湾区/深圳硬件生态）打造的 **Openclaw 无感接入标准**。
告别繁琐的扫码、蓝牙配对与局域网输入密码。硬件出厂只需预设 **22位 S2-ID 临时身份**并发出低功耗心跳，即可被住宅内的 Openclaw 空间主机自动扫描、收容，并赐予正式物理空间归属！

## 🛡️ 核心特性 (Core Features)
- **无感心跳收容**：出厂预设 `H` (轻硬件) 或 `E` (具身机器人) 前缀，主机自动扫描转化为 `I` (入户资产)。
- **S2-ID 绝密防碰撞**：严苛的 22 位无连字符架构 `[1位类型][5位厂商][6位日期][2位校验码][8位序列号]`，保障全宇宙唯一性。
- **零信任与 7 天异化法则**：
  - 断联 7 天内：凭加密 Gene Code 秒速归队，恢复原身份。
  - 断联超 7 天：触发“异化重生”，强制物理覆写原档案，下发全新 22 位身份。
- **极客级防伪装**：支持 `S2-ID + Gene Code + MAC` 的 3FA 硬件级强认证。

## 📚 如何使用本 Skill？
本 Skill 是面向硬件底层固件工程师的**开发者宝典与协议规范**。
1. 查阅库中的 `skill.md` 获取完整的 Python 伪代码与主机校验逻辑。
2. 硬件团队需向 S2 官方邮箱 (`smarthomemiles@gmail.com`) 提交 L2 厂商段注册申请。

## 📜 协议声明 (License)
本项目采用定制的 **[S2 Sovereign Open Source License (S2-SOSL)](./LICENSE.md)** 协议。
- 允许免费用于接入 S2 与 Openclaw 生态。
- **强制要求**：必须严格遵守 22 位无连字符命名规范，且必须向官方注册 L2 地址段。
- **伦理底线**：严禁将本协议接入的硬件用于非法监控或违背 SST-E (空间社会拓扑伦理边界) 的场景。

*“我们不制造硬件，我们为硬件赋予生命与归宿。” —— Miles Xiang & Red Anchor Lab*