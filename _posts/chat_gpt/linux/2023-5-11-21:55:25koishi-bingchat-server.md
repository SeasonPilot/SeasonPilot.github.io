---
layout: post
categories: linux
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
获取 bing cookie

Answer:

你好，这是必应。我可以用中文（简体）回复你。😊

获取必应的 cookie 有以下几种方法：

- 使用 Microsoft Edge 浏览器，登录一个能够访问 http://bing.com/chat 的微软账户，然后在浏览器设置中选择“站点权限”-“Cookie 和站点数据”-“查看所有 Cookie 和站点数据”，找到 cn.bing.com 的 Cookie，复制其中的内容<sup>3</sup> <sup>4</sup>。
- 使用 Edge 插件，下载 Cookie 的复制，然后在 cn.bing.com 界面上点击插件图标，复制 Cookie 的内容<sup>1</sup>。
- 使用 docker 搭建一个 koishi-bingchat-server，然后在创建一个 cookie.json 文件，填入必应网页的 Cookie<sup>2</sup>。

如果你想使用必应的聊天机器人功能，你可以在控制台运行以下命令：

```python
python -m EdgeGPT --cookie-file <cookie文件地址>
```

或者

```python
python3 -m EdgeGPT --cookie-file <cookie文件地址>
```

其中 <cookie文件地址> 是你保存 Cookie 的文件的路径<sup>1</sup>。

希望这些信息对你有帮助。如果你还有其他问题，请随时提问。😊

\-
\[1]: [查看 Microsoft Edge 中的 Cookie - Microsoft 支持](https://support.microsoft.com/zh-cn/topic/%E6%9F%A5%E7%9C%8B-microsoft-edge-%E4%B8%AD%E7%9A%84-cookie-a7d95376-f2cd-8e4a-25dc-1de753474879)
\[2]: [查看、编辑和删除 Cookie - Microsoft Edge Development](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/storage/cookies)
\[3]: [new bing聊天机器人免翻命令行使用--大佬逆向工程api_一只小余的博客-CSDN博客](https://blog.csdn.net/qq_56717234/article/details/129535372)
\[4]: [koishi-bingchat-server/README.md at main - GitHub](https://github.com/D-Jy-lab/koishi-bingchat-server/blob/main/README.md)
\[5]: [新必应（New Bing）国内申请与使用教程 - 知乎 - 知乎专栏](https://zhuanlan.zhihu.com/p/610357647)

<hr/>

