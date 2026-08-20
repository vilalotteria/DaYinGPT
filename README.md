# DaYin GPT

> **Status: being prepared for submission to the Chrome Web Store.** The install
> link will be added here once it's live. This repository is already open so that
> issues can be filed.

Export ChatGPT conversations to **PDF / HTML / Markdown**, picking exactly which
messages to include, with the page's original formatting preserved — code blocks
with syntax highlighting, tables, nested lists, quotes and images.

**Everything runs locally in your browser. No conversation content is ever
uploaded anywhere.** See [PRIVACY.md](PRIVACY.md).

[中文说明见下 ↓](#中文说明)

> **This repository is for feedback, not source code.** It holds this README and
> the issue tracker. If you hit a bug or want a feature,
> [open an issue](https://github.com/vilalotteria/DaYinGPT/issues).

## Install

<!-- TODO: 上架后把下面这行换成商店链接 -->
Chrome Web Store: *not listed yet — link coming once it's live*

After installing, **pin the extension to your toolbar** — otherwise you have to
dig it out of the puzzle-piece menu every time.

## How to use

1. Open any ChatGPT conversation
2. Click the **Print / Export** button at the bottom-right of the page (or the
   toolbar icon → **Select & Export**)
3. Tick the messages you want. There are shortcuts for *All / Answers only / Invert*
4. Edit the title if you like, pick a format, click **Print / Export**

Picking **PDF** opens Chrome's print dialog — from there you can send it to a
printer or choose **Save as PDF**. Either way, tick **Background graphics**.

Picking **HTML** or **Markdown** opens a save dialog, so you choose the filename
and folder yourself.

The gear icon ⚙️ has one option: **PDF page numbers**.

## Known issues & FAQ

### Print it, or save it as a PDF — the dialog does both

*DaYin* (打印) is Chinese for *print*, and that is the point of this extension:
turning a conversation into something you can actually put on paper or file away.

Choosing **PDF** opens Chrome's print dialog, and from there you pick either path:

- **Select a printer** → the conversation is printed
- **Select "Save as PDF"** → it's written to a file

Both are intended uses. The document is rendered by Chrome's own print engine —
the same one behind Ctrl+P on any page — so nothing is uploaded and no PDF library
is bundled.

**Tick "Background graphics"** under *More settings*. Without it, code blocks lose
their shading, which is most of what makes the export look like the page.

One caveat: **Chrome can't be told which destination to preselect.** No browser API
sets the print destination for a page, so the extension can't choose for you. The
only way around it — driving Chrome's debugging interface to render the PDF with no
dialog at all — needs the `debugger` permission, which this extension deliberately
does not request: it would allow reading and modifying any page, and Chrome would
show a "being debugged" banner on every export.

In practice it's a one-time step, since **Chrome remembers the destination you used
last**.

### Long conversations with many images take a while

Every image is downloaded separately and converted to base64 so that it lives
*inside* the exported file. A conversation with dozens of images can take tens of
seconds, and the result can be tens of megabytes.

The progress bar shows `Processing images x/y` — it isn't frozen, just working.

**There is no way to turn this off, on purpose.** ChatGPT's image URLs are signed
and expire, so an export that only references them looks fine today and is full of
broken images a while later. Making that a checkbox would mean asking you to decide
based on something you have no way of knowing. The wait buys you a file that still
works in a year.

### A Markdown viewer shows the code blocks as plain text

Some Markdown readers don't support fenced code blocks (the ``` kind) out of the
box — Calibre's viewer, for instance, has that extension switched off by default.
The result is that code runs together into one paragraph.

The exported file is fine; the reader just isn't reading it fully. Either enable
the `fenced_code` extension in that reader, or **export HTML instead** — for
reading rather than editing, HTML keeps the formatting exactly and needs no
extensions.

### Images end up at the bottom of a message

Images are appended after the text of the message they belong to, rather than
being placed back at their original position in the paragraph flow. The content is
all there; the layout differs from the web page.

### Math formulas aren't rendered

Formulas are kept as their original LaTeX source. There is no math rendering in
the exported file.

### Not supported

Canvas documents, and the citation superscripts in Deep Research answers.

### It worked yesterday and today it doesn't

Most likely ChatGPT changed something on their end.

This extension reads your conversation through the same internal interface the
ChatGPT web app uses on itself. That interface isn't a published, stable API —
OpenAI can change it at any time, without notice, and when they do, an extension
built on it can stop working overnight. Every ChatGPT exporter has this problem;
it isn't something that can be engineered away.

What to do:

1. **Check for an extension update first.** `chrome://extensions` → turn on
   *Developer mode* → *Update*. If a fix is already out, this is the fastest path.
2. If it's still broken, [open an issue](https://github.com/vilalotteria/DaYinGPT/issues)
   and say **what you saw** — nothing exported at all, some messages missing,
   images broken, the Print / Export button gone — plus your Chrome version. That
   distinction is what points at the cause.

Exports you've already saved are plain PDF, HTML, or Markdown files on your own
computer. They keep working no matter what happens to the extension or to ChatGPT.

### Markdown export says it can't find the source

Markdown export needs ChatGPT's own backend response. If that request fails, the
extension falls back to scraping the page, which only yields rendered HTML — no
Markdown source. Reload the page and try again; PDF and HTML still work.

## Privacy in one paragraph

The extension reads your conversation using ChatGPT's **own internal API** — the
same request your browser already makes when you open a past conversation — using
your existing login. That request is read-only and **does not consume tokens or
cost anything**. Nothing is sent to the author or to any third party; there is no
server involved. The only outbound requests are image downloads from OpenAI's CDN,
so that images end up inside the file. Full details: [PRIVACY.md](PRIVACY.md).

## Reporting a bug

[Open an issue](https://github.com/vilalotteria/DaYinGPT/issues) and include:

- Chrome version and OS
- Which format you exported (PDF / HTML / Markdown)
- What you expected vs. what you got

**Please don't paste conversation content into a public issue.** A screenshot with
the sensitive parts blacked out is enough — and if a bug only reproduces with
specific content, say so and I'll work out another way to look at it.

## Buy me a boba tea

DaYin GPT is free and stays free — nothing is gated, and there is nothing to buy
inside it. If it saved you some time,
[you can buy me a boba tea](https://ko-fi.com/vilalotteria). Entirely optional.

---

<a id="中文说明"></a>

# 中文说明

> **状态：正在准备上架 Chrome 应用商店。** 上架后会把安装链接补在这里。
> 仓库先公开，是为了可以提 issue。

把 ChatGPT 网页对话导出成 **PDF / HTML / Markdown**，可以逐条挑选要导出哪些消息，
排版尽量贴近网页所见 —— 代码块（含语法高亮）、表格、嵌套列表、引用、图片都保留。

**全部在你的浏览器本地完成，对话内容不上传到任何地方。**
详见 [PRIVACY.md](PRIVACY.md)。

> **这个仓库只用来收集反馈，不放源码。** 里面只有这份说明和 Issue 区。遇到问题或
> 想要新功能，[提个 issue](https://github.com/vilalotteria/DaYinGPT/issues)。

## 安装

<!-- TODO: 上架后把下面这行换成商店链接 -->
Chrome 应用商店：*尚未上架，上线后补上链接*

装好后建议**把插件固定到工具栏**，否则每次都要去拼图图标里翻。

## 怎么用

1. 打开任意一个 ChatGPT 对话
2. 点页面右下角的**打印 / 导出**按钮（或点工具栏图标 →**选择并导出**）
3. 勾选要导出的消息，上面有**全部 / 仅回答 / 反选**三个快捷键
4. 需要的话改一下标题，选格式，点**打印 / 导出**

选 **PDF** 会弹出 Chrome 的打印对话框 —— 可以直接选打印机打印，也可以选**另存为
PDF** 存成文件。两种都记得勾上**背景图形**。

选 **HTML** 或 **Markdown** 会弹出保存对话框，文件名和位置由你自己定。

齿轮 ⚙️ 里只有一个选项：**PDF 页码**。

## 已知问题与常见疑问

### 可以直接打印，也可以存成 PDF

**大印**就是打印 —— 这个插件的落点就是把对话变成能真正打出来、能归档的东西。

选 **PDF** 会弹出 Chrome 的打印对话框，从那里走哪条都行：

- **选一台打印机** → 直接把对话打印出来
- **选「另存为 PDF」** → 存成文件

两条都是正常用法。文档由 Chrome 自己的打印引擎渲染 —— 和你在任意网页上按 Ctrl+P
是同一个引擎 —— 所以不上传任何东西，也没有内置任何 PDF 库。

**记得在「更多设置」里勾上「背景图形」。** 不勾的话代码块的底色会全部丢掉，而那
正是「看起来像网页原样」的主要来源。

一个限制：**没法让 Chrome 预先选好某个目标。** 浏览器不提供设置打印目标的接口，
插件替你选不了。唯一能绕开的办法是调用 Chrome 的调试接口直接渲染，那需要
`debugger` 权限 —— 本插件**特意不申请**：它意味着可以读写任意网页，而且每次导出
Chrome 都会挂出「正在调试此浏览器」的横幅。

实际上这是一次性的，因为 **Chrome 会记住你上次选的目标**。

### 图片多的长对话导出很慢

每张图都要单独下载再转成 base64 塞**进文件里**。几十张图的对话可能要等几十秒，
生成的文件也可能有几十 MB。

进度条上会显示`正在处理图片 x/y`，不是卡死了，是真在跑。

**这个没有开关，是故意的。** ChatGPT 的图片地址是带签名、会过期的临时链接，只存
链接的文件今天看着好好的，过一阵打开就是满屏裂图。把它做成一个勾选项，等于要你
拿一个你无从知道的前提去做决定。多等这几十秒，换的是一份一年后还能打开的文件。

### 用某些 Markdown 阅读器打开，代码块变成了普通文字

有些 Markdown 阅读器默认不支持围栏代码块（就是 ``` 那种）—— 比如 Calibre 的
阅读器就默认关着这个扩展。结果就是代码全挤成一段。

**导出的文件本身没问题**，是阅读器没读全。要么在那个阅读器里打开 `fenced_code`
扩展，要么**改导 HTML** —— 只是拿来读而不是再编辑的话，HTML 排版原样保留，
也不依赖任何扩展。

### 图片都跑到消息末尾去了

图片会追加在所属消息的文字之后，而不是还原到原文段落中间的位置。内容不会丢，
但版式和网页上不完全一样。

### 数学公式没有渲染

公式保留 LaTeX 原文，导出的文件里不做渲染。

### 不支持的内容

Canvas 画布，以及深度研究回答里的引用角标。

### 昨天还能用，今天不行了

多半是 ChatGPT 那边改了东西。

这个插件读对话，用的是 ChatGPT 网页版**对自己用的那套内部接口**。它不是公开的、
有稳定性承诺的 API —— OpenAI 随时可以改，改了也不会有通知，一改插件就可能一夜之间
失效。所有做 ChatGPT 导出的插件都有这个问题，**这不是靠把代码写得更结实能消除的**。

怎么办：

1. **先看有没有插件更新。** `chrome://extensions` → 打开**开发者模式** →
   点**更新**。如果修复已经发出来了，这是最快的路
2. 还是不行就[提个 issue](https://github.com/vilalotteria/DaYinGPT/issues)，说清楚
   **你看到的现象** —— 完全导不出来、少了一部分消息、图片裂了、还是导出按钮直接
   不见了 —— 再带上 Chrome 版本。这个区分正是定位原因的关键

已经存下来的文件是普通的 PDF / HTML / Markdown，就在你自己电脑上。**无论插件还是
ChatGPT 之后发生什么，它们都照常能打开。**

### 导出 Markdown 时提示找不到源码

Markdown 导出依赖 ChatGPT 自己的后端返回。那个请求失败时，插件会退回到从页面上
抓取，而页面上只有渲染后的 HTML、没有 Markdown 源码。刷新页面重试即可，此时
PDF 和 HTML 不受影响。

## 隐私（一段话版）

插件读对话用的是 ChatGPT 网页版**自己的内部接口** —— 就是你点开一个历史对话时
浏览器本来就会发的那个请求 —— 用的是你当前的登录状态。这个请求是**纯读取**，
**不消耗 token、不产生任何费用**。没有任何内容发给作者或第三方，整个过程不经过
任何服务器。唯一的对外请求是从 OpenAI 的 CDN 下载图片，好把它们存进导出的文件里。
完整说明见 [PRIVACY.md](PRIVACY.md)。

## 反馈问题

[提 issue](https://github.com/vilalotteria/DaYinGPT/issues) 时请带上：

- Chrome 版本和操作系统
- 导出的是哪种格式（PDF / HTML / Markdown）
- 你期望的结果 vs 实际的结果

**请不要把对话内容贴进公开 issue。** 打个码的截图就够了；如果某个问题只有特定内容
才能复现，说一声，我们再想别的办法看。

## 请我喝杯奶茶

这个插件是免费的，以后也是 —— 没有任何功能被锁住，插件里也没有任何可购买的东西。
如果它帮你省了点时间，可以[请我喝杯奶茶](https://ko-fi.com/vilalotteria)，纯自愿。
