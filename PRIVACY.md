# Privacy Policy — DaYin GPT

**Last updated: 2026-08-09**

[中文版见下 ↓](#隐私政策--dayin-gpt)

## Summary

DaYin GPT does not collect, transmit, store, or sell any personal data. There is
no server, no account, no analytics, and no third party involved. Everything the
extension does happens inside your own browser, and the file it produces is saved
to your own computer.

## What the extension accesses

When — and only when — you click **Export** on a ChatGPT page, the extension reads
the content of that conversation: the message text, its formatting, and any images
in it.

It does this by calling ChatGPT's **own internal API** (`/backend-api/conversation/…`),
the same request your browser already makes when you open a past conversation, using
the login session you already have. The extension does not ask for, see, or store
your password or any authentication token beyond the duration of the export.

That request is read-only. It does not run a model, so it **does not consume tokens,
incur charges, or use up message quota**.

## What happens to that content

It is turned into a PDF, HTML, or Markdown file and saved where you tell your browser
to save it. That is the whole lifecycle.

The content is **never** sent to the extension's author, to any server operated by
the author, or to any third party. There is no telemetry, no crash reporting, no
usage statistics, and no advertising.

## Network requests

The extension makes outbound requests to exactly two kinds of destination, both
belonging to OpenAI:

| Destination | Why |
|---|---|
| `chatgpt.com`, `chat.openai.com` | Read the conversation you asked to export |
| `*.oaiusercontent.com`, `*.oaistatic.com` | Download images in that conversation, when *embed images* is enabled |

These are declared in the extension's `manifest.json` as `host_permissions`, which
is the complete and enforceable whitelist — Chrome will not let the extension reach
any other host. You can inspect it yourself in `chrome://extensions`.

No requests are made to any domain owned by the author.

## Local storage

The extension uses Chrome's local extension storage for two things:

1. **Your preferences** (whether to embed images, whether to number PDF pages).
   These never leave your device.
2. **A temporary copy of the document being exported**, when a file is too large to
   pass between extension components directly. It is deleted as soon as the export
   finishes, and any leftovers from an interrupted export are cleared the next time
   your browser starts.

Nothing is written to any remote storage.

## Permissions and why each one is needed

| Permission | Why |
|---|---|
| `activeTab` | Read the conversation on the ChatGPT tab you are currently looking at, at the moment you click Export |
| Host access to the domains above | Fetch the conversation and its images |
| `storage` | Remember your export preferences |
| `unlimitedStorage` | Hold the temporary document above — a long conversation with embedded images can exceed the default quota |

That is the complete list. In particular, the extension does **not** request access
to your browsing history, your bookmarks, your downloads, or any site other than
the ones named above. You can verify this at `chrome://extensions` → *Details*.

## Children

The extension is not directed at children and does not knowingly process any data
about them. It processes only the conversation you explicitly choose to export.

## Changes to this policy

If this policy changes, the updated version will be published in this repository and
the date at the top will be revised. Because the repository is public, the full
history of changes is visible to anyone.

## Contact

Questions about this policy, or about anything the extension does, are welcome as an
[issue in this repository](https://github.com/vilalotteria/DaYinGPT/issues).

---

# 隐私政策 — DaYin GPT

**最后更新：2026-08-09**

## 一句话概括

DaYin GPT 不收集、不传输、不存储、不出售任何个人数据。没有服务器、没有账号、没有
数据统计、不涉及任何第三方。插件做的一切都发生在你自己的浏览器里，生成的文件保存
在你自己的电脑上。

## 插件会读取什么

**只有**在你于 ChatGPT 页面上点击**导出**时，插件才会读取该对话的内容：消息文字、
排版，以及其中的图片。

读取方式是调用 ChatGPT **自己的内部接口**（`/backend-api/conversation/…`）—— 就是
你点开一个历史对话时浏览器本来就会发的那个请求 —— 用的是你已有的登录状态。插件
不索取、不查看、也不留存你的密码或任何认证凭据（导出过程之外一概不持有）。

这个请求是纯读取，不运行模型，因此**不消耗 token、不产生费用、不占用消息次数**。

## 这些内容之后怎么处理

被转换成 PDF、HTML 或 Markdown 文件，保存到你指定的位置。整个生命周期到此为止。

这些内容**绝不会**发送给插件作者、作者运营的任何服务器，或任何第三方。没有遥测、
没有崩溃上报、没有使用统计、没有广告。

## 对外网络请求

插件只会向两类目标发出请求，都属于 OpenAI：

| 目标 | 用途 |
|---|---|
| `chatgpt.com`、`chat.openai.com` | 读取你要导出的那个对话 |
| `*.oaiusercontent.com`、`*.oaistatic.com` | 开启**内嵌图片**时下载对话里的图片 |

这些写在插件 `manifest.json` 的 `host_permissions` 里，是完整且由浏览器强制执行的
白名单 —— Chrome 不会允许插件访问名单外的任何主机。你可以在 `chrome://extensions`
里自行核对。

不存在任何指向作者名下域名的请求。

## 本地存储

插件使用 Chrome 的本地扩展存储，只存两样东西：

1. **你的偏好设置**（是否内嵌图片、PDF 是否加页码）。这些不会离开你的设备
2. **正在导出的文档的临时副本** —— 文件太大、无法在扩展内部各组件之间直接传递时
   会先落到本地。导出一结束就删除；如果导出被中断留下了残留，下次浏览器启动时会
   自动清理

没有任何内容写入远程存储。

## 各项权限分别用来做什么

| 权限 | 用途 |
|---|---|
| `activeTab` | 在你点导出的那一刻，读取你当前正在看的那个 ChatGPT 标签页里的对话 |
| 上表中域名的访问权 | 抓取对话及其图片 |
| `storage` | 记住你的导出偏好 |
| `unlimitedStorage` | 存放上面那份临时文档 —— 图片内嵌的长对话会超出默认配额 |

以上就是全部。特别说明：插件**不**申请浏览历史、书签、下载记录的访问权，也不申请
上面列出之外的任何站点。可以在 `chrome://extensions` →**详情**里自行核对。

## 未成年人

本插件并非面向儿童设计，也不会有意处理与儿童相关的任何数据。它只处理你明确选择
导出的那个对话。

## 政策变更

政策如有变更，新版本会发布在本仓库，并更新顶部日期。仓库是公开的，所有修改记录
任何人都可以查看。

## 联系方式

对本政策或插件行为有任何疑问，欢迎在
[本仓库提 issue](https://github.com/vilalotteria/DaYinGPT/issues)。
