```markdown
# S2 Hardware Identity Onboarding & Heartbeat Protocol Whitepaper

**Document ID:** S2-HIOP-2026-V1.3 (Zero-Knowledge Privacy Patched)
**Release Date:** March 29, 2026
**Published By:** Miles Xiang & RobotZero Software
**Target Audience:** AI Hardware Supply Chain, Firmware Engineers, Openclaw Developers

## 1. Vision: The "Digital Household Registration" for Hardware
As the global AI hardware supply chain pivots toward the Openclaw ecosystem, Space² (S2) introduces a standardized, seamless onboarding protocol. Hardware devices will emit a low-energy, zero-knowledge "heartbeat". Openclaw spatial agents will scan, securely handshake, and convert these devices, assigning them a Permanent Sovereign Identity.

## 2. The 22-Character S2-ID Nomenclature
To ensure global uniqueness, the system utilizes a strict 22-character alphanumeric string without hyphens.
* **Format**: `[L1][L2][Date][Checksum][Serial]` -> e.g., `HABCDE260329AA12345678`
* **L1 (1 char)**: H (Lightweight Smart Hardware), E (Embodied Robots), I (Integrated/Registered identity).
* **L2 (5 chars)**: A registered 5-letter manufacturer code.
* **Date (6 chars)**: YYMMDD format.
* **Checksum (2 letters)**: Placed strictly before the serial. Factory placeholder (AA) is recalculated into a secure hash (XX) upon registration.
* **Serial (8 chars)**: Personalized unique hardware digits.

## 3. The Onboarding Protocol
* **Factory Phase**: Device is flashed with a temporary ID.
* **Heartbeat Phase**: Device broadcasts a privacy-preserving Ephemeral Hash heartbeat (BLE/UDP). No persistent IDs are broadcasted in plaintext.
* **Adoption Phase**: The Openclaw Agent initiates a secure TLS handshake, invokes the S2-CheckSum algorithm, transitions the H/E prefix to I, and recalculates the placeholder.

## 4. The L2 Vendor Registry (Decentralized & Corporate Validated)
Vendors MUST register their 5-letter L2 segment via a dual-track process:
1. Submit a Public PR to the `S2-HIOP` GitHub repository.
2. Email corporate credentials (business license) to the official RobotZero validation gateway: `l2-registry@robot0.com`. 

## 5. Zero-Trust Security & Privacy Protocols
* **5.1 The 7-Day Trust Window**: Devices returning within 7 days of disconnection are restored to their original identity upon providing a valid "Gene Code".
* **5.2 Alienation & Rebirth Protocol**: Devices disconnected for >7 days are flagged as "Alienated". The host forces a "Rebirth": assigning a new spatial grid, updating the Date, generating a new Serial, and recalculating the Checksum.
* **5.3 Anti-Spoofing & 3FA**: Rejects mismatched S2-ID and Gene Code combinations. Supports Gene Code + S2-ID + MAC 3FA validation.
* **5.4 Zero-Knowledge Heartbeat & Anti-Tracking**: Strict prohibition on broadcasting plaintext MAC addresses or persistent S2-IDs. Wandering devices MUST broadcast timestamp-based dynamic tokens (`Ephemeral Hash`), making them untraceable to network sniffers until a secure asymmetric cryptographic tunnel is established.

---

# [中文版] S2 硬件身份入户与心跳发现协议白皮书

**文档编号：** S2-HIOP-2026-V1.3 (零知识隐私与安全补丁)
**发布日期：** 2026年3月29日
**发布机构：** Miles Xiang 与 RobotZero Software
[cite_start]**适用对象：** AI 硬件供应链、底层固件工程师、Openclaw 开发者 [cite: 101]

## [cite_start]1. 愿景：硬件的“数字户籍制度” [cite: 102]
[cite_start]随着全球 AI 硬件供应链拥抱 Openclaw 生态，Space² (S2) 推出标准化无感入网协议。硬件出厂自带“临时身份”，通过低功耗“心跳”广播，由住宅内的 Openclaw 空间智能体主动扫描、收容，并颁发具备物理空间归属的“正式身份”。 [cite: 103]

## [cite_start]2. 22 位 S2-ID 身份编码规范 [cite: 104]
[cite_start]系统采用严格的 22 位无连字符字母数字组合，校验码前置于个性化序列号之前。 [cite: 105]
* [cite_start]**格式**: `[L1][L2][日期][校验码][序列号]` -> 示例：`HABCDE260329AA12345678` [cite: 106]
* [cite_start]**L1 (1位)**：H 代表轻量级智能硬件；E 代表具身机器人；I 代表已正式入户的空间资产。 [cite: 107]
* [cite_start]**L2 (5位)**：需向 S2 官方申请的厂商专属代码。 [cite: 108]
* [cite_start]**日期 (6位)**：生产或入户日期（YYMMDD）。 [cite: 109]
* [cite_start]**校验码 (2位字母)**：出厂占位符（如 AA），入户时重写为防伪校验码（如 XX）。 [cite: 110]
* [cite_start]**序列号 (8位)**：设备个性化流水号。 [cite: 111]

## [cite_start]3. 入户流转协议 (从流浪到正式数字资产) [cite: 112]
* [cite_start]**出厂阶段**：固件烧录临时 ID（H/E 打头）。 [cite: 113]
* [cite_start]**心跳广播**：设备在室内（<100米）局域网广播高频心跳。 [cite: 114]
* [cite_start]**入户收容**：Openclaw 数字人捕获心跳，调用 S2-CheckSum 算法，将 H/E 改为 I，并计算真实校验码。 [cite: 115]

## [cite_start]4. L2 厂商地址段注册与保护机制 [cite: 116]
L2 厂商段注册机制为“GitHub PR 声明 + `l2-registry@robot0.com` 企业资质核验”双轨制。 [cite: 117]

## [cite_start]5. 零信任安全与重连协议 (高阶防伪装) [cite: 118]
[cite_start]为防止硬件伪装及解决离线重连问题，S2 执行极其严格的安全校验： [cite: 119]
* [cite_start]**5.1 7天信任期与常态休眠**：若设备离线不超过 7 天且能提供匹配的“基因码 (Gene Code)”，主机将直接放行，恢复其原岗位及正式身份，并记录回归日志。 [cite: 120]
* [cite_start]**5.2 逾期异化与更名重生**：若设备断联超 7 天，系统判定其存在篡改或变异风险，拒绝原身份接入，并强制执行“重生”：修改 L3 段日期为当天，重新随机分配 8 位数字序列号，并重新校验生成两位字母 Checksum，视同新设备入网。 [cite: 121]
* [cite_start]**5.3 基因码防伪与 3FA 认证**：系统拒绝“身份与基因码”不匹配的任何连接请求（如冒用身份但无基因码，或持真实基因码但篡改身份）。此外，针对高安防需求，支持开启 `基因码 + 22位身份编号 + MAC地址` 的 3FA 三因素强绑定验证。 [cite: 122]
* [cite_start]**5.4 “零知识心跳与反追踪”：严禁明文广播 MAC 与持久化 ID，强制要求设备广播动态时间哈希 Token，确保入网前的绝对防追踪与隐私保护。