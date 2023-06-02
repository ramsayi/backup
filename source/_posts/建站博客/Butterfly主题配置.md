---
title: Butterfly主题配置
tags:
  - 博客
  - Hexo
  - Butterfly
categories:
  - 建站博客
swiper_index: 5
swiper_desc: 不设置点击动画和动态背景，对性能影响比较大，会卡顿。
swiper_cover: '/assets/img/post/hexo-theme-butterfly.webp'
abbrlink: 23ce82cf
date: 2021-09-08 19:39:20
---

> 版本 4.2.0-b1

## 前言

Butterfly主题设置了首页图片后会明显卡顿，并且在重载或移动的时候，页面会疯狂变换形态，所以直接去掉了主页图片。
页面内的banner图片全部替换为最大 1920*1080px 图片，格式为Google推荐的webp，质量80%，压缩方法4，滤镜强度60%，滤镜锐度0。
不设置点击动画和动态背景，对性能影响比较大，会卡顿。
不设置aplayer音乐播放器，全局吸底时，手机端看起来像广告。设置自动播放又吵人。

## Hexo博客 `.yml` 文件修改

```yaml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: 𝙍𝙖𝙢𝙨𝙖𝙮𝙞'𝙨 𝘽𝙡𝙤𝙜
subtitle: 
description: ''
keywords:
author: Ramsayi
language: zh-CN
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://ramsayi.github.io
permalink: posts/:abbrlink/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link:
  enable: true # Open external links in new tab
  field: site # Apply to the whole site
  exclude: ''
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: false
  preprocess: true
  line_number: true
  tab_replace: ''

# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date

# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Metadata elements
## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta
meta_generator: true

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss
## updated_option supports 'mtime', 'date', 'empty'
updated_option: 'mtime'

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Include / Exclude file(s)
## include:/exclude: options only apply to the 'source/' folder
include:
exclude:
ignore:

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: butterfly3

# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: 
    github: https://github.com/ramsayi/ramsayi.github.io.git
  branch: master

# 豆瓣
douban:
  user: 194612089
  builtin: false
  book:
    title: 'This is my book title'
    quote: 'This is my book quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: books
    limit:
  movie:
    title: 'This is my movie title'
    quote: 'This is my movie quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: movies
    limit:
  game:
    title: 'This is my game title'
    quote: 'This is my game quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: games
    limit:
  timeout: 10000 

# abbrlink config
abbrlink:
  alg: crc32  #算法: crc16(default) and crc32
  rep: hex    #进制: dec(default) and hex

# Ice Kano Plus_in
# Hexo Github Canlendar
# Author: Ice Kano
# Modify: Lete乐特
githubcalendar:
  enable: true
  priority: 3
  enable_page: /
  user: ramsayi
  layout:
    type: id
    name: recent-posts
    index: 0
  githubcalendar_html: '<div class="recent-post-item" style="width:100%;height:auto;padding:10px;"><div id="github_loading" style="width:10%;height:100%;margin:0 auto;display: block"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"  viewBox="0 0 50 50" style="enable-background:new 0 0 50 50" xml:space="preserve"><path fill="#d0d0d0" d="M25.251,6.461c-10.318,0-18.683,8.365-18.683,18.683h4.068c0-8.071,6.543-14.615,14.615-14.615V6.461z" transform="rotate(275.098 25 25)"><animateTransform attributeType="xml" attributeName="transform" type="rotate" from="0 25 25" to="360 25 25" dur="0.6s" repeatCount="indefinite"></animateTransform></path></svg></div><div id="github_container"></div></div>'
  pc_minheight: 280px
  mobile_minheight: 0px
  color: "['#f3f5ff', '#ccd4ff', '#a5b3ff', '#7e91fe', '#5770fe', '#304ffe', '#092efe', '#0122de', '#011cb7', '#011690', '#011069']"
  api: https://python-github-calendar-api.vercel.app/api
  # api: https://python-gitee-calendar-api.vercel.app/api
  calendar_js: https://cdn.jsdelivr.net/gh/Zfour/hexo-github-calendar@1.21/hexo_githubcalendar.js
  plus_style: ""

magnet:
  enable: true
  priority: 2
  enable_page: all
  type: categories
  devide: 2
  display:
    - name: 博客
      display_name: Ramsayiの魔改教程
      icon: 📚
    - name: 游戏
      display_name: Ramsayiの游戏修改
      icon: 🎮
    - name: 生活
      display_name: Ramsayiの生活趣闻
      icon: 🎉
    - name: 编程
      display_name: Ramsayiの编程学习
      icon: 👩‍💻
    - name: 书籍
      display_name: Ramsayiの读书笔记
      icon: 📒
    - name: 随想
      display_name: Ramsayiの胡思乱想
      icon: 💡
  color_setting:
    text_color: black
    text_hover_color: white
    background_color: "#f2f2f2"
    background_hover_color: "#304FFE"
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="width:100%;height: auto"><div id="catalog_magnet">${temple_html_item}</div></div>'
  plus_style: ""

swiper:
  enable: true
  priority: 1
  enable_page: /
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="height: auto;width: 100%"><div class="blog-slider swiper-container-fade swiper-container-horizontal" id="swiper_container">${temple_html_item}</div></div>'
  plus_style: ""
```



## Butterfly主题 `.yml` 文件修改

```yaml
blackandwhite: false

# Main menu navigation (導航目錄)
# see https://butterfly.js.org/posts/4aa8abbe/#導航菜單
# --------------------------------------

menu:
  首页: / || fas fa-home
  归档: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  清单||fa fa-heartbeat:
    音乐: /music/ || fas fa-music
    照片: /gallery/ || fas fa-images
    电影: /movies/ || fas fa-video
  其他||fas fa-chevron-circle-down:
    Scabet: //scabet.github.io/ || fas fa-compass
    网址导航: //aabbk.github.io/ || fas fa-compass
    小游戏: //aabbs.github.io/ || fas fa-compass
    Aabbt: //aabbt.github.io/ || fas fa-compass
    SWClub: //swclub.github.io/ || fas fa-compass
  友链: /link/ || fas fa-link
  关于: /about/ || fas fa-heart

# Code Blocks (代碼相關)
# --------------------------------------

highlight_theme: mac #  darker / pale night / light / ocean / mac / mac light / false
highlight_copy: true # copy button
highlight_lang: true # show the code language
highlight_shrink: false # true: shrink the code blocks / false: expand the code blocks | none: expand code blocks and hide the button
highlight_height_limit: false # unit: px
code_word_wrap: false

# copy settings
# copyright: Add the copyright information after copied content (複製的內容後面加上版權信息)
copy:
  enable: true
  copyright:
    enable: false
    limit_count: 50

# social settings (社交圖標設置)
# formal:
#   icon: link || the description
social:
  fab fa-github: https://github.com/ramsayi || Github
  fas fa-envelope: mailto:ramsayi726@gmail.com || Email
  fab fa-qq: https://qm.qq.com/cgi-bin/qm/qr?k=zJMwaNu8TejipA9mfddmkCBmSDYxgINU&noverify=0 || QQ
  fab fa-zhihu: https://www.zhihu.com/people/zhu-meng-zl || 知乎

# search (搜索)
# --------------------------------------

# Algolia search
algolia_search:
  enable: false
  hits:
    per_page: 6

# Local search
local_search:
  enable: true

# Math (數學)
# --------------------------------------
# About the per_page
# if you set it to true, it will load mathjax/katex script in each page (true 表示每一頁都加載js)
# if you set it to false, it will load mathjax/katex script according to your setting (add the 'mathjax: true' in page's front-matter)
# (false 需要時加載，須在使用的 Markdown Front-matter 加上 mathjax: true)

# MathJax
mathjax:
  enable: false
  per_page: false

# KaTeX
katex:
  enable: false
  per_page: false
  hide_scrollbar: true

# Image (圖片設置)
# --------------------------------------

# Favicon（網站圖標）
favicon: /assets/img/logo/logo_2.png

# Avatar (頭像)
avatar:
  img: /assets/img/logo/avatar.jpg
  effect: false

# Disable all banner image
disable_top_img: false

# The banner image of home page
index_img: /assets/img/bg/bg/1003.jpg

# If the banner of page not setting, it will show the top_img
default_top_img: /assets/img/bg/bg/1003.jpg

# The banner image of archive page
archive_img: /assets/img/bg/bg/1003.jpg

# If the banner of tag page not setting, it will show the top_img
# note: tag page, not tags page (子標籤頁面的 top_img)
tag_img: /assets/img/bg/bg/1003.jpg

# The banner image of tag page
# format:
#  - tag name: xxxxx
tag_per_img:

# If the banner of category page not setting, it will show the top_img
# note: category page, not categories page (子分類頁面的 top_img)
category_img: /assets/img/bg/bg/1003.jpg

# The banner image of category page
# format:
#  - category name: xxxxx
category_per_img:

cover:
  # display the cover or not (是否顯示文章封面)
  index_enable: true
  aside_enable: true
  archives_enable: true
  # the position of cover in home page (封面顯示的位置)
  # left/right/both
  position: left
  # When cover is not set, the default cover is displayed (當沒有設置cover時，默認的封面顯示)
  default_cover:
    - /assets/img/bg/cover/0001.jpg
    - /assets/img/bg/cover/0002.jpg
    - /assets/img/bg/cover/0003.jpg
    - /assets/img/bg/cover/0004.jpg
    - /assets/img/bg/cover/0005.jpg
    - /assets/img/bg/cover/0006.jpg
    - /assets/img/bg/cover/0007.jpg
    - /assets/img/bg/cover/0008.jpg
    - /assets/img/bg/cover/0009.jpg
    - /assets/img/bg/cover/0010.jpg
    - /assets/img/bg/cover/0011.jpg
    - /assets/img/bg/cover/0012.jpg
    - /assets/img/bg/cover/0013.jpg
    - /assets/img/bg/cover/0014.jpg
    - /assets/img/bg/cover/0015.jpg
    - /assets/img/bg/cover/0016.jpg

# Replace Broken Images (替換無法顯示的圖片)
error_img:
  flink: /img/friend_404.gif
  post_page: /img/404.jpg

# A simple 404 page
error_404:
  enable: true
  subtitle: 'Page Not Found'
  background: /assets/img/404/404.svg

post_meta:
  page: # Home Page
    date_type: both # created or updated or both 主頁文章日期是創建日或者更新日或都顯示
    date_format: date # date/relative 顯示日期還是相對日期
    categories: true # true or false 主頁是否顯示分類
    tags: false # true or false 主頁是否顯示標籤
    label: true # true or false 顯示描述性文字
  post:
    date_type: both # created or updated or both 文章頁日期是創建日或者更新日或都顯示
    date_format: date # date/relative 顯示日期還是相對日期
    categories: true # true or false 文章頁是否顯示分類
    tags: true # true or false 文章頁是否顯示標籤
    label: true # true or false 顯示描述性文字

# wordcount (字數統計)
wordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true

# Display the article introduction on homepage
# 1: description
# 2: both (if the description exists, it will show description, or show the auto_excerpt)
# 3: auto_excerpt (default)
# false: do not show the article introduction
index_post_content:
  method: 3
  length: 500 # if you set method to 2 or 3, the length need to config

# anchor
# when you scroll in post, the URL will update according to header id.
anchor: false

# Post
# --------------------------------------

# toc (目錄)
toc:
  post: true
  page: false
  number: false
  expand: false
  style_simple: false # for post

post_copyright:
  enable: true
  decode: false
  license: CC BY-NC-SA 4.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/

# Sponsor/reward
reward:
  enable: false
  QR_code:
    - img: /img/wechat.jpg
      link:
      text: wechat
    - img: /img/alipay.jpg
      link:
      text: alipay

# Post edit
# Easily browse and edit blog source code online.
post_edit:
  enable: false
  # url: https://github.com/user-name/repo-name/edit/branch-name/subdirectory-name/
  # For example: https://github.com/jerryc127/butterfly.js.org/edit/main/source/
  url:

# Related Articles
related_post:
  enable: true
  limit: 6 # Number of posts displayed
  date_type: created # or created or updated 文章日期顯示創建日或者更新日

# figcaption (圖片描述文字)
photofigcaption: false

# post_pagination (分頁)
# value: 1 || 2 || false
# 1: The 'next post' will link to old post
# 2: The 'next post' will link to new post
# false: disable pagination
post_pagination: 1

# Displays outdated notice for a post (文章過期提醒)
noticeOutdate:
  enable: ture
  style: flat # style: simple/flat
  limit_day: 365 # When will it be shown
  position: top # position: top/bottom
  message_prev: It has been
  message_next: days since the last update, the content of the article may be outdated.

# Share System (分享功能)
# --------------------------------------

# AddThis
# https://www.addthis.com/
addThis:
  enable: false
  pubid:

# Share.js
# https://github.com/overtrue/share.js
sharejs:
  enable: true
  sites: facebook,twitter,wechat,weibo,qq

# AddToAny
# https://www.addtoany.com/
addtoany:
  enable: false
  item: facebook,twitter,wechat,sina_weibo,facebook_messenger,email,copy_link

# Comments System
# --------------------------------------

comments:
  # Up to two comments system, the first will be shown as default
  # Choose: Disqus/Disqusjs/Livere/Gitalk/Valine/Waline/Utterances/Facebook Comments/Twikoo/Giscus
  use: Valine # Valine,Disqus
  text: true # Display the comment name next to the button
  # lazyload: The comment system will be load when comment element enters the browser's viewport.
  # If you set it to true, the comment count will be invalid
  lazyload: true
  count: true # Display comment count in post's top_img
  card_post_count: true # Display comment count in Home Page

# disqus
# https://disqus.com/
disqus:
  shortname:
  apikey: # For newest comments widget

# Alternative Disqus - Render comments with Disqus API
# DisqusJS 評論系統，可以實現在網路審查地區載入 Disqus 評論列表，兼容原版
# https://github.com/SukkaW/DisqusJS
disqusjs:
  shortname:
  apikey:
  option:

# livere (來必力)
# https://www.livere.com/
livere:
  uid:

# gitalk
# https://github.com/gitalk/gitalk
gitalk:
  client_id:
  client_secret:
  repo:
  owner:
  admin:
  option:

# valine
# https://valine.js.org
valine:
  appId: hYhAkaCoGek8gsKP8H2vLfmS-gzGzoHsz # leancloud application app id
  appKey: 8Cxp5qHQuHTnuUIsOuPqWoQk # leancloud application app key
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  serverURLs: # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
  bg: # valine background
  visitor: false
  option:

# waline - A simple comment system with backend support fork from Valine
# https://waline.js.org/
waline:
  serverURL: # Waline server address url
  bg: # waline background
  visitor: false
  option:

# utterances
# https://utteranc.es/
utterances:
  repo:
  # Issue Mapping: pathname/url/title/og:title
  issue_term: pathname
  # Theme: github-light/github-dark/github-dark-orange/icy-dark/dark-blue/photon-dark
  light_theme: github-light
  dark_theme: photon-dark

# Facebook Comments Plugin
# https://developers.facebook.com/docs/plugins/comments/
facebook_comments:
  app_id:
  user_id: # optional
  pageSize: 10 # The number of comments to show
  order_by: social # social/time/reverse_time
  lang: en_US # Language en_US/zh_CN/zh_TW and so on

# Twikoo
# https://github.com/imaegoo/twikoo
twikoo:
  envId:
  region:
  visitor: false
  option:

# Giscus
# https://giscus.app/
giscus:
  repo:
  repo_id:
  category_id:
  theme:
    light: light
    dark: dark
  option:

# Chat Services
# --------------------------------------

# Chat Button [recommend]
# It will create a button in the bottom right corner of website, and hide the origin button
chat_btn: true

# The origin chat button is displayed when scrolling up, and the button is hidden when scrolling down
chat_hide_show: true

# chatra
# https://chatra.io/
chatra:
  enable: false
  id: 9nyHzPKA34yBkiihn

# tidio
# https://www.tidio.com/
tidio:
  enable: true
  public_key: fxk9glqedvgfb9eqhzyajcc3o4oupxbo

# daovoice
# http://daovoice.io/
daovoice:
  enable: false
  app_id:

# gitter
# https://gitter.im/
gitter:
  enable: false
  room:

# crisp
# https://crisp.chat/en/
crisp:
  enable: false
  website_id:

# Footer Settings
# --------------------------------------
footer:
  owner:
    enable: true
    since: 2018
  custom_text: <a href="https://www.gushici.com/t_782">满堂花醉三千客，一剑霜寒十四州</a>
  copyright: true # Copyright of theme and framework

# Analysis
# --------------------------------------

# Baidu Analytics
# https://tongji.baidu.com/web/welcome/login
baidu_analytics:

# Google Analytics
# https://analytics.google.com/analytics/web/
google_analytics:

# CNZZ Analytics
# https://www.umeng.com/
cnzz_analytics:

# Cloudflare Analytics
# https://www.cloudflare.com/zh-tw/web-analytics/
cloudflare_analytics:

# Microsoft Clarity
# https://clarity.microsoft.com/
microsoft_clarity:

# Advertisement
# --------------------------------------

# Google Adsense (谷歌廣告)
google_adsense:
  enable: false
  auto_ads: true
  js: https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js
  client:
  enable_page_level_ads: true

# Insert ads manually (手動插入廣告)
# ad:
#   index:
#   aside:
#   post:

# Verification (站長驗證)
# --------------------------------------

site_verification:
  # - name: google-site-verification
  #   content: xxxxxx
  # - name: baidu-site-verification
  #   content: xxxxxxx

# Beautify/Effect (美化/效果)
# --------------------------------------

# Theme color for customize
# Notice: color value must in double quotes like "#000" or may cause error!

theme_color:
  enable: true
  main: "#304FFE" # Indigo 1
  paginator: "#8C9EFF" # Indigo 2
  button_hover: "#B388FF" # Deep purple 3 2
  text_selection: "#8C9EFF" # Indigo 2
  link_color: "#304FFE" # Indigo 1
  meta_color: "#858585"
  hr_color: "#A4D8FA"
  code_foreground: "#651FFF" # Deep purple 3
  code_background: "rgba(27, 31, 35, .05)"
  toc_color: "#304FFE" # Indigo 1
  blockquote_padding_color: "#304FFE" # Indigo 1
  blockquote_background_color: "#304FFE" # Indigo 1

# The top_img settings of home page
# default: top img - full screen, site info - middle (默認top_img全屏，site_info在中間)
# The position of site info, eg: 300px/300em/300rem/10% (主頁標題距離頂部距離)
index_site_info_top:
# The height of top_img, eg: 300px/300em/300rem (主頁top_img高度)
index_top_img_height:

# The user interface setting of category and tag page (category和tag頁的UI設置)
# index - same as Homepage UI (index 值代表 UI將與首頁的UI一樣)
# default - same as archives UI 默認跟archives頁面UI一樣
category_ui: # 留空或 index
tag_ui: # 留空或 index

# Website Background (設置網站背景)
# can set it to color or image (可設置圖片 或者 顔色)
# The formal of image: url(http://xxxxxx.com/xxx.jpg)
background: url(/assets/img/bg/bg/1003.jpg)

# Footer Background
footer_bg: false

# the position of 3 right button/default unit: px (右下角按鈕距離底部的距離/默認單位為px)
rightside-bottom:

# Enter transitions (開啓網頁進入效果)
enter_transitions: true

# Background effects (背景特效)
# --------------------------------------

# canvas_ribbon (靜止彩帶背景)
# See: https://github.com/hustcc/ribbon.js
canvas_ribbon:
  enable: false
  size: 150
  alpha: 0.6
  zIndex: -1
  click_to_change: false
  mobile: false

# Fluttering Ribbon (動態彩帶)
canvas_fluttering_ribbon:
  enable: false
  mobile: false

# canvas_nest
# https://github.com/hustcc/canvas-nest.js
canvas_nest:
  enable: false
  color: '0,0,255' #color of lines, default: '0,0,0'; RGB values: (R,G,B).(note: use ',' to separate.)
  opacity: 0.7 # the opacity of line (0~1), default: 0.5.
  zIndex: -1 # z-index property of the background, default: -1.
  count: 99 # the number of lines, default: 99.
  mobile: false

# Typewriter Effect (打字效果)
# https://github.com/disjukr/activate-power-mode
activate_power_mode:
  enable: false
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖動特效)
  mobile: false

# Mouse click effects: fireworks (鼠標點擊效果: 煙火特效)
fireworks:
  enable: true
  zIndex: 9999 # -1 or 9999
  mobile: false

# Mouse click effects: Heart symbol (鼠標點擊效果: 愛心)
click_heart:
  enable: false
  mobile: false

# Mouse click effects: words (鼠標點擊效果: 文字)
ClickShowText:
  enable: false
  text:
    # - I
    # - LOVE
    # - YOU
  fontSize: 15px
  random: false
  mobile: false

# Default display mode (網站默認的顯示模式)
# light (default) / dark
display_mode: light

# Beautify (美化頁面顯示)
beautify:
  enable: ture
  field: post # site/post
  title-prefix-icon: '\f863'
  title-prefix-icon-color: '#304FFE'

# Global font settings
# Don't modify the following settings unless you know how they work (非必要不要修改)
font:
  global-font-size:
  code-font-size:
  font-family: '霞鹜文楷'
  code-font-family:

# Font settings for the site title and site subtitle
# 左上角網站名字 主頁居中網站名字
blog_title_font:
  font_link:
  font-family:

# The setting of divider icon (水平分隔線圖標設置)
hr_icon:
  enable: true
  icon: # the unicode value of Font Awesome icon, such as '\3423'
  icon-top:

# the subtitle on homepage (主頁subtitle)
subtitle:
  enable: true
  # Typewriter Effect (打字效果)
  effect: true
  # loop (循環打字)
  loop: true
  # source 調用第三方服務
  # source: false 關閉調用
  # source: 1  調用一言網的一句話（簡體） https://hitokoto.cn/
  # source: 2  調用一句網（簡體） http://yijuzhan.com/
  # source: 3  調用今日詩詞（簡體） https://www.jinrishici.com/
  # subtitle 會先顯示 source , 再顯示 sub 的內容
  source: 4
  # 如果關閉打字效果，subtitle 只會顯示 sub 的第一行文字
  sub:
    - 满堂花醉三千客，一剑霜寒十四州。
    - 我本可以忍受黑暗，如果不曾见到光明。
    - 骊山语罢清宵半，泪雨霖铃终不怨。
    - 斜月沉沉藏海雾，碣石潇湘无限路。
    - 草色烟光残照里，无言谁会凭阑意。
    - 世事漫随流水，算来一梦浮生。
    - 夜耿耿而不寐，沾繁霜而至曙。
    - 你遇见一个人，犯了一个错，你想弥补想还清，到最后才发现你根本无力回天，犯下的罪过永远无法弥补，我们永远无法还清欠下的......
    - 人生若只如初见，何事秋风悲画扇？
    - 细雨柔丝霏霏落，槐春阳暖渐渐开。

# Loading Animation (加載動畫)
preloader: false

# aside (側邊欄)
# --------------------------------------

aside:
  enable: true
  hide: false
  button: true
  mobile: true # display on mobile
  position: right # left or right
  card_author:
    enable: true
    description:
    button:
      enable: true
      icon: fab fa-github
      text: 关注
      link: https://github.com/ramsayi
  card_announcement:
    enable: true
    content: 月亮不睡你不睡，医院等你去缴费
  card_recent_post:
    enable: true
    limit: 5 # if set 0 will show all
    sort: date # date or updated
    sort_order: # Don't modify the setting unless you know how it works
  card_categories:
    enable: true
    limit: 8 # if set 0 will show all
    expand: none # none/true/false
    sort_order: # Don't modify the setting unless you know how it works
  card_tags:
    enable: true
    limit: 40 # if set 0 will show all
    color: true
    sort_order: # Don't modify the setting unless you know how it works
  card_archives:
    enable: true
    type: monthly # yearly or monthly
    format: MMMM YYYY # eg: YYYY年MM月
    order: -1 # Sort of order. 1, asc for ascending; -1, desc for descending
    limit: 8 # if set 0 will show all
    sort_order: # Don't modify the setting unless you know how it works
  card_webinfo:
    enable: true
    post_count: true
    last_push_date: true
    sort_order: # Don't modify the setting unless you know how it works

# busuanzi count for PV / UV in site
# 訪問人數
busuanzi:
  site_uv: true
  site_pv: true
  page_pv: true

# Time difference between publish date and now (網頁運行時間)
# Formal: Month/Day/Year Time or Year/Month/Day Time
runtimeshow:
  enable: true
  publish_date: 2018/1/1 00:00:00

# Aside widget - Newest Comments
newest_comments:
  enable: false
  sort_order: # Don't modify the setting unless you know how it works
  limit: 6
  storage: 10 # unit: mins, save data to localStorage
  avatar: true

# Bottom right button (右下角按鈕)
# --------------------------------------

# Conversion between Traditional and Simplified Chinese (簡繁轉換)
translate:
  enable: false
  # The text of a button
  default: 繁
  # the language of website (1 - Traditional Chinese/ 2 - Simplified Chinese）
  defaultEncoding: 2
  # Time delay
  translateDelay: 0
  # The text of the button when the language is Simplified Chinese
  msgToTraditionalChinese: '繁'
  # The text of the button when the language is Traditional Chinese
  msgToSimplifiedChinese: '簡'

# Read Mode (閲讀模式)
readmode: true

# dark mode
darkmode:
  enable: true
  # Toggle Button to switch dark/light mode
  button: true
  # Switch dark/light mode automatically (自動切換 dark mode和 light mode)
  # autoChangeMode: 1  Following System Settings, if the system doesn't support dark mode, it will switch dark mode between 6 pm to 6 am
  # autoChangeMode: 2  Switch dark mode between 6 pm to 6 am
  # autoChangeMode: false
  autoChangeMode: false

# Don't modify the following settings unless you know how they work (非必要請不要修改 )
# Choose: readmode,translate,darkmode,hideAside,toc,chat,comment
# Don't repeat 不要重複
rightside_item_order:
  enable: false
  hide: # readmode,translate,darkmode,hideAside
  show: # toc,chat,comment

# Lightbox (圖片大圖查看模式)
# --------------------------------------
# You can only choose one, or neither (只能選擇一個 或者 兩個都不選)

# medium-zoom
# https://github.com/francoischalifour/medium-zoom
medium_zoom: false

# fancybox
# http://fancyapps.com/fancybox/3/
fancybox: true

# Tag Plugins settings (標籤外掛)
# --------------------------------------

# mermaid
# see https://github.com/mermaid-js/mermaid
mermaid:
  enable: false
  # built-in themes: default/forest/dark/neutral
  theme:
    light: default
    dark: dark

# Note (Bootstrap Callout)
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0

# other
# --------------------------------------

# Pjax
# It may contain bugs and unstable, give feedback when you find the bugs.
# https://github.com/MoOx/pjax
pjax:
  enable: true
  exclude:
    # - xxxx
    # - xxxx

# Inject the css and script (aplayer/meting)
aplayerInject:
  enable: false
  per_page: false

# Snackbar (Toast Notification 彈窗)
# https://github.com/polonel/SnackBar
# position 彈窗位置
# 可選 top-left / top-center / top-right / bottom-left / bottom-center / bottom-right
snackbar:
  enable: true
  position: bottom-left
  bg_light: '#FFC107' # The background color of Toast Notification in light mode
  bg_dark: '#121212' # The background color of Toast Notification in dark mode

# https://instant.page/
# prefetch (預加載)
instantpage: false

# https://github.com/vinta/pangu.js
# Insert a space between Chinese character and English character (中英文之間添加空格)
pangu:
  enable: false
  field: site # site/post

# Lazyload (圖片懶加載)
# https://github.com/verlok/vanilla-lazyload
lazyload:
  enable: true
  field: site # site/post
  placeholder:
  blur: true

# PWA
# See https://github.com/JLHwung/hexo-offline
# ---------------
# pwa:
#   enable: false
#   manifest: /pwa/manifest.json
#   apple_touch_icon: /pwa/apple-touch-icon.png
#   favicon_32_32: /pwa/32.png
#   favicon_16_16: /pwa/16.png
#   mask_icon: /pwa/safari-pinned-tab.svg

# Open graph meta tags
# https://developers.facebook.com/docs/sharing/webmasters/
Open_Graph_meta: true

# Add the vendor prefixes to ensure compatibility
css_prefix: true

# Inject
# Insert the code to head (before '</head>' tag) and the bottom (before '</body>' tag)
# 插入代码到头部 </head> 之前 和 底部 </body> 之前
inject:
  head:
    # - <link rel="stylesheet" href="/xxx.css">
  bottom:
    - <link rel="stylesheet" href="/css/ramsayi.css">
    - <script src="/js/ramsayi.js"></script>
    - <link rel="stylesheet" href="/css/lantern.css">
    # - <script src="https://cdn.jsdelivr.net/gh/fz6m/china-lantern@1.6/dist/china-lantern.min.js"></script>
    # - <script src="xxxx"></script>

# CDN
# Don't modify the following settings unless you know how they work
# 非必要請不要修改
CDN:
  # main
  main_css:
  main:
  utils:

  # pjax
  pjax:

  # comments
  gitalk:
  gitalk_css:
  blueimp_md5:
  valine:
  disqusjs:
  disqusjs_css:
  utterances:
  twikoo:
  waline:
  giscus:

  # share
  addtoany:
  sharejs:
  sharejs_css:

  # search
  local_search:
  algolia_js:
  algolia_search_v4:
  instantsearch_v4:

  # math
  mathjax:
  katex:
  katex_copytex:
  katex_copytex_css:
  mermaid:

  # count
  busuanzi:

  # background effect
  canvas_ribbon:
  canvas_fluttering_ribbon:
  canvas_nest:

  lazyload:
  instantpage:
  typed:
  pangu:

  # photo
  fancybox_css_v4:
  fancybox_v4:
  medium_zoom:

  # snackbar
  snackbar_css:
  snackbar:

  # effect
  activate_power_mode:
  fireworks:
  click_heart:
  ClickShowText:

  # fontawesome
  fontawesome:

  # Conversion between Traditional and Simplified Chinese
  translate:

  # flickr-justified-gallery
  flickr_justified_gallery_js:
  flickr_justified_gallery_css:

  # aplayer
  aplayer_css:
  aplayer_js:
  meting_js:

  # Prism.js
  prismjs_js:
  prismjs_lineNumber_js:
  prismjs_autoloader:
```



## Butterfly主题 `.css` 文件修改

`/themes/butterfly/source/css/ramsayi.css`

```css
/* 滚动条 */
::-webkit-scrollbar {
    width: 6px;
    height: 10px;
}

::-webkit-scrollbar-thumb {
    background-color: #304FFE;
    background-image: -webkit-linear-gradient( 45deg, rgba(255, 255, 255, 0.4) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.4) 50%, rgba(255, 255, 255, 0.4) 75%, transparent 75%, transparent);
    border-radius: 2em;
}

::-webkit-scrollbar-corner {
    background-color: transparent;
}

::-moz-selection {
    color: #fff;
    background-color: #304FFE;
}

/* 自定义字体 */
@font-face {
    font-family: '霞鹜文楷';
    src: url('/assets/fonts/LXGWWenKai/LXGWWenKaiLite-Bold.ttf');
}

/* 文章页H1-H6图标样式效果 */
h1::before, h2::before, h3::before, h4::before, h5::before, h6::before {
    -webkit-animation: ccc 1.6s linear infinite ;
    animation: ccc 1.6s linear infinite ;
}
@-webkit-keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}
@keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}

/*半透明*/

/*文章*/
.layout > div:first-child:not(.recent-posts) {
    background: rgba(255,255,255,.7);
}
  
/*主页文章*/
#recent-posts > .recent-post-item {
    background: rgba(255,255,255,.7);
}
  
/*侧边栏*/
#aside-content .card-widget {
    background: rgba(255,255,255,.7);
}
/*黑暗模式*/
[data-theme="dark"] 
.layout > div:first-child:not(.recent-posts) {
    background: rgba(255,255,255,.3);
}
[data-theme="dark"] 
#recent-posts > .recent-post-item {
    background: rgba(255,255,255,.3);
}
[data-theme="dark"]     
#aside-content .card-widget {
    background: rgba(255,255,255,.3);
}

/* 底部按钮圆角 */
#rightside > div > button, #rightside > div > a{
    margin-bottom: 6px;
}
#rightside>div>a, #rightside>div>button {
    border-radius: 12px;
}

/* 卡片毛玻璃效果 */
div#post:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#post:hover{
    background-color: rgb(255 255 255 / 30%);
}
#aside-content .card-widget:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
    border-radius: 8px;
}
[data-theme="dark"]
#aside-content .card-widget:hover {
    background-color: rgb(255 255 255 / 30%);
}
div#recent-posts .recent-post-item:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#recent-posts .recent-post-item:hover{
    background-color: rgb(255 255 255 / 30%);
}
div#page:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#page:hover{
    background-color: rgb(255 255 255 / 30%);
}

/* 页脚透明 */
#footer {
	background: rgba(255, 255, 255, .15);
	color: #000;
	border-top-right-radius: 20px;
	border-top-left-radius: 20px;
	-webkit-backdrop-filter: saturate(100%) blur(5px);
	backdrop-filter: saturate(100%) blur(5px)
}

#footer::before {
	background: rgba(255, 255, 255, .15);
}

#footer #footer-wrap {
	color: var(--font-color);
}

#footer #footer-wrap a {
	color: var(--font-color);
}
```

## 主题魔改

### 滚动条

```css
/* 滚动条 */
::-webkit-scrollbar {
    width: 6px;
    height: 10px;
}

::-webkit-scrollbar-thumb {
    background-color: #304FFE;
    background-image: -webkit-linear-gradient( 45deg, rgba(255, 255, 255, 0.4) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.4) 50%, rgba(255, 255, 255, 0.4) 75%, transparent 75%, transparent);
    border-radius: 2em;
}

::-webkit-scrollbar-corner {
    background-color: transparent;
}

::-moz-selection {
    color: #fff;
    background-color: #304FFE;
}
```

### 自定义字体

```css
/* 自定义字体 */
@font-face {
    font-family: '霞鹜文楷';
    src: url('/assets/fonts/LXGWWenKai/LXGWWenKaiLite-Bold.ttf');
}
```

### 文章页 H1~H6 样式修改

```
{% tabs 1 %}
<!-- tab fontawesome 图标 -->
Butterfly 在 H1~H6 样式上使用了 [fontawesome.com](https://fontawesome.com/v5.15/icons?from=io) 上的图标，引用的是 Unicode 形式。可自行查找合适的。
<!-- endtab -->
```

```
<!-- tab 图标 Unicode 值获取-->
![](/assets/img/post/23ce82cf/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-09-11%20165341.png)
<!-- endtab -->
{% endtabs %}
```



#### 本站小风车样式

````
{% tabs 2 %}
<!-- tab 本站小风车样式 -->

```yaml
beautify:
  enable: true
  field: post # site/post
  # title-prefix-icon: '\f0c1' 原内容
  title-prefix-icon: '\f863'
  title-prefix-icon-color: '#304FFE'
```

<!-- endtab -->
````

````
<!-- tab 让小风车转起来-->

```css
/* 文章页H1-H6图标样式效果 */
h1::before, h2::before, h3::before, h4::before, h5::before, h6::before {
    -webkit-animation: ccc 1.6s linear infinite ;
    animation: ccc 1.6s linear infinite ;
}
@-webkit-keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}
@keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}
```

<!-- endtab -->
````

````
<!-- tab 风车转动速度 --->

想调整风车转动速度，修改以下内容里的时间，数字越小转动越快。

```css
h1::before, h2::before, h3::before, h4::before, h5::before, h6::before {
    -webkit-animation: ccc 1.6s linear infinite ;
    animation: ccc 1.6s linear infinite ;
}
```

<!-- endtab -->
````

````
<!-- tab 风车转的方向 -->

以下代码中，`-1turn` 为逆时针转动，`1turn` 为顺时针转动，相同数字部分记得统一修改：

```css
@-webkit-keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}
@keyframes ccc {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg)
    }
    to {
        -webkit-transform: rotate(-1turn);
        transform: rotate(-1turn)
    }
}
```

<!-- endtab -->

{% endtabs %}
````



#### 小风车颜色、大小修改

**效果演示**

![](/assets/img/post/23ce82cf/%E9%A3%8E%E8%BD%A6%E9%A2%84%E8%A7%88.jpg)

````
{% tabs 3 %}

<!-- tab 小风车颜色 css 代码 -->

```css
#content-inner.layout h1::before {
    color: #ef50a8 ;
    margin-left: -1.55rem;
    font-size: 1.3rem;
    margin-top: -0.23rem;
}
#content-inner.layout h2::before {
    color: #fb7061 ;
    margin-left: -1.35rem;
    font-size: 1.1rem;
    margin-top: -0.12rem;
}
#content-inner.layout h3::before {
    color: #ffbf00 ;
    margin-left: -1.22rem;
    font-size: 0.95rem;
    margin-top: -0.09rem;
}
#content-inner.layout h4::before {
    color: #a9e000 ;
    margin-left: -1.05rem;
    font-size: 0.8rem;
    margin-top: -0.09rem;
}
#content-inner.layout h5::before {
    color: #57c850 ;
    margin-left: -0.9rem;
    font-size: 0.7rem;
    margin-top: 0.0rem;
}
#content-inner.layout h6::before {
    color: #5ec1e0 ;
    margin-left: -0.9rem;
    font-size: 0.66rem;
    margin-top: 0.0rem;
}
```

<!-- endtab -->
````

````
<!-- tab 小风车 hover 效果 -->

**鼠标碰到小风车转速变慢及变色**

设置鼠标碰到标题时，小风车跟随标题变色，且像是被光标阻碍了，转速变慢。鼠标离开恢复转速。也可以设置为 `none` 鼠标碰到停止转动。

```css
#content-inner.layout h1:hover, #content-inner.layout h2:hover, #content-inner.layout h3:hover, #content-inner.layout h4:hover, #content-inner.layout h5:hover, #content-inner.layout h6:hover {
    color: #49b1f5 ;
}
#content-inner.layout h1:hover::before, #content-inner.layout h2:hover::before, #content-inner.layout h3:hover::before, #content-inner.layout h4:hover::before, #content-inner.layout h5:hover::before, #content-inner.layout h6:hover::before {
    color: #49b1f5 ;
    -webkit-animation: ccc 3.2s linear infinite ;
    animation: ccc 3.2s linear infinite ;
}
```

<!-- endtab -->
````

````
<!-- tab 页面设置图标转速 -->

**页面设置图标转速**

突然发现原作者设置的右下角设置 icon 转的太快了，让它慢一点吧。继续添加：

```css
/* 页面设置icon转动速度调整 */
#rightside_config i.fas.fa-cog.fa-spin {
    animation: fa-spin 5s linear infinite ;
}
```

<!-- endtab -->

{% endtabs %}
````



### 半透明

```css
/*半透明*/

/*文章*/
.layout > div:first-child:not(.recent-posts) {
    background: rgba(255,255,255,.7);
}
  
/*主页文章*/
#recent-posts > .recent-post-item {
    background: rgba(255,255,255,.7);
}
  
/*侧边栏*/
#aside-content .card-widget {
    background: rgba(255,255,255,.7);
}
/*黑暗模式*/
[data-theme="dark"] 
.layout > div:first-child:not(.recent-posts) {
    background: rgba(255,255,255,.3);
}
[data-theme="dark"] 
#recent-posts > .recent-post-item {
    background: rgba(255,255,255,.3);
}
[data-theme="dark"]     
#aside-content .card-widget {
    background: rgba(255,255,255,.3);
}
```

### 底部按钮圆角

```css
/* 底部按钮圆角 */
#rightside > div > button, #rightside > div > a{
    margin-bottom: 6px;
}
#rightside>div>a, #rightside>div>button {
    border-radius: 12px;
}
```

### 卡片毛玻璃效果

```css
/* 卡片毛玻璃效果 */
div#post:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#post:hover{
    background-color: rgb(255 255 255 / 30%);
}
#aside-content .card-widget:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
    border-radius: 8px;
}
[data-theme="dark"]
#aside-content .card-widget:hover {
    background-color: rgb(255 255 255 / 30%);
}
div#recent-posts .recent-post-item:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#recent-posts .recent-post-item:hover{
    background-color: rgb(255 255 255 / 30%);
}
div#page:hover{
    -webkit-backdrop-filter: saturate(180%) blur(5px);
    backdrop-filter: saturate(180%) blur(5px);
    background-color: rgb(255 255 255 / 70%);
}
[data-theme="dark"]
div#page:hover{
    background-color: rgb(255 255 255 / 30%);
}
```

### 页脚透明

```css
/* 页脚透明 */
#footer {
	background: rgba(255, 255, 255, .15);
	color: #000;
	border-top-right-radius: 20px;
	border-top-left-radius: 20px;
	-webkit-backdrop-filter: saturate(100%) blur(5px);
	backdrop-filter: saturate(100%) blur(5px)
}

#footer::before {
	background: rgba(255, 255, 255, .15);
}

#footer #footer-wrap {
	color: var(--font-color);
}

#footer #footer-wrap a {
	color: var(--font-color);
}
```

### 雪花飘落

themes\butterfly\source\js\ramsayi.js

```js
var stop, staticx;
var img = new Image();
img.src =
    "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACUAAAAlCAMAAADyQNAxAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAB1FBMVEUAAAD//////////6r//7///8z/1dX/29vf37/j48bm5szo6NHq6tXr69jt7cju3bvv37/t27br2LHq1b/o6Lnm5rPw4cPx48bj46rf35/V1ary5Lzm5r/b27bMzJnn58Lo6MXo3Lnn27bk17zj47i/v4Dq37/m2bPh4bTf36/r4Ljr4rrj2bPi2LHg1q3q37Xo3K7n26rl3Lnk263i2Kfk167d3arb26Tk27bl3bLl3bvl3arl3LDg1qPm2abj1arm3rXn36/f1arc0aLq1arp3rzo2LLu6c359u7y7dzh2q3g2Krl1Krj2are06aqqlXt58r///3////////z79vh0qXm1q3k0aTZzJndzJno0aL49ef6+PDg2KLe1qXizp3bzp7///307dvh0p7g0Zvd1KHc057f1Z/j1ZzbyJLw5sn59uvz7Nji06Dfz5fdzJnb0Zvfz4/mzJnjxo7p3rHf16fezpzZ0I7gzJneyJDc0Zfh0pbYxInl06fYzpPfypXcxYvbzpLbyH/MzIDfv4Dj2aHWzI/XyZTV1ZXbtpLi2J3cypX/gIDYzonVxo7dzIjR0Yvbwobfz5/h0qXk16HZzIyAgADYxHbbyKTVv4DV1YD///8ISxdUAAAAm3RSTlMAAQIDBAUGBwgJCgsMDQ4PEA4NDAsKERIJCAYTFAcFFRYWFRMSBBgUERAZGhsaGRgWFR0cGhMPDhweHh4dGRQSHyAYFgwXIS5YOiIhHhsXAyudp6ZAIh8cFA8LSWghHxoVnkYiIR4dGBIONFlCIyAeHBAKCRcgHxsZFxYRDR0aGBYVDgoIGxkTDAcaHQIaEg8LFRARExQCDQ4MBh76jTgAAAABYktHRAH/Ai3eAAAAB3RJTUUH5AwLEgsGRsWS1AAAAzxJREFUOMtV1AlXElEUB/BRh9g0thnBUVnUIdxSWSTcULAsUyjKBCuhcKNFAnO3JKzUmso2Wj5t9915g6d7DudwZn7872Xem8cwTA1ULak6LJZl5S94jdxkGESUsKxKdUEulQotdaioQaFWqzXwQUkgZRShUWs0Gq1Op9NqNRo1Osyjqq6OGkL0ej2BVScrBaHR1zeQqtcrToVhqFhEaC4ajEajwWQyWzheSxhLFUaRIIvJZDA2Wq3WRqMRHMfztiaB9ETFYhJnNpmIaW5pJs4AjONtrYIdwhhoqILBCTIYrdYWh8PpcrW1dyAjYYIoK+xnkZHT6YZyuS61ezqRYRhDGkIUzATI4XR3dff09F7u6x8gzMJBmF2kSqszI3K5u7u9Xq/P5wcW8AwGIYy0ZMhYGp3eZGi0tgC6EhoKhYZHfP7R/rGwJ2jmoCUqGEtXD1EtToLGJ6BCwCLRsfBgcJJvogoaNkCU42pXT2j82tT1G9M3Z3yz/lg0EA6aQdnjijJamx3ubu/QxK3biTt35+7NzENYMpwyL9hgfKYWhoexQLncPd7QxP1EIvFg7uHifDoSzZwrzJJV70hoYupRIvE4u7S8kl6NJtdSuf8UzOXq6/UNj08/efrseXY9/wJVIVfcoHPBf4TH1d720j/rm9mcy2azS1v57Z3dvbX9wgEoMU6fF6xPR3t/xO97tbi5tLS+nt9+fVh6s1YoHxy9lRULywhr7ekYi0X87+aXt7bygN6XSsf7hfJJ8VRRag0P6+gJDAD7sLKS/ygjiCofbZzaRYnuCZ6zmDo9gUwsMppOp7c/EfS58KV8Bg2pgv1l4zlzsDMcyERjq6s7h7sUnUAUNJSUvYpsMBzOZKLRvb3SV0QkChrKiux7G89zweC372s/ksnkz2MYHBFEgaoo71CTDdNS4KD2CzD4L4IgSpSq76PQCmxh0vw7lSoUSA4EESSI0LD6bgtCK8QVFyYnc7kc5Pw5OoKZsJ9UqZ4TdoG64sLJydmZbP5CO1kpTCQOYFOxWNzYAAIGUJygmur5Bb+yIxQEIpAQI1UqyjFHXDwuikjtCAhBIyPqAEpS/LwkCUmlRkGKw6rQuwgU8g+WNe/jJXwgmQAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAyMC0xMi0xMVQxMDoxMTowNiswODowMCGmScoAAAAldEVYdGRhdGU6bW9kaWZ5ADIwMjAtMTItMTFUMTA6MTE6MDYrMDg6MDBQ+/F2AAAAAElFTkSuQmCC";
function Sakura(x, y, s, r, fn) {
    this.x = x;
    this.y = y;
    this.s = s;
    this.r = r;
    this.fn = fn;
}
Sakura.prototype.draw = function(cxt) {
    cxt.save();
    var xc = 40 * this.s / 4;
    cxt.translate(this.x, this.y);
    cxt.rotate(this.r);
    cxt.drawImage(img, 0, 0, 40 * this.s, 40 * this.s)
    cxt.restore();
}
Sakura.prototype.update = function() {
    this.x = this.fn.x(this.x, this.y);
    this.y = this.fn.y(this.y, this.y);
    this.r = this.fn.r(this.r);
    if (this.x > window.innerWidth || this.x < 0 || this.y > window.innerHeight || this.y < 0) {
        this.r = getRandom('fnr');
        if (Math.random() > 0.4) {
            this.x = getRandom('x');
            this.y = 0;
            this.s = getRandom('s');
            this.r = getRandom('r');
        } else {
            this.x = window.innerWidth;
            this.y = getRandom('y');
            this.s = getRandom('s');
            this.r = getRandom('r');
        }
    }
}
SakuraList = function() {
    this.list = [];
}
SakuraList.prototype.push = function(sakura) {
    this.list.push(sakura);
}
SakuraList.prototype.update = function() {
    for (var i = 0, len = this.list.length; i < len; i++) {
        this.list[i].update();
    }
}
SakuraList.prototype.draw = function(cxt) {
    for (var i = 0, len = this.list.length; i < len; i++) {
        this.list[i].draw(cxt);
    }
}
SakuraList.prototype.get = function(i) {
    return this.list[i];
}
SakuraList.prototype.size = function() {
    return this.list.length;
}

function getRandom(option) {
    var ret, random;
    switch (option) {
        case 'x':
            ret = Math.random() * window.innerWidth;
            break;
        case 'y':
            ret = Math.random() * window.innerHeight;
            break;
        case 's':
            ret = Math.random();
            break;
        case 'r':
            ret = Math.random() * 6;
            break;
        case 'fnx':
            random = -0.5 + Math.random() * 1;
            ret = function(x, y) {
                return x + 0.5 * random - 1.7;
            };
            break;
        case 'fny':
            random = 1.5 + Math.random() * 0.7
            ret = function(x, y) {
                return y + random;
            };
            break;
        case 'fnr':
            random = Math.random() * 0.03;
            ret = function(r) {
                return r + random;
            };
            break;
    }
    return ret;
}

function startSakura() {
    requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame || window.webkitRequestAnimationFrame ||
        window.msRequestAnimationFrame || window.oRequestAnimationFrame;
    var canvas = document.createElement('canvas'),
        cxt;
    staticx = true;
    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;
    canvas.setAttribute('style', 'position: fixed;left: 0;top: 0;pointer-events: none;');
    canvas.setAttribute('id', 'canvas_sakura');
    document.getElementsByTagName('body')[0].appendChild(canvas);
    cxt = canvas.getContext('2d');
    var sakuraList = new SakuraList();
    for (var i = 0; i < 50; i++) {
        var sakura, randomX, randomY, randomS, randomR, randomFnx, randomFny;
        randomX = getRandom('x');
        randomY = getRandom('y');
        randomR = getRandom('r');
        randomS = getRandom('s');
        randomFnx = getRandom('fnx');
        randomFny = getRandom('fny');
        randomFnR = getRandom('fnr');
        sakura = new Sakura(randomX, randomY, randomS, randomR, {
            x: randomFnx,
            y: randomFny,
            r: randomFnR
        });
        sakura.draw(cxt);
        sakuraList.push(sakura);
    }
    stop = requestAnimationFrame(function() {
        cxt.clearRect(0, 0, canvas.width, canvas.height);
        sakuraList.update();
        sakuraList.draw(cxt);
        stop = requestAnimationFrame(arguments.callee);
    })
}
window.onresize = function() {
    var canvasSnow = document.getElementById('canvas_snow');
}
img.onload = function() {
    startSakura();
}

function stopp() {
    if (staticx) {
        var child = document.getElementById("canvas_sakura");
        child.parentNode.removeChild(child);
        window.cancelAnimationFrame(stop);
        staticx = false;
    } else {
        startSakura();
    }
}

var full_page = document.getElementsByClassName("full_page");
if (full_page.length != 0) {
  full_page[0].style.background = "transparent";
}
```

_config.butterfly.yml

```yml
inject:
  head:
  bottom:
    - <script src="/js/ramsayi.js"></script>
```

### 特殊节日黑白

themes\butterfly\layout\includes\head.pug	在末尾添加

```pug
if theme.blackandwhite
  include ./addons/blackandwhite.pug
```

themes\butterfly\layout\includes\addons\blackandwhite.pug

```pug
html
  body
    // 黑白色
    style.
      html{
      filter: grayscale( 100%);
      -webkit-filter: grayscale( 100%);
      -moz-filter: grayscale( 100%);
      -ms-filter: grayscale( 100%);
      -o-filter: grayscale( 100%);
      filter: url( "data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\'><filter id=\'grayscale\'><feColorMatrix type=\'matrix\' values=\'0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0\'/></filter></svg>#grayscale");
      filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
      -webkit-filter: grayscale( 1);
      }
```

_config.butterfly.yml

```yml
blackandwhite: false
```

### 灯笼

themes\butterfly\layout\includes\head.pug	末尾添加

```pug
include ./lantern.pug
```

themes\butterfly\layout\includes\lantern.pug

```pug
.dengl
  .d-box
    .d1
      span
      span
        p
      ul
        li
        li  
        li
          span
        li  
        li  
    .d2
      span
      span
        p
      ul
        li
        li  
        li
          span
        li  
        li  
  .d-box1
    .d1
      span
      span
        p
      ul
        li
        li  
        li
          span
        li  
        li  
    .d2
      span
      span
        p
      ul
        li
        li  
        li
          span
        li  
        li   
```

themes\butterfly\source\css\lantern.css

```css
/* 灯笼 Start */

* {
    box-sizing: border-box;
}


/* 移动端显示/隐藏 /none/block，可自定义显示一个 */

@media screen and (max-width: 970px) {
    .d-box1 {
        display: none;
    }
    .dengl .d-box {
        right: 0px;
        top: -40px;
        /* 自定义灯笼大小 */
        transform: scale(0.4);
    }
}

.dengl {
    position: fixed;
    z-index: 9;
}


/* .d-box,.d-box1{
    z-index: 9;
  } */

.d-box {
    position: fixed;
    /* 自定义灯笼的位置 */
    right: 85px;
    top: 0;
    /* 自定义灯笼大小 */
    transform: scale(0.8);
}

.d-box1 {
    position: fixed;
    /* 自定义灯笼的位置 */
    left: 0;
    top: 0;
    /* 自定义灯笼大小 */
    transform: scale(0.8);
}


/* 修改灯笼的字体 */

.d-box .d1::after {
    content: '虎年大吉';
}

.d-box1 .d1::after {
    content: '万事顺遂';
}

.d-box1 .d1,
.d-box1 .d2,
.d-box1 .d1::after,
.d-box1 .d1::before,
.d-box1 .d2::after,
.d-box1 .d2::before,
.d-box1 .d2 ul li span,
.d-box1 .d1 ul li span {
    background-color: #f01f1a;
    border: 5px solid #5c1713;
    /* 自定义灯笼的阴影 */
    /* box-shadow: 0 5px 61px rgba(255, 240, 29, 0.88); */
}

.d1,
.d2,
.d1::after,
.d1::before,
.d2::after,
.d2::before,
.d2 ul li span,
.d1 ul li span {
    background-color: #f01f1a;
    border: 5px solid #5c1713;
    /* 自定义灯笼的阴影 */
    box-shadow: 0 5px 61px #ff1d1d;
}

.d1::after,
.d1::before {
    height: 82px;
    position: absolute;
    top: 0;
    content: '';
    font-size: 17px;
}

.d1,
.d2 {
    position: relative;
    animation: swing 4s linear infinite;
    transform-origin: top center;
}

.d1 {
    width: 160px;
    top: 100px;
    height: 90px;
    right: 0;
    border-radius: 80px/49px;
}

.d1::before {
    top: -5px;
    right: 7px;
    width: 123px;
    border-radius: 62px/52px;
}

.d1::after {
    text-align: center;
    line-height: 90px;
    color: #ffe31d;
    font-weight: 600;
    top: -5px;
    right: 35px;
    width: 69px;
    border-radius: 41px/49px;
}

.d1 span {
    position: absolute;
    top: 84px;
    left: 49px;
    width: 50px;
    height: 16px;
    z-index: 2;
    border-radius: 0 0 10px 10px;
    background-color: #ffe31d;
    border: 5px solid #5c1713;
}

.d1 span:nth-child(2) {
    top: -17px;
    border-radius: 10px 10px 0 0;
}

.d1 p {
    position: absolute;
    top: -31px;
    left: 13px;
    width: 16px;
    height: 13px;
    border-radius: 25px;
    border: 5px solid #5c1713;
    border-bottom: 0;
}

.d1 ul {
    position: relative;
    top: 80px;
    left: 13px;
    width: 54px;
    display: flex;
}

.d1 li {
    flex: 1;
    list-style: none;
    height: 24px;
    margin: 0px 2.5px;
    width: 5px;
    border-radius: 5px;
    border-right: 3.5px solid #5c1713;
}

.d1 ul li:nth-child(3) {
    content: '';
    height: 50px;
}

.d1 ul li:nth-child(3)::before {
    content: '';
    position: absolute;
    top: 47px;
    left: 54px;
    width: 5px;
    height: 5px;
    border-radius: 5px 5px 10px 10px;
    background-color: #ffe31d;
    border: 5px solid #5c1713;
}

.d1 ul li span {
    position: absolute;
    top: 20px;
    left: 55px;
    width: 13px;
    height: 19px;
    border-radius: 14px;
}

.d2::after,
.d2::before {
    position: absolute;
    height: 128px;
    top: -3px;
    content: '';
}

.d2 {
    width: 199px;
    height: 128px;
    top: -61px;
    right: -122px;
    border-radius: 98px/70px;
}

.d2::before {
    top: -8px;
    right: 18px;
    width: 143px;
    border-radius: 69px/67px;
}


/* 自定义背景图片 */

.d2::after {
    top: -8px;
    right: 51px;
    width: 75px;
    border-radius: 57px/89px;
    background: url(https://bu.dusays.com/2021/02/03/7e1a77cf800cf.png) no-repeat;
    background-position: center;
    background-size: 92px auto;
}

.d2 span {
    position: absolute;
    top: 123px;
    left: 68px;
    width: 55px;
    height: 14px;
    z-index: 2;
    border-radius: 0 0 10px 10px;
    background-color: #ffe31d;
    border: 5px solid #5c1713;
}

.d2 span:nth-child(2) {
    top: -16px;
    border-radius: 10px 10px 0 0;
}

.d2 p {
    position: absolute;
    top: -32px;
    left: 13px;
    width: 19px;
    height: 13px;
    border-radius: 25px;
    border: 5px solid #5c1713;
    border-bottom: 0;
}

.d2 ul {
    position: relative;
    top: 121px;
    left: 32px;
    width: 53px;
    display: flex;
}

.d2 li {
    flex: 1;
    list-style: none;
    height: 24px;
    margin: 0px 3px;
    width: 4px;
    border-radius: 7px;
    border-right: 3px solid #5c1713;
}

.d2 ul li:nth-child(3) {
    content: '';
    height: 60px;
}

.d2 ul li:nth-child(3)::before {
    content: '';
    position: absolute;
    top: 59px;
    left: 53px;
    width: 9px;
    height: 6px;
    border-radius: 5px 5px 10px 10px;
    background-color: #ffe31d;
    border: 5px solid #5c1713;
}

.d2 ul li span {
    position: absolute;
    top: 21px;
    left: 54px;
    width: 18px;
    height: 17px;
    border-radius: 20px;
}

@keyframes swing {
    0% {
        transform: rotate(0);
    }
    25% {
        transform: rotate(-13deg);
    }
    50% {
        transform: rotate(0);
    }
    75% {
        transform: rotate(13deg);
    }
    100% {
        transform: rotate(0);
    }
}

/* 灯笼 END */
```

_config.butterfly.yml

```yml
inject:
  head:
  bottom:
    - <link rel="stylesheet" href="/css/lantern.css">
```

### 手机版 媒体查询

```css
/* 手机版 媒体查询 */
@media screen and (max-width: 900px) {

    /* 根字体大小 */
    :root {
        --global-font-size: 12px;
    }

    /* 文章块大小 */
    .layout>div:first-child {
        width: 95% !important;
        margin: 0 auto;
    }
}
```

### 手机版侧栏宽度

```css
/* 手机版侧栏宽度 */
#sidebar #sidebar-menus {
    right: -250px;
    width: 250px;
}
```

### 手机版侧栏圆角阴影

```css
/* 手机版侧栏圆角阴影 */
#sidebar #sidebar-menus .menus_items .site-page:hover {
    color: white;
    padding: 5px 0 5px 25px;
    border-radius: 8px;
    box-shadow: 2px 5px 10px #304ffe;
}
```

### 首页黑色遮罩

```css
/* 首页黑色遮罩 */
#page-header:not(.not-top-img):before {
    background-color: transparent;
}
```

### 顶部导航栏白色悬停字体

```css
/* 顶部导航栏白色悬停字体 */
#nav .menus_items .menus_item .menus_item_child li:hover * {
    color: white;
}
```

### 首页关注按钮

```css
/* 首页关注按钮 */
#aside-content .card-info #card-info-btn {
    border-radius: 25px;
    box-shadow: 2px 5px 10px #304ffe;
}

#aside-content .card-info #card-info-btn:hover {
    background-color: #2196f3;
    box-shadow: 2px 5px 10px #2196f3;
    transform: scale(1.1);
    transition: .5s;
}
```

### 右下角固定按钮

```css
/* 右下角固定按钮 */
#rightside>div>button,
#rightside>div>a {
    box-shadow: 0 5px 7px #5972fe;
}
```

### 首页分类悬停圆角阴影

```css
/* 首页分类悬停圆角阴影 */
#aside-content .card-archives ul.card-archive-list>.card-archive-list-item a,
#aside-content .card-categories ul.card-category-list>.card-category-list-item a {
    border-radius: 8px;
}

#aside-content .card-archives ul.card-archive-list>.card-archive-list-item a:hover,
#aside-content .card-categories ul.card-category-list>.card-category-list-item a:hover {
    background-color: #304ffe;
    color: white;
    box-shadow: 2px 5px 10px #304ffe;
}
```

### 文章页目录悬停阴影

```css
/* 文章页目录悬停阴影 */
#aside-content #card-toc .toc-content .toc-link.active {
    padding: 5px 0 5px 15px;
    border-radius: 8px;
    box-shadow: 2px 5px 10px #304ffe;
}
```

### 文章页 底部 tags阴影 share阴影

```css
/* 文章页 底部 tags阴影 share阴影 */
#post .tag_share .post-meta__tags {
    box-shadow: 0px 5px 7px #304ffe;
}

.social-share .icon-facebook {
    box-shadow: 0px 5px 7px #44619d;
}

.social-share .icon-twitter {
    box-shadow: 0px 5px 7px #55acee;
}

.social-share .icon-wechat {
    box-shadow: 0px 5px 7px #7bc549;
}

.social-share .icon-weibo {
    box-shadow: 0px 5px 7px #ff763b;
}

.social-share .icon-qq {
    box-shadow: 0px 5px 7px #56b6e7;
}
```

### 文章页 底部推荐文章 圆角

```css
/* 文章页 底部推荐文章 圆角 */
#pagination.pagination-post {
    border-radius: 8px;
}

.relatedPosts>.relatedPosts-list>div {
    border-radius: 8px;
}
```

### valine评论按钮阴影

```css
/* valine评论按钮阴影 */
#vcomment .vbtn {
    box-shadow: 0px 5px 7px #304ffe;
}
```



## 主题插件

### hexo-deployer-git

```bash
npm install hexo-deployer-git --save
```

```yml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: 
    github: https://github.com/ramsayi/ramsayi.github.io.git
  branch: master
```

### hexo-blog-encrypt

```bash
npm install --save hexo-blog-encrypt
```

```yml

# Security
encrypt: # hexo-blog-encrypt
  abstract: 有东西被加密了, 请输入密码查看.
  message: 您好, 这里需要密码.
  tags:
  - {name: tagName, password: 密码A}
  - {name: tagName, password: 密码B}
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
```

### hexo-douban

```bash
npm install hexo-douban --save
```

```yml
# 豆瓣
douban:
  user: 194612089
  builtin: false
  book:
    title: 'This is my book title'
    quote: 'This is my book quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: books
    limit:
  movie:
    title: 'This is my movie title'
    quote: 'This is my movie quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: movies
    limit:
  game:
    title: 'This is my game title'
    quote: 'This is my game quote'
    meta: true
    comments: true
    top_img: /assets/img/bg/bg/1001.jpg
    aside: true
    path: games
    limit:
  timeout: 10000 
```

### hexo-abbrlink

```bash
npm install hexo-abbrlink --save
```

```yml
# abbrlink config
abbrlink:
  alg: crc32  #算法: crc16(default) and crc32
  rep: hex    #进制: dec(default) and hex
```

### hexo-githubcalendar

```bash
npm i hexo-githubcalendar --save
```

```yml
# Ice Kano Plus_in
# Hexo Github Canlendar
# Author: Ice Kano
# Modify: Lete乐特
githubcalendar:
  enable: true
  priority: 3
  enable_page: /
  user: ramsayi
  layout:
    type: id
    name: recent-posts
    index: 0
  githubcalendar_html: '<div class="recent-post-item" style="width:100%;height:auto;padding:10px;"><div id="github_loading" style="width:10%;height:100%;margin:0 auto;display: block"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"  viewBox="0 0 50 50" style="enable-background:new 0 0 50 50" xml:space="preserve"><path fill="#d0d0d0" d="M25.251,6.461c-10.318,0-18.683,8.365-18.683,18.683h4.068c0-8.071,6.543-14.615,14.615-14.615V6.461z" transform="rotate(275.098 25 25)"><animateTransform attributeType="xml" attributeName="transform" type="rotate" from="0 25 25" to="360 25 25" dur="0.6s" repeatCount="indefinite"></animateTransform></path></svg></div><div id="github_container"></div></div>'
  pc_minheight: 280px
  mobile_minheight: 0px
  color: "['#f3f5ff', '#ccd4ff', '#a5b3ff', '#7e91fe', '#5770fe', '#304ffe', '#092efe', '#0122de', '#011cb7', '#011690', '#011069']"
  api: https://python-github-calendar-api.vercel.app/api
  # api: https://python-gitee-calendar-api.vercel.app/api
  calendar_js: https://cdn.jsdelivr.net/gh/Zfour/hexo-github-calendar@1.21/hexo_githubcalendar.js
  plus_style: ""
```

### hexo-magnet

```bash
npm i hexo-magnet --save
```

```yml
magnet:
  enable: true
  priority: 2
  enable_page: all
  type: categories
  devide: 2
  display:
    - name: 博客
      display_name: Ramsayiの魔改教程
      icon: 📚
    - name: 游戏
      display_name: Ramsayiの游戏修改
      icon: 🎮
    - name: 生活
      display_name: Ramsayiの生活趣闻
      icon: 🎉
    - name: 编程
      display_name: Ramsayiの编程学习
      icon: 👩‍💻
    - name: 书籍
      display_name: Ramsayiの读书笔记
      icon: 📒
    - name: 随想
      display_name: Ramsayiの胡思乱想
      icon: 💡
  color_setting:
    text_color: black
    text_hover_color: white
    background_color: "#f2f2f2"
    background_hover_color: "#304FFE"
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="width:100%;height: auto"><div id="catalog_magnet">${temple_html_item}</div></div>'
  plus_style: ""
```

### hexo-swiper

```bash
npm i hexo-swiper-bar --save
```

```yml
swiper:
  enable: true
  priority: 1
  enable_page: /
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="height: auto;width: 100%"><div class="blog-slider swiper-container-fade swiper-container-horizontal" id="swiper_container">${temple_html_item}</div></div>'
  plus_style: ""
```

### [hexo-butterfly-charts](https://guole.fun/posts/18158/)

```bash
npm i hexo-butterfly-charts --save
```

```yml
# 统计图表，支持发布文章统计、发布日历、Top标签统计、分类统计、分类雷达。
# see https://www.npmjs.com/package/hexo-butterfly-charts
charts:
  enable: true # 是否启用功能
  postsChart:
    title: 文章发布统计 # 设置文章发布统计的标题，默认为空
    interval: 1 # 横坐标间隔
  tagsChart:
    title: Top 10 标签统计 # 设置标签统计的标题，默认为空
    interval: 1 # 横坐标间隔
  postsCalendar_Title: #文章发布日历 # 设置发布日历的标题，默认为空
  categoriesChart_Title: # 设置分类统计的标题，默认为空
  categoriesRadar_Title: # 设置分类雷达的标题，默认为空
```

## 教程合集


|     作者     |                             连结                             |
| :----------: | :----------------------------------------------------------: |
|    Jerry     |   [自定义侧边栏](https://butterfly.js.org/posts/ea33ab97/)   |
|     小康     | [优雅魔改](https://www.antmoe.com/posts/a811d614/index.html) |
|  Lete 乐特   | [Butterfly主题美化-无修改源码 (持续更新中...)](https://butterfly.lete114.top/article/Butterfly-config.html) |
|    Akilar    |  [Hexo博客访问优化日记](https://akilar.top/posts/7c16c4bb/)  |
|    Akilar    | [基于Butterfly主题的美化日记](https://akilar.top/posts/f99b208/) |
|    Akilar    | [平滑升级魔改后的Hexo主题](https://akilar.top/posts/bbf68ad4/) |
|   小冰博客   | [小冰插件包 butterfly-orchid 1.0](https://zfe.space/post/hexo-butterfly-orchid.html) |
| 小嘉的部落格 | [关于我 Butterfly 主题的所有美化](https://blog.imzjw.cn/posts/b74f504f/) |
| 唐先森の博客 | [Hexo+Butterfly主题美化](https://ethant.top/articles/hexo541u/) |
| guole's Blog | [Butterfly美化日记/页面美化/插件美化/踩坑经历](https://guole.fun/posts/butterfly-custom/) |
| guole's Blog | [使用 Charts 插件给 Butterfly 增加统计图表](https://guole.fun/posts/18158/) |
| guole's Blog | [使用 Hexo-tag-map 插件，给文章插入高德百度谷歌地图](https://guole.fun/posts/41887/) |

