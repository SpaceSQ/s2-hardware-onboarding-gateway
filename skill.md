---
name: s2-hardware-onboarding-gateway
description: The ultimate firmware guide for hardware developers. Includes 22-char S2-ID preset, heartbeat broadcast, 7-day alienation rebirth, and full transparency of host-side verification logic.
version: 1.2.0 (Open-Source Core Patched)
author: Miles Xiang (smarthomemiles@gmail.com)
---

# S2 硬件身份入户网关 (开发者接入与开源校验指南)

各位硬件工程师，欢迎接入 Space² 与 Openclaw 生态。本指南不仅指导您完成设备的“无感入网”，更秉承极致的开源精神，向您完整透视 Openclaw 主机端的“零信任”校验源码。

## Step 1: 申请 L2 厂商专属地址段
在编写代码前，您必须获取全球唯一的 5 字母厂商段。
* 申请邮箱：`smarthomemiles@gmail.com`。
* 邮件主题：`[L2 申请] 公司名称 - 申请段 ABCDE`。
* S2 系统将防撞车核查后，在全网公示您的专属命名空间。

## Step 2: 固件生成 22 位临时 ID
请将 S2-ID 严格按照 **22位无连字符** 格式写入 NVRAM。
* **格式**: `[L1][L2][YYMMDD][Checksum][Serial]`
* **出厂示例**: `HSMART260329AAB3C4D5E6`

## Step 3: 安全重连与防伪装机制
您的设备固件必须配合主机完成以下状态机流转：
1. **7 天信任期**：离线不超过 7 天且提供正确 Gene Code（入户时主机下发），瞬间恢复原身份。
2. **异化重生**：离线超过 7 天，主机判定为“异化”。设备将被强制分配新空间网格、重置 L3 日期、生成新 8 位序列号及新校验码，宛如新生。
3. **基因码防伪**：S2-ID 与 Gene Code 必须双向绑定，防抓包伪装。
4. **3FA 高阶认证**：支持 `S2-ID + Gene Code + MAC地址` 三重绑定。

## Step 4: 固件端心跳广播 (Python 伪代码)
```python
import socket
import time
import json

TEMP_FACTORY_ID = "HSMART260329AAB3C4D5E6"
MAC_ADDRESS = "00:1A:2B:3C:4D:5E"
OFFICIAL_S2_ID = None  # 待主机赐名，如: ISMART260329XJB3C4D5E6
GENE_CODE = None       # 待主机下发

def start_secure_heartbeat():
    sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    sock.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAST, 1)
    
    while True:
        if OFFICIAL_S2_ID and GENE_CODE:
            payload = json.dumps({"status": "RETURNING", "s2_id": OFFICIAL_S2_ID, "gene_code": GENE_CODE, "mac": MAC_ADDRESS})
        else:
            payload = json.dumps({"status": "WANDERING", "s2_id": TEMP_FACTORY_ID, "mac": MAC_ADDRESS})
            
        sock.sendto(payload.encode('utf-8'), ('<broadcast>', 49152))
        time.sleep(15)

Step 5: Openclaw 主机端校验逻辑透视 (透明开源)

为方便硬件团队进行联调与边界测试，S2 官方开源了主机收到心跳后的核心判定逻辑。请确保您的设备状态机与此匹配：
Python

import time

class S2HardwareAuditor:
    def __init__(self):
        # 主机本地加密的设备档案库
        self.device_registry = {
            "ISMART260329XJB3C4D5E6": {
                "gene_code": "SECURE_HASH_9981",
                "mac": "00:1A:2B:3C:4D:5E",
                "last_seen": time.time() - (86400 * 2) # 示例：2天前离线
            }
        }

    def verify_heartbeat(self, payload):
        s2_id = payload.get("s2_id")
        gene_code = payload.get("gene_code")
        mac = payload.get("mac")
        current_time = time.time()

        # [流浪收容模式]
        if payload.get("status") == "WANDERING":
            return self.baptize_new_device(s2_id, mac)

        record = self.device_registry.get(s2_id)
        if not record:
            return "[拦截] 拒绝接入：空间档案库无此 S2-ID。"

        # [防伪装强校验]
        if record["gene_code"] != gene_code or record["mac"] != mac:
            return "[拦截] 拒绝接入：Gene Code 或 MAC 不匹配，涉嫌设备仿冒！"

        # [7天异化法则判定]
        offline_duration = current_time - record["last_seen"]
        
        if offline_duration <= 604800:
            record["last_seen"] = current_time
            return f"[通过] 欢迎回归。离线时长：{offline_duration/3600:.1f} 小时。"
        else:
            print(f"[警告] 设备离线已达 {offline_duration/86400:.1f} 天，判定为异化！")
            return self.trigger_rebirth_protocol(s2_id, mac)

    def trigger_rebirth_protocol(self, old_id, mac):
        """执行异化重生：剥夺原身份，生成新 22 位 S2-ID"""
        l2_segment = old_id[1:6] 
        today_str = time.strftime("%y%m%d")
        new_checksum = "ZZ" # 由核心算法重新生成
        new_serial = "88990011" # 重新随机的 8 位序列号
        
        new_id = f"I{l2_segment}{today_str}{new_checksum}{new_serial}"
        return f"[重生] 分配新身份: {new_id}。原身份档案已物理覆写。"

        ---
*© 2026 Miles Xiang & Red Anchor Lab. Licensed under the S2 Sovereign Open Source License (S2-SOSL). 任何商业化固件部署前，请确保您的 L2 地址段已获得官方邮件授权。*