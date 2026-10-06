# Git_mode-1

本仓库对应 GitHub 仓库 [Linxhzy/Git_mode-1-](https://github.com/Linxhzy/Git_mode-1-)。

## 仓库用途

此仓库用于验证本机 Git / GitHub 同步链路，后续放置该项目自身的代码与文档。

## 开始使用

```bash
git clone https://github.com/Linxhzy/Git_mode-1-.git
cd Git_mode-1-
```

## 本机环境说明

本机在初始化此仓库时遇到若干与仓库内容无关的环境问题，记录于此以便复现和排查。

### 1. DSH 沙箱内无法使用 HTTPS

DSH 会话的 shell 被限制在工作区内：工作区外的写入（含 `%APPDATA%`）会被拒绝。Schannel 需要写 `%APPDATA%\Microsoft\Crypto\...` 才能取得 TLS 客户端凭据，因此**沙箱内所有 HTTPS 握手都会失败**：

```
schannel: AcquireCredentialsHandle failed: SEC_E_NO_CREDENTIALS (0x8009030e)
```

同一段代码在沙箱外（如提权进程）运行完全正常。因此 `git push` 必须在沙箱外执行。

### 2. hosts 屏蔽 GitHub

本机 hosts 文件将 `github.com`、`api.github.com`、`*.githubusercontent.com` 等 30 余个域名指向 `127.0.0.1`，且该文件受驱动级保护（提权修改后仍会被还原）。绕开方式是把 GitHub 真实 IP 固定在仓库配置里，跳过 DNS：

```bash
git config http."https://github.com/".curloptResolve "github.com:443:20.205.243.166"
```

该配置已写入本仓库。`hosts.backup-github-unblock.txt` 是排查时留下的 hosts 备份副本，未纳入版本控制。

### 3. 沙箱外的推送方式

在沙箱外执行（首次会由 Git Credential Manager 弹浏览器登录）：

```bash
git -C "D:\Git\Git Projects\git_mode1" push -u origin main
```

本仓库的 GitHub 凭据已存入 Windows 凭据管理器，条目为 `git:https://github.com`（用户 `Linxhzy`）。
