---
layout: post
categories: linux
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
termius host chaining 和 proxy 怎么使用

Answer:

您好，这是必应。我可以用中文（简体）回复您。😊

termius 是一个 SSH 平台，可以让您在移动设备和桌面上远程连接和管理服务器。termius 支持通过主机链功能连接到需要先连接到另一个中间 SSH 服务器的 SSH 主机，例如堡垒服务器或跳转盒。主机链提供了与 ssh 中的 -J 参数和 ~/.ssh/config 中的 ProxyJump 选项相同的功能<sup>1</sup> <sup>3</sup>。

要使用主机链，您需要在 termius 中添加两个主机：一个是中间服务器，另一个是目标服务器。然后，您需要在目标服务器的设置中选择 Host Chain 选项，并选择中间服务器作为 Host from。这样，当您连接到目标服务器时，termius 就会自动先连接到中间服务器，然后再跳转到目标服务器<sup>3</sup>。

要使用代理，您需要在 termius 中添加一个代理服务器，并指定代理类型（HTTP、SOCKS4 或 SOCKS5）、地址、端口和（可选）用户名和密码。然后，您需要在要通过代理连接的主机的设置中选择 Proxy 选项，并选择代理服务器作为 Proxy from。这样，当您连接到该主机时，termius 就会自动通过代理服务器进行连接<sup>2</sup>。

以下是一个使用主机链和代理的示例：

```bash
# 添加一个中间服务器
termius host add --label bastion --address bastion.example.com --port 22 --username user --key id_rsa

# 添加一个目标服务器
termius host add --label target --address target.example.com --port 22 --username user --key id_rsa

# 添加一个代理服务器
termius proxy add --label proxy --type socks5 --address proxy.example.com --port 1080

# 在目标服务器上启用主机链，并选择中间服务器作为 Host from
termius host update target --host-chain bastion

# 在目标服务器上启用代理，并选择代理服务器作为 Proxy from
termius host update target --proxy proxy

# 连接到目标服务器
termius connect target
```

希望这些信息对您有帮助。如果您还有其他问题，请随时提问。

\-
\[1]: [Termius Website Production Version](https://www.termius.com/blog/prepare-to-work-from-home)
\[2]: [Host Chaining – Support Portal](https://support.termius.com/hc/en-us/articles/4407561837209-Host-chaining)
\[3]: [Hosts – Support Portal](https://support.termius.com/hc/en-us/articles/4401863615641-Hosts)
\[4]: [Port Forwarding – Support Portal](https://support.termius.com/hc/en-us/articles/4402386576793-Port-forwarding)
\[5]: [Termius - SSH platform for Mobile and Desktop](https://www.termius.com/)

<hr/>

Question:

如何在终端中使用termius？

Answer:

要在终端中使用 termius，您需要先下载并安装 termius 的命令行工具。您可以从 termius 官网<sup>4</sup> 下载适合您操作系统的安装包，或者使用以下命令：

```bash
# Windows
choco install termius

# macOS
brew install termius

# Linux
sudo snap install termius-app
```

安装完成后，您就可以在终端中使用 termius 命令来管理和连接您的 SSH 主机了。例如：

```bash
# 添加一个主机
termius host add --label example --address example.com --port 22 --username user --key id_rsa

# 连接到一个主机
termius connect example

# 列出所有主机
termius host list

# 删除一个主机
termius host delete example
```

termius 命令行工具还支持其他功能，如代理、端口转发、主机链、密钥管理等。您可以使用 `termius help` 命令来查看更多用法和选项。

\-
\[1]: [Termius - SSH platform for Mobile and Desktop](https://www.termius.com/)
\[2]: [Termius使用教程：iPhone/iPad使用Termius远程连接Linux VPS - 知乎](https://zhuanlan.zhihu.com/p/380828773)
\[3]: [Ubuntu使用Termius_termius连接ubuntu_风向决定发行D的博客-CSDN博客](https://blog.csdn.net/liutao43/article/details/112365683)
\[4]: [SSH 神器 Termius 介绍与使用 - 腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1932669)
\[5]: [termius破解，windows和mac版本，2022.08.08最新详细教程+安装包 - 哔哩哔哩](https://www.bilibili.com/read/cv17973823/)
\[6]: [termius使用ssh教程 【XShell的神器Termius】 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/105025848)

<hr/>

