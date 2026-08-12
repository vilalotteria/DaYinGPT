# DaYin GPT

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
Chrome Web Store: *not published yet*

After installing, **pin the extension to your toolbar** — otherwise you have to
dig it out of the puzzle-piece menu every time.

## How to use

1. Open any ChatGPT conversation
2. Click the **Export** button at the bottom-right of the page (or the toolbar
   icon → **Select & Export**)
3. Tick the messages you want. There are shortcuts for *All / Prompts / Answers /
   None / Invert*
4. Edit the title if you like, pick a format, click **Export**

For **PDF**, Chrome's print dialog opens. Under *Destination*, choose
**Save as PDF**.

The gear icon ⚙️ has two options: **embed images** and **PDF page numbers**.

## Known issues & FAQ

### Why does exporting a PDF open the print dialog?

Because that dialog *is* how the PDF gets made. The extension hands your formatted
document to Chrome's own print pipeline and lets Chrome render the PDF — the same
engine you get from Ctrl+P on any page. Nothing is uploaded and no PDF library is
bundled.

In the dialog, set **Destination** to **Save as PDF**, and tick **Background
graphics** under *More settings* — without it, code blocks lose their shading.

**Chrome cannot be told to preselect "Save as PDF".** There is no browser API that
sets the print destination for a page, so the extension can't do it for you. The
one workaround — driving Chrome's debugging interface to render the PDF without any
dialog — requires the `debugger` permission, which this extension deliberately does
not request: it would let the extension read and modify any page, and Chrome would
show a "being debugged" banner on every export.

The good news is that it's a one-time step. **Chrome remembers the destination you
last used**, so after the first export the dialog already opens on *Save as PDF*.

### Long conversations with many images take a while

With **embed images** on, every image is downloaded separately and converted to
base64 so it lives inside the file. A conversation with dozens of images can take
tens of seconds, and the result can be tens of megabytes.

The progress bar shows `Processing images x/y` — it isn't frozen, just working.

**If you want it fast:** turn off *embed images* in the gear menu. Export finishes
almost instantly and the file stays small, but images are then referenced by URL —
and ChatGPT's image URLs expire, so after a while you'll see broken images. For
anything you want to keep, leave embedding on and wait.

### The exported file gets a garbled name, or the download is taken over

HTML and Markdown exports use a normal browser download. If you have a download
manager extension installed (IDM, Chrono, Thunder, etc.), it can intercept the
download and rename the file to a random string.

DaYin GPT does not fight over the filename — when several extensions want to name
the same download, Chrome's rule is that the most recently installed one wins.

**Workarounds:** temporarily disable the download manager before exporting, or add
`chatgpt.com` to its exclusion list.

### Images end up at the bottom of a message

Images are appended after the text of the message they belong to, rather than
being placed back at their original position in the paragraph flow. The content is
all there; the layout differs from the web page.

### Math formulas aren't rendered

Formulas are kept as their original LaTeX source. There is no math rendering in
the exported file.

### Not supported

Canvas documents, and the citation superscripts in Deep Research answers.

### Markdown export says it can't find the source

Markdown export needs ChatGPT's own backend response. If that request fails, the
extension falls back to scraping the page, which only yields rendered HTML — no
Markdown source. Reload the page and try again; PDF and HTML still work.

## Privacy in one paragraph

The extension reads your conversation using ChatGPT's **own internal API** — the
same request your browser already makes when you open a past conversation — using
your existing login. That request is read-only and **does not consume tokens or
cost anything**. Nothing is sent to the author or to any third party; there is no
server involved. The only outbound requests are image downloads from OpenAI's CDN
when image embedding is on. Full details: [PRIVACY.md](PRIVACY.md).

## Reporting a bug

[Open an issue](https://github.com/vilalotteria/DaYinGPT/issues) and include:

- Chrome version and OS
- Which format you exported (PDF / HTML / Markdown)
- Whether *embed images* was on
- What you expected vs. what you got

**Please don't paste conversation content into a public issue.** A screenshot with
the sensitive parts blacked out is enough — and if a bug only reproduces with
specific content, say so and I'll work out another way to look at it.

---

<a id="中文说明"></a>

# 中文说明

把 ChatGPT 网页对话导出成 **PDF / HTML / Markdown**，可以逐条挑选要导出哪些消息，
排版尽量贴近网页所见 —— 代码块（含语法高亮）、表格、嵌套列表、引用、图片都保留。

**全部在你的浏览器本地完成，对话内容不上传到任何地方。**
详见 [PRIVACY.md](PRIVACY.md)。

> **这个仓库只用来收集反馈，不放源码。** 里面只有这份说明和 Issue 区。遇到问题或
> 想要新功能，[提个 issue](https://github.com/vilalotteria/DaYinGPT/issues)。

## 安装

<!-- TODO: 上架后把下面这行换成商店链接 -->
Chrome 应用商店：*尚未上架*

装好后建议**把插件固定到工具栏**，否则每次都要去拼图图标里翻。

## 怎么用

1. 打开任意一个 ChatGPT 对话
2. 点页面右下角的**导出**按钮（或点工具栏图标 →**选择并导出**）
3. 勾选要导出的消息，上面有**全部 / 提问 / 回答 / 无 / 反选**几个快捷键
4. 需要的话改一下标题，选格式，点**导出**

导出 **PDF** 时会弹出 Chrome 的打印对话框，在**目标打印机**里选**另存为 PDF**。

齿轮 ⚙️ 里有两个选项：**内嵌图片**和 **PDF 页码**。

## 已知问题与常见疑问

### 为什么导出 PDF 会弹打印对话框？

因为这个对话框**就是**生成 PDF 的方式。插件把排好版的文档交给 Chrome 自己的打印
管线，由 Chrome 渲染成 PDF —— 和你在任意网页上按 Ctrl+P 用的是同一个引擎。不上传
任何东西，也没有内置任何 PDF 库。

在对话框里把**目标打印机**选成**另存为 PDF**，并在**更多设置**里勾上**背景图形**
—— 不勾的话代码块的底色会丢掉。

**没有办法让 Chrome 预先选好"另存为 PDF"。** 浏览器不提供任何设置打印目标的接口，
插件替你选不了。唯一能绕开的办法是调用 Chrome 的调试接口直接渲染 PDF，那需要
`debugger` 权限 —— 本插件**特意不申请**：它意味着可以读写任意网页，而且每次导出
Chrome 都会挂出"正在调试此浏览器"的横幅。

好在这是一次性的：**Chrome 会记住你上次选的目标**，第一次选过之后，以后打开对话框
就已经停在"另存为 PDF"上了。

### 图片多的长对话导出很慢

开着**内嵌图片**时，每张图都要单独下载再转成 base64 塞进文件里。几十张图的对话
可能要等几十秒，生成的文件也可能有几十 MB。

进度条上会显示`正在处理图片 x/y`，不是卡死了，是真在跑。

**想快就关掉内嵌图片**（齿轮 ⚙️ 里）。导出几乎瞬间完成、文件也小，但图片会以链接
形式引用 —— 而 ChatGPT 的图片链接会过期，过一阵再打开就是裂图。**要长期存档的
文件，还是开着内嵌等一会儿。**

### 导出的文件名变成乱码，或者下载被别的插件接管

HTML 和 Markdown 导出走的是浏览器的普通下载。如果你装了下载管理器类扩展（IDM、
Chrono、迅雷等），它可能会接管这个下载，把文件名换成一串随机字符。

DaYin GPT 不参与文件名的争夺 —— 多个扩展同时想给一个下载命名时，Chrome 的规则是
**最后安装的那个说了算**。

**绕过办法**：导出前临时停用下载管理器；或者在它的设置里把 `chatgpt.com` 加进
排除列表。

### 图片都跑到消息末尾去了

图片会追加在所属消息的文字之后，而不是还原到原文段落中间的位置。内容不会丢，
但版式和网页上不完全一样。

### 数学公式没有渲染

公式保留 LaTeX 原文，导出的文件里不做渲染。

### 不支持的内容

Canvas 画布，以及深度研究回答里的引用角标。

### 导出 Markdown 时提示找不到源码

Markdown 导出依赖 ChatGPT 自己的后端返回。那个请求失败时，插件会退回到从页面上
抓取，而页面上只有渲染后的 HTML、没有 Markdown 源码。刷新页面重试即可，此时
PDF 和 HTML 不受影响。

## 隐私（一段话版）

插件读对话用的是 ChatGPT 网页版**自己的内部接口** —— 就是你点开一个历史对话时
浏览器本来就会发的那个请求 —— 用的是你当前的登录状态。这个请求是**纯读取**，
**不消耗 token、不产生任何费用**。没有任何内容发给作者或第三方，整个过程不经过
任何服务器。唯一的对外请求是开启图片内嵌时从 OpenAI 的 CDN 下载图片。
完整说明见 [PRIVACY.md](PRIVACY.md)。

## 反馈问题

[提 issue](https://github.com/vilalotteria/DaYinGPT/issues) 时请带上：

- Chrome 版本和操作系统
- 导出的是哪种格式（PDF / HTML / Markdown）
- 当时**内嵌图片**开着还是关着
- 你期望的结果 vs 实际的结果

**请不要把对话内容贴进公开 issue。** 打个码的截图就够了；如果某个问题只有特定内容
才能复现，说一声，我们再想别的办法看。
