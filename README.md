# Git_mode-1

本仓库对应 GitHub 仓库 [Linxhz/Git_mode-1-](https://github.com/Linxhzy/Git_mode-1-)。

## 仓库用途

此仓库当前用于验证本机的 Git / GitHub 同步链路，后续放置该项目自身的代码与文档。

## 开始使用

```bash
git clone https://github.com/Linxhzy/Git_mode-1-.git
cd Git_mode-1-
```

## 本地环境备注

初始化本仓库时，本机存在以下**与仓库内容无关**的系统级问题，已记录于此以便后续恢复：

1. **文件夹权限**：`D:\Git\Git Projects\git_mode1` 及其父目录原本仅授予 `BUILTIN\Administrators` 完全控制，当前用户 `chimtree` 无写权限。已通过一次提权操作为该用户补上完全控制权限；同目录下的 `hosts.backup-github-unblock.txt` 是当时对系统 hosts 文件的备份副本，未纳入版本控制。
2. **HTTPS / TLS 故障**：本机所有 HTTPS 请求均握手失败（`Schannel` 报 `SEC_E_NO_CREDENTIALS`，内部状态 10013），普通网站（如百度）同样失败，用户级与机器级密钥容器均无法创建（`Access denied`）。该故障早于本仓库创建，需在系统层修复后 `git push` 才能成功。
3. **GitHub 域名被 hosts 屏蔽**：系统 hosts 文件将 `github.com`、`api.github.com`、`*.githubusercontent.com` 等 30 余个域名指向 `127.0.0.1`，且被安全软件在数秒内回写。推送前需先解除该屏蔽。
