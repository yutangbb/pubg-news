# PUBG 新闻 📢

获取 [PUBG 官网](https://pubg.com/news) 最新的新闻公告，支持 iOS Bark 发送通知 。


---

## ✨ 主要功能

- 🔗 使用官网 API 获取新闻公告列表
- 🌐 支持多语言获取并保存到多个 `.json` 文件
- 🔢 自定义获取条数
- 📲 指定语言有更新时通过 [Bark](https://github.com/Finb/Bark) 推送通知到 iOS 设备，支持图标、链接跳转
- 🔍 推送通知支持排除特定关键词，例如 “每周违规账号公示”
- ⏲️ 定时执行 `pubg_news.py` 以自动获取更新和推送通知


---

## 📢 获取新闻公告

此仓库每隔数分钟获取 4 种语言的新闻公告，你可以直接通过下面的 URL 获取最新 10 条新闻公告列表。

> ℹ️ 可能无法按照期望的时间获取数据从而导致延迟更新，这取决于 [Github Actions](https://github.com/yutangbb/pubg-news/actions) 任务执行情况。


| 语言   | URL                                                                       |
| ---- | ------------------------------------------------------------------------- |
| 简体中文 | https://raw.githubusercontent.com/yutangbb/pubg-news/main/news_zh-cn.json |
| 繁体中文 | https://raw.githubusercontent.com/yutangbb/pubg-news/main/news_zh-tw.json |
| 英语   | https://raw.githubusercontent.com/yutangbb/pubg-news/main/news_en.json    |
| 韩语   | https://raw.githubusercontent.com/yutangbb/pubg-news/main/news_ko.json    |

### 通过 jsDelivr CDN 访问
| 语言   | URL                                                                 |
| ---- | ------------------------------------------------------------------- |
| 简体中文 | https://cdn.jsdelivr.net/gh/yutangbb/pubg-news@main/news_zh-cn.json |
| 繁体中文 | https://cdn.jsdelivr.net/gh/yutangbb/pubg-news@main/news_zh-tw.json |
| 英语   | https://cdn.jsdelivr.net/gh/yutangbb/pubg-news@main/news_en.json    |
| 韩语   | https://cdn.jsdelivr.net/gh/yutangbb/pubg-news@main/news_ko.json    |

> ℹ️ 通过 jsDelivr CDN 访问内容有更长时间的更新延迟。


---

## ⚙️ 可配置项（编辑 `pubg-news.py` 顶部）

### 分多种语言获取

```python
# 分多种语言获取新闻列表
LANGUAGES = ["zh-cn", "zh-tw", "en", "ko"]
```
将分多种语言保存到文件：
```
news_zh-cn.json
news_zh-tw.json
news_en.json
news_ko.json
```

### 获取条数
```python
# 获取最新条数
SIZE = 10
```
每次将获取最新 10 条新闻公告，同时最多保存 10 条，建议设置 `10`，设置最大上限为 `50`。

### 指定语言推送通知
```python
LANG = "zh-cn"
```
获取指定语言时，有更新的内容将通过 [Bark](https://github.com/Finb/Bark) 推送通知到 iOS 设备，设置为空则关闭通知。
> ℹ️ 此项设置的语言必须已在 `LANGUAGES` 中设置。

### 排除关键词
```python
EXCLUDE_KEYWORDS = ["每周违规账号公示"]
```
新闻公告标题中包含任意排除关键词则不推送此条。

### 通知标题
```python
BARK_PUSH_TITLE = "PUBG 新闻公告"  
```
通知显示的标题（新闻公告的标题将作为通知内容推送）。

### 通知图标
```python
BARK_PUSH_ICON = "https://wstatic-prod.pubg.com/web/live/static/favicons/apple-icon-180x180.png"  
```
通知显示的图标，建议使用官网图标（默认）。

<img src="https://wstatic-prod.pubg.com/web/live/static/favicons/apple-icon-180x180.png" width="60" />

图标效果

### Bark 推送 URL
```python
BARK_PUSH_URL = "https://api.day.app/你的Key"
```
本地运行时设置 Bark 推送 URL , 请设置为 `https://api.day.app/你的Key`。

> ⚠️ 注意：包含你的 Bark 推送密钥，代码在 Github 仓库或任何公开场景请勿设置！

#### 使用环境变量
```bash
export BARK_PUSH_URL=https://api.day.app/你的Key/
```
> 程序会优先使用 `BARK_PUSH_URL` 环境变量中的 Bark 推送 URL。

#### [GitHub Actions 设置环境变量](#2-在-secrets-中设置-bark_push_url-变量)

---

## ☁️ GitHub Actions 自动化

### 1. Fork 本仓库
点击右上角的 “Fork” 按钮，将项目复制到你自己的 GitHub 账户中。

### 2. 在 Secrets 中设置 BARK_PUSH_URL 变量

在你的 GitHub 仓库中打开：

> **Settings → Secrets → Actions**

找到 `Repository secrets` 面板，点击右侧 <kbd>New repository secret</kbd> 按钮添加：

Name *
```
BARK_PUSH_URL
```
Secret *
```
https://api.day.app/你的Key/
```
填写你的 Bark 推送 URL。

### 3. 配置定时任务

你可以在 `.github/workflows/pubg-news.yml` 文件中修改配置：

```yaml
schedule:
  - cron: '*/10 * * * *'  # 每 10 分钟执行一次
```

也可以手动点击 Actions 页面右上角 **Run workflow** 立即执行一次。

---

## 📝 许可

MIT License.  

> 本项目与 PUBG/KRAFTON 无任何官方关联，仅供学习与非商业用途使用。
> 
> PUBG 及相关标识是 PUBG Corp. 或其关联公司的商标。