# Cloudflare Pages 纯官方极速直连版（零第三方依赖 · 完整脱敏）

本代码已完成 **100% 隐私脱敏**，密码、UUID、域名全部通过 Cloudflare 环境变量注入，不含任何个人隐私信息。移除所有第三方个人反代，纯走 Cloudflare 官方原生 Anycast 骨干网，支持 5 大地区多端口分流与一键健康度检测。

---

## 极简部署教程（3 步上线）

### 第 1 步：上传代码到 Cloudflare Pages
1. 登录 [Cloudflare 控制台](https://dash.cloudflare.com/)。
2. 左侧菜单点击 **Workers 和 Pages** -> **Pages** -> **创建项目** -> 选择 **直接上传 (Direct Upload)**。
3. 项目名称随意填（例如 `my-vpn-site`），把包含 `_worker.js` 的文件夹拖入上传，点击 **部署站点**。

---

### 第 2 步：设置环境变量（核心隐私参数）
进入该项目详情页 -> **设置 (Settings)** -> **环境变量 (Environment variables)** -> **生产环境 (Production)**，添加以下变量：

| 变量名 | 推荐类型 | 说明 | 示例值 |
| :--- | :--- | :--- | :--- |
| `ADMIN` | **Secret (加密文本)** | 管理员后台登录密码与订阅 Token | `自定义长密码` |
| `UUID` | Plain text (文本) | VLESS 节点用户 UUID（标准 UUIDv4） | `可用在线工具生成的UUID` |
| `URL` | Plain text (文本) | 未授权防探测伪装页 | `1101` |
| `OFF_LOG` | Plain text (文本) | 关闭访问日志记录（提升性能与隐私） | `1` |

> 提示：无需设置任何 `PROXYIP` 变量，系统默认使用 Cloudflare 纯官方原生直连。

---

### 第 3 步：绑定自定义域名
1. 在项目详情页点击 **自定义域 (Custom domains)** -> **设置自定义域**。
2. 输入你解析在 Cloudflare 上的二级域名（例如 `sub.yourdomain.com`），点击继续并绑定。
3. 等待 1~2 分钟 SSL 证书生成完成。

---

## 使用与管理
- **管理后台**：访问 `https://你的域名/admin`，输入你设置的 `ADMIN` 密码即可登录。
- **一键检测**：登录后台后，点击 **【⚡ 一键检测】** 可秒级探测当前运营商识别、官方直连延迟和真实出站机房。
- **节点订阅**：支持直接复制 **Clash (YAML)**、**Base64** 与 **通用 VLESS** 链接，或直接用手机客户端扫码导入。

