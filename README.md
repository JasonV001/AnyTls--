 # AnyTls一键安装
<details>
    <summary>(点击展开)</summary>
 
```
bash <(curl -Ls https://raw.githubusercontent.com/JasonV001/AnyTls-ReaLity/main/install_anytls.sh)
```

</details>
 
 # reality-hysteria2一键安装
 
<details>
    <summary>(点击展开)</summary>

 ```bash
wget -O rl-hy2.sh https://raw.githubusercontent.com/JasonV001/AnyTls-ReaLity/main/reality-hysteria2.sh && chmod +x reality-hysteria2.sh && ./reality-hysteria2.sh
```
或者
```bash
bash <(curl -sSL https://raw.githubusercontent.com/JasonV001/AnyTls-ReaLity/main/reality-hysteria2.sh)
```

### 2. 再次运行脚本

```bash
sudo bash reality-hysteria2.sh
```

脚本将以 root 权限运行，并显示主菜单。
 <details>
    <summary>(点击展开)</summary>
    
*   **一键安装 Sing-Box (beta 版)**：自动从官方渠道下载并安装最新 beta 版本的 Sing-Box。
*   **多种安装模式**：
    *   同时安装 Hysteria2 和 Reality (VLESS) 服务，实现共存。
    *   单独安装 Hysteria2 服务。
    *   单独安装 Reality (VLESS) 服务。
*   **自动化配置**：
    *   Hysteria2: 自动生成自签名证书、随机密码。
    *   Reality (VLESS): 自动生成 UUID、Reality Keypair (私钥和公钥)。
    *   自动填充生成的凭证到 `config.json` 配置文件。
    *   用户可自定义监听端口、伪装域名 (SNI) 等关键参数。
*   **Systemd 服务管理**：
    *   自动创建并配置 Sing-Box 的 systemd 服务。
    *   方便地启动、停止、重启、查看服务状态及日志。
    *   设置开机自启。
*   **导入信息与二维码**：
    *   安装完成后，自动显示详细的客户端导入参数。
    *   如果系统已安装 `qrencode`，则会直接在终端显示导入链接的二维码。
    *   支持随时查看上次成功安装的配置信息及二维码。
*   **依赖自动处理**：
    *   自动检测核心依赖 (`curl`, `openssl`, `jq`) 和可选依赖 (`qrencode`)。
    *   如果依赖缺失，会提示用户并尝试通过系统包管理器 (apt, yum, dnf) 自动安装。
*   **便捷管理**：
    *   提供菜单式交互界面，操作简单直观。
    *   支持查看和编辑 Sing-Box 配置文件 (使用 `nano`)。
    *   一键更新 Sing-Box 内核。
    *   一键卸载 Sing-Box 及相关配置。
*   **信息持久化**：上次成功安装的配置参数会被保存，方便后续通过菜单再次查看。

## 环境要求

*   Linux (x86_64 / amd64, aarch64 / arm64 架构理论上支持，未全面测试)
*   root 权限 (脚本内操作需要 sudo)
*   核心依赖: `curl`, `openssl`, `jq` (脚本会尝试自动安装)
*   可选依赖: `qrencode` (用于显示二维码，脚本会尝试自动安装)


**初次使用建议：**

*   选择 `1`, `2`, 或 `3` 进行安装。脚本会引导你输入必要的参数（如端口、SNI 等），大部分参数有默认值可直接回车使用。
*   安装成功后，脚本会显示客户端导入所需的全部信息，包括文本参数和二维码（如果 `qrencode` 已安装）。请妥善保存这些信息。
*   之后你可以使用选项 `11` 再次查看这些信息。

### 注意事项

*   **配置文件**: Sing-Box 的主配置文件位于 `/usr/local/etc/sing-box/config.json`。Hysteria2 使用的自签名证书位于 `/etc/hysteria/`。
*   **持久化信息**: 上次成功安装的导入参数会保存在 `/usr/local/etc/sing-box/.last_singbox_script_info` 文件中，以便下次运行时通过菜单查看。卸载时如果选择删除配置目录，此文件也会被删除。
*   **SNI (伪装域名)**:
    *   对于 Reality，选择一个响应良好且不易被GFW干扰的SNI（如 `www.microsoft.com`, `www.apple.com` 等）非常重要。脚本会让你自定义。
    *   对于 Hysteria2 的自签名证书，SNI 主要用于客户端验证，默认使用 `bing.com`，你也可以自定义。
*   **端口占用**: 请确保你为 Hysteria2 和 Reality 选择的监听端口未被其他程序占用。脚本默认 Hysteria2 使用 `8443`，Reality 使用 `443`。
*   **防火墙**: 如果你的服务器启用了防火墙 (如 ufw, firewalld)，请确保放行 Sing-Box 使用的端口。
    例如，如果使用 ufw 并且 Reality 使用 443 端口，Hysteria2 使用 8443 端口：
    ```bash
    sudo ufw allow 443/tcp
    sudo ufw allow 8443/tcp
    sudo ufw allow 8443/udp # Hysteria2 需要 UDP
    sudo ufw reload
    ```

 </details>

</details>

# ReaLity一键安装
<details>
    <summary>(点击展开)</summary>
    
    
```
apt update
apt install -y curl
```
```
bash <(curl -L https://github.com/JasonV001/AnyTls-ReaLity/raw/main/install.sh)
```
脚本中很大部分都是在校验用户的输入。其实照着下面的步骤自己配置就行了。
# 说明 
这个一键脚本超级简单。有效语句8行(其中BBR 5行, 安装Xray 1行, 生成x25519公私钥 1行，生成UUID 1行)+Xray配置文件69行(其中你需要修改4行), 其它都是用来检验小白输入错误参数或者搭建条件不满足的。

你如果不放心开源的脚本，你可以自己执行那8行有效语句，再修改配置文件中的4行，也能达到一样的效果。

Reality底层是TCP直连，如果你的VPS已经被墙，那肯定用不了。出门左转 https://github.com/crazypeace/v2ray_wss

</details>

# 具体手搓步骤 (点击展开)
<details>
    <summary>(点击展开)</summary>

# 打开BBR
```
sed -i '/net.ipv4.tcp_congestion_control/d' /etc/sysctl.conf
sed -i '/net.core.default_qdisc/d' /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control = bbr" >>/etc/sysctl.conf
echo "net.core.default_qdisc = fq" >>/etc/sysctl.conf
sysctl -p >/dev/null 2>&1
```


# 安装Xray
source: https://github.com/XTLS/Xray-install
```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```


# 生成 x25519 公钥和私钥
```
xray x25519
```
私钥会在服务端用到，公钥会在客户端用到。


# 生成 UUID
```
xray uuid
```

# 选一个你喜欢的网站 (SNI)
比如，`learn.microsoft.com`


# 选一个你喜欢的指纹 (Fingerprint)
可选项见此：https://xtls.github.io/en/config/transport.html 不想选，就用`random`
![image](https://github.com/crazypeace/xray-vless-reality/assets/665889/89cdc776-95b4-4003-b89f-ac5a48bd1da5)


# Reality 协议中定义了 ShortId, SpiderX
个人使用可以不管，留空


# 配置 /usr/local/etc/xray/config.json
```
{ // VLESS + Reality
  "log": {
    "loglevel": "warning"
  },
  "inbounds": [
    {
      "listen": "0.0.0.0",
      "port": 443,    // 理论上可以随便改，不过从访问梯子的行为上，我个人认为使用443比较合适
      "protocol": "vless",
      "settings": {
        "clients": [
          {
            "id": "你的UUID",    // ***改这里
            "flow": "xtls-rprx-vision"
          }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "security": "reality",
        "realitySettings": {
          "show": false,
          "dest": "你喜欢的网站:443",    // ***如 learn.microsoft.com:443
          "xver": 0,
          "serverNames": ["你喜欢的网站"],    //***如 learn.microsoft.com
          "privateKey": "你的**私钥**",    // ***改这里
          "shortIds": [""]    // 可以留空
        }
      },
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "tag": "block"
    }
  ],
  "dns": {
    "servers": [
      "8.8.8.8",
      "1.1.1.1",
      "2001:4860:4860::8888",
      "2606:4700:4700::1111",
      "localhost"
    ]
  },
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "block"
      }
    ]
  }
}
```

# 客户端参数配置
脚本最后会输出VLESS链接，方便你导入翻墙客户端。

如果你是手搓自建，请参考下图配置。特别需要注意的是，客户端用的是**公钥**。和服务端用的**私钥**不一样。
![image](https://github.com/crazypeace/xray-vless-reality/assets/665889/52a943aa-ba8b-4a4a-a7ca-21c75807d678)

如果你是手搓VLESS链接，那么参考：https://github.com/XTLS/Xray-core/discussions/716
如 `vless://${xray_id}@${ip}:443?encryption=none&flow=xtls-rprx-vision&security=reality&sni=${domain}&fp=${fingerprint}&pbk=${public_key}&type=tcp#VLESS_R_${ip}`

# 如果是 IPv6 only 的小鸡，用 WARP 添加 IPv4 出站能力
```
bash <(curl -L git.io/warp.sh) 4
```

# Uninstall
```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ remove --purge
```
# 脚本支持带参数运行
```
bash <(curl -L https://github.com/crazypeace/xray-vless-reality/raw/main/install.sh) <netstack> [port] [domain] [UUID]
```

其中, 

`netstack` 6 表示 IPv6 入站; 4 表示 IPv4 入站.

`port` 端口. 不写的话, 默认443

`domain` 你指定的网站域名. 不写的话, 默认 learn.microsoft.com

`UUID` 你的UUID. 不写的话, 自动生成

例如,
```
bash <(curl -L https://github.com/crazypeace/xray-vless-reality/raw/main/install.sh) 6
bash <(curl -L https://github.com/crazypeace/xray-vless-reality/raw/main/install.sh) 6 443
bash <(curl -L https://github.com/crazypeace/xray-vless-reality/raw/main/install.sh) 6 443 learn.microsoft.com
bash <(curl -L https://github.com/crazypeace/xray-vless-reality/raw/main/install.sh) 6 443 learn.microsoft.com 1b0b723f-0544-4f9c-8df8-2b8975c5e47a
```

</details>

