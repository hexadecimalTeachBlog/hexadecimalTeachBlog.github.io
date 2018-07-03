## hexo-theme-skapp

### 項目簡介

項目為 hexo 主題 skapp。

附上預覽地址： [demo][demo]

#### 主題效果
    
![screenshot][screenshot]

#### 語言支持

主題默認支持 `zh-cn`、`en` 兩種語言，有需要其它語言的可以自行擴展，將相應語言寫成 yml 文件放置於主題下的 `languages` 文件下。

### 使用方式

基本的 hexo 博客搭建請參照 [hexo官網][hexo]，配置完 hexo 項目後再進行下面的操作。

> 以下操作均默認當前路徑為 hexo 博客項目目錄，請自行進入項目中。

**注意**：**目前nodejieba2.2.5在node10版本中build會報錯，nodejieba2.2.6已經修復了該bug，但是lunr仍然使用的是nodejieba2.2.5.因此建議使用node LTS版本,比如8.9.3** 

使用 git 將主題 clone 至你的 hexo 博客項目下的 themes 文件夾下

``` shell
cd themes && git clone https://github.com/Mrminfive/hexo-theme-skapp.git
```

clone 完後將根目錄下的 `_config.yml` 文件中的 `theme` 字段設置為 `hexo-theme-skapp`，同時安裝對應 node 依賴：

``` shell
npm install --save hexo-autoprefixer hexo-filter-cleanup hexo-generator-feed hexo-generator-sitemap hexo-renderer-sass hexo-renderer-swig mamboer/lunr.js moment node-sass object-assign
```

**注意**：如果安裝失敗可嘗試用 cnpm 進行安裝。另外，由於使用 `nodejieba` 分詞庫，所以 windows 下用戶應提前安裝好相應編譯環境。操作如下：

``` shell
npm install -g windows-build-tools
npm install -g node-gyp
```

(確認 `PATH` 中 `python` 路徑是否設置。)

安裝完依賴後將以下配置寫入根目錄下的 `_config.yml` 文件中

``` yml
# Sass
node_sass:
  outputStyle: nested
  precision: 5
  sourceComments: false

# Autoprefixer
autoprefixer:
  exclude:
    - '*.min.css'
  browsers:
    - 'last 2 versions'

# Lunr
lunr:
  field: all
  fulltext: false
  path: assets/lunr/

# filter_cleanup
hfc_useref:
  enable: true
  concat: true

hfc_html:
  enable: true
  exclude:

hfc_css:
  enable: true
  exclude: 
    - '*.min.css'

hfc_js:
  enable: true
  mangle: true
  exclude: 
    - '*.min.js'

hfc_img:
  enable: false
  interlaced: false
  multipass: false
  optimizationLevel: 2
  pngquant: false
  progressive: false

hfc_favicons:
  enable: false
  src: img/blog-logo.png
  target: img/
  icons:
    android: true
    appleIcon: true
    appleStartup: false
    coast: false
    favicons: true
    firefox: false
    opengraph: false
    windows: true
    yandex: false
```

ok，走到這一步主題編譯需要的環境配置完了，可以使用 `hexo s --debug` 進行本地預覽了。

*注：*如果樣式生成失敗，請用 `hexo clean` 清除下緩存後在 `hexo s --debug`。

*注：*如果調試時遇到缺少某些js文件(404error)，使用`hexo s`來替代`hexo s --debug`來調試
### 主題配置

#### 設置語言

編輯根 `_config.yml` 文件，將 `language` 設置為你想要的語言：

``` yml
language: zh-cn
```

目前主題支持的語言如下：

| 語言     |  代碼  |
| ------- | ----- |
| English | en |
| 簡體中文 | zh-cn |

#### 設置菜單

編輯根 `_config.yml` 文件，將 `menu` 設置為如下：

``` yml
menu:
  home: / 
  archive: /archives
  about: /about
```

主題默認的菜單項有：

| 鍵值 | 設定值 | 顯示文本（簡體中文）|
| --- | ----- | ---------------- |
| home | home: / | 首頁 |
| archive | archive: /archives | 歸檔 |
| about | about: /about | 關於 |
| search | search: /search | 搜索頁 | 

其中 `about`、`search` 與主題內置的 `404` 頁面一樣需要手動創建，創建方式如下：

創建 about 頁面：

``` shell
hexo new page about
```

然後編輯 source 文件夾下的 about 文件夾中的 index.md 文件：

``` md
---
title: 關於
date: 2017-07-29 00:50:51
type: about
layout: about
---

...(以下內容將渲染在關於頁面中)
```

創建 search 頁面：

``` shell
hexo new page search
```

然後編輯 source 文件夾下的 search 文件夾中的 index.md 文件：

``` md
---
title: 關於
date: 2017-07-29 00:50:51
type: search
layout: search
---
```

404 頁面則直接在 source 目錄下創建 404.md 文件，文件內容如下：

``` md
---
title: 404 Page Not Found
date: 2017-08-04 23:36:59
type: error
layout: error
---
```

#### 博客信息配置

以下配置均在根 `_config.yml` 中：

``` yml
# Site
# 博客的標題
title: MINFIVE

# banner顯示的子標題
subtitle: MINFIVE BLOG

# banner顯示的簡短介紹
subtitle_desc: 日常學習與興趣交流

# seo關鍵字
keywords: minfive, minfive blog, 前端博客, 前端, 程序員, 前端開發, 全棧開發, node.js, javascript

# 博客介紹（同時用於seo）
description: 日常學習與興趣交流的個人博客

# 個人介紹
introduction: 不思量，自難忘！

# 博客的favicon圖標，支持本地及在線兩種方式，本地請將圖標放置於 themes/hexo-theme-skapp/source/img 目錄下
favicon_ico: http://oo12ugek5.bkt.clouddn.com/blog/images/favicon.ico

# 博客的左上角logo圖標，支持本地及在線兩種方式
logo: http://oo12ugek5.bkt.clouddn.com/images/logo-text-white.png

# 頭像/二維碼（用於顯示在底部）二選一
avatar: http://oo12ugek5.bkt.clouddn.com/images/qrcode.png
# qrcode: http://oo12ugek5.bkt.clouddn.com/images/qrcode.png

# 文章的默認封面
default_cover: http://oo12ugek5.bkt.clouddn.com/images/default_cover.png

# header 的背景圖
header_cover: http://oo12ugek5.bkt.clouddn.com/blog/images/banner-bg.jpg

# 404 頁面的背景圖
error_page_bg: http://oo12ugek5.bkt.clouddn.com/blog/images/dogs.jpg

# 頁面加載loading圖標
loader_img: http://oo12ugek5.bkt.clouddn.com/blog/images/loader.gif

# 站長信息
author:
  name: minfive
  link: https://github.com/Mrminfive
# 用於頁面 footer 的站長信息
about:
  info: 本站是基於 Hexo 搭建的靜態資源博客，主要用於分享日常學習、生活及工作的一些心得總結，歡迎點擊右下角訂閱 rss。
  address: Guangzhou, Guangdong Province, China
  email: chenxiaowu1994@outlook.com
```

#### 聯繫方式

在 `/source/_data` 目錄下創建 `contact.yml` 文件將在頁面底部生成相應的標籤鏈接，如：

![contact-img][contact-img]

配置內容如下：

``` yml
- title: github
  icon: icon-github
  link: https://github.com/Mrminfive
- title: email
  icon: icon-email
  link: mailto:chenxiaowu1994@outlook.com
- title: rss
  icon: icon-rss
  link: /atom.xml
```

其中 `title` 表示鏈接的 `title` 值，`icon` 表示使用css圖標，`link` 表示跳轉的鏈接。

`icon` 僅支持如下值：

* `icon-email`: 郵箱
* `icon-rss`: rss
* `icon-in`: linkedin
* `icon-twitter`: twitter
* `icon-facebook`: facebook
* `icon-github`: github
* `icon-zhihu`: 知乎
* `icon-douban`: 豆瓣
* `icon-weibo`: 微博
* `icon-telegram`: telegram

#### 外部鏈接

在 `source/_data` 目錄下創建 `footer_link.yml` 文件將在頁面底部生成相應的外部鏈接列表，如：

![footer-link][footer-link]

配置內容如下：

```
friend_links:
  - name: hexo-theme-skapp
    desc: hexo-theme-skapp
    link: https://github.com/Mrminfive/hexo-theme-skapp

build_tools:
  - name: Hexo
    desc: Blog Framework
    link: https://hexo.io/
```

其中 `name` 表示鏈接的顯示值，`desc` 表示鏈接的 `title` 值，`link` 表示跳轉的鏈接。

該文件中的每一個數組代表一列鏈接，數據的key 值代表對應該列的標題，如：`friend_links` 對應 `友情鏈接`，同時允許設置多列鏈接，只需要在 `hexo-theme-skapp/languages` 下的語言配置中設置好相應的對照值即可。


#### 個性化配置

主題使用 sass 預編譯樣式，筆者將所有基本樣式參數封裝在 `hexo-theme-skapp/source/scss` 下的 `_theme.scss` 文件文件中：

``` scss
/**
 * blog theme 
 */

$main-color: #19abd6                                !default;
$main-color--hover: lighten($main-color, 10%)       !default;

$font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,"PingFang SC","Lantinghei SC","Microsoft Yahei","Hiragino Sans GB","Microsoft Sans Serif","WenQuanYi Micro Hei",sans           !default;

$main-fc: #666                                      !default;
$main-fs: 14px                                      !default;
$main-lh: 1.7                                       !default;

$title-fc: #242f35                                  !default;

$hint-fc: #19abd6                                   !default;

$bgc--main: #fff                                    !default;
$bgc--bottom: #2d383e                               !default;
$bgc--footer: #242f35                               !default;

$border-c: #d8e5f3                                  !default;

$transition: .3s                                    !default;

$mq-desktop--wide: 1280px                           !default;
$mq-desktop: 980px                                  !default;
$mq-mobile: 736px                                   !default;

$pad: 15px                                          !default;

$z-index--bottom: 1                                 !default;
$z-index--center: 50                                !default;
$z-index--top: 100                                  !default;
```

有興趣的可以自行修改。

#### 基本使用
每篇文章的基本配置如下：
```
title: Hello World 
cover: http://oxnuwmm3w.bkt.clouddn.com/hello-world.jpeg
author: 
  nick: BruceYJ
  link: https://www.github.com/BruceYuj

# 如果文章為轉載文章，需要多加文章出處項
editor:
  name: Minfive
  link: https://www.github.com/Mrminfive

# 首頁每篇文章的子標題
subtitle: your subtitle
```
title為文章的標題，cover為文章的首圖和縮略圖，author為文章的作者信息。

#### 第三方服務

##### 統計

###### 百度統計

主題已集成百度統計，使用百度統計僅需要獲取百度統計的腳本id並將其配置到根 `_config.yml` 中：

``` yml
# Baidu statistic
baidu_statistic: e3267498201dfa9699a5c509424709d6
```

###### 谷歌統計

主題已集成谷歌統計，使用谷歌統計僅需要獲取谷歌統計的腳本id並將其配置到根 `_config.yml` 中：

``` yml
# Google statistic
google_statistic: UA-108468870-1
```

##### 不蒜子統計

主題使用不蒜了統計文章pv，默認不開啟，可在根 `_config.yml` 配置開啟:

``` yml
# Busuanzi
busuanzi: true
```

##### 內容搜索

主題使用 lunr 進行站內檢索，暫不支持配置。

##### rss

將如下代碼寫入根 `_config.yml` 中：

``` yml
# Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20

# Sitemap
sitemap:
  path: sitemap.xml
```

##### 評論系統

###### gitalk

主題集成 [gitalk][gitalk] 作為評論功能。開啟評論功能需要註冊 Github Application，具體請參照 [gitalk文檔][gitalk doc]，申請完後在根 `_config.yml` 配置：

``` yml
# Gitalk
gitTalk:
  clientId: ***
  clientSecret: ***
  repo: ***
  owner: ***
  admin: 
    - ***
```

###### disqus

主題集成 [disqus][disqus] 作為評論功能。開啟此評論功能請註冊 Disqus 站點，具體參照官方指引，申請完成後在根 `_config.yml` 配置：

``` yml
# Disqus

disqus_shortname: ***
```

#### 數學公式渲染

主題集成[hexo-math][math]顯示數學公式，默認不開啟。在主題目錄 `_config.yml` 中配置：

```yml
# Math Equations Render Support
math:
  enable: true

  # Default(true) will load mathjax/katex script on demand
  # That is it only render those page who has 'mathjax: true' in Front Matter.
  # If you set it to false, it will load mathjax/katex srcipt EVERY PAGE.
  per_page: false

  engine: mathjax
  #engine: katex

  # hexo-rendering-pandoc (or hexo-renderer-kramed) needed to full MathJax support.
  mathjax:
    # Use 2.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/mathjax@2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For newMathJax CDN (cdnjs.cloudflare.com) with fallback to oldMathJax (cdn.mathjax.org).
    #cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For direct link to MathJax.js with CloudFlare CDN (cdnjs.cloudflare.com).
    #cdn: //cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML
    # For automatic detect latest version link to MathJax.js and get from Bootcss.
    #cdn: //cdn.bootcss.com/mathjax/2.7.1/latest.js?config=TeX-AMS-MML_HTMLorMML

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin)
  # needed to full Katex support.
  katex:
    # Use 0.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/katex@0.7.1/dist/katex.min.css
    # CDNJS, provided by cloudflare, maybe the best CDN, but not works in China
    #cdn: //cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.css
    # Bootcss, works great in China, but not so well in other region
    #cdn: //cdn.bootcss.com/KaTeX/0.7.1/katex.min.css
```


[demo]: http://blog.minfive.com/
[screenshot]: http://oo12ugek5.bkt.clouddn.com/blog/images/17-09-17/hexo-theme-skapp-screenshot.png
[hexo]: https://hexo.io/zh-cn/
[gitalk]: https://github.com/gitalk/gitalk
[gitalk doc]: https://github.com/gitalk/gitalk#usage
[contact-img]: http://oo12ugek5.bkt.clouddn.com/blog/images/17-09-17/hexo-theme-skapp-contact.png
[footer-link]: http://oo12ugek5.bkt.clouddn.com/blog/images/17-09-17/hexo-theme-skapp-footer.png
[disqus]: https://disqus.com/
[math]: https://github.com/hexojs/hexo-math
