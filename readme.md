<h1 align="center">appsx</h1>
<h3 align="center">appsx 是一款自动化信息收集｜敏感信息识别｜未授权漏洞扫描｜敏感信息识别｜指纹识别｜常见漏洞扫描工具</h3>
<p align="center">
  <img src="https://img.shields.io/badge/Version-V1.1.0-green?style=flat">
  <img src="https://img.shields.io/github/stars/chasingboy/appsx?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://img.shields.io/github/issues/chasingboy/appsx">
  <img src="https://img.shields.io/github/downloads/chasingboy/appsx/total?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=chasingboy.appsx&left_color=green&right_color=#66ccff">
</p>

<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/appsx.png">

### 前言
在 WEB 渗透测试中，经常需要收集前端 js 文件中的信息，比如提取 API 信息｜URL 信息｜敏感信息等。appsx 工具的核心理念就是把这一过程自动化，能够提升渗透测试的效率。

### 功能
* 爬虫提供普通模式和 headless 模式
* 支持自动爬取 js｜html｜php｜asp 等页面
* 支持自动识别 webpack 打包的 js 文件
* 支持下载爬取的文件并提取 API 信息
* 支持批量测试 URL 和 API 信息
* 支持先指纹识别再 POC 扫描漏洞
* 支持对爬取的页面进行敏感信息识别
* 支持导出敏感信息识别报告、扫描报告
* 支持对 40X URL Bypass 探测

### 基本使用
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/run.png">

* 默认爬虫模式
```
root$ appsx -u http://127.0.0.1
```
* headless 模式
```
# 需要在 config.yaml 中配置 chrome 路径
root$ appsx -u http://127.0.0.1 --headless
```
* POC 扫描模式
```
root$ appsx -u http://127.0.0.1 --pocsan
```
**先对目标进行指纹识别，再使用对应 POC 进行漏洞扫描**
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/scan.png">

*  敏感信息识别模式
```
root$ appsx --target-dir /root/static --select
```
### 自动化扫描过程
对目标 URL 进行爬取文件 php | js | html | asp | jsp |... -> 下载爬取到的页面 -> 提取 API 信息并进行探测未授权漏洞 -> 对目标进行指纹识别 -> 使用指纹对应 POC 进行漏洞扫描 -> 使用 select 模块进行敏感信息识别 -> 输出报告
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/result.png">

### 插件模式
使用插件模式参数指定某一功能
```
--crawler -> 只对目标 URL 进行爬取不进行漏洞扫描
--select  -> 只对指定的目录｜文件进行敏感信息识别
--bypass  -> 只对目标 URL 进行 40X Bypass 探测
--pocscan -> 只对目标 URL 进行 poc 扫描
```

```bash
Plugins Options:
      --crawler           only crawling web files|router|..., disable httpx|poc|...
      --select            enable select routers|password|email|.. from files
      --bypass            enable 40X bypass testing
      --pocscan           enable poc scanning
```

### chromium 下载
--headless 模式需要在 config.yaml 文件配置 chromium

**不要下载新版本, 新版本在爬取 http 链接时会自动转为 https, 导致访问出错, 108.x.x.x 以下的版本都是可以的**

Chromium@https://vikyd.github.io/download-chromium-history-version/#/

### 结果保存
默认保存在桌面的 xworks 文件夹，可通过 config.yaml 文件配置
```
# crawler-urls.txt      -> 爬取的 URL 结果
# select-results.txt    -> 提取的 API 结果
# httpx-results.txt     -> 探测的 API 结果
# APPSX扫描报告.html
# APPSX-SELECT报告.html

# static -> 保存下载的文件
2025-05-20-16-23-20-127.0.0.1 kali$ tree .
.
├── crawler-urls.txt
├── httpx-results.txt
├── select-results.txt
└── static
    ├── 097628.chunk-2125b98f.99d70750.js
    ├── ... ...
```

### 报告样例
[1] 扫描报告-> https://htmlpreview.github.io/?https://github.com/chasingboy/appsx/blob/main/reports/127.0.0.1-APPSX%E6%89%AB%E6%8F%8F%E6%8A%A5%E5%91%8A-1.html

[2] 扫描报告-> https://htmlpreview.github.io/?https://github.com/chasingboy/appsx/blob/main/reports/127.0.0.1-APPSX%E6%89%AB%E6%8F%8F%E6%8A%A5%E5%91%8A-2.html

[3] 识别报告-> https://htmlpreview.github.io/?https://github.com/chasingboy/appsx/blob/main/reports/APPSX-SELECT%E6%8A%A5%E5%91%8A.html

### 激活方式
执行命令生成 **activate.appsx 文件**, 通过邮件｜微信群提交 **activate.appsx文件** 至开发者获取 license

⚠️注意: **linux 系统需要在root权限下才能运行**
```bash
# appsx -h
Activation Options:
      --activate          enable to activate appsx
      --activate-help     show activate help
      --license=          set license file eg: --license license.appsx
      --license-time      show license activated time and expiry time

# 在当前目录生成 activate.appsx 文件, 通过邮件或者微信群提交该文件给开发者获取 license
root$ appsx --activate

# 激活 appsx, 比如 license 文件: xxx-c3a9f4d1cca725543a2a10b2cf8a224a-license.appsx
root$ appsx --license xxx-c3a9f4d1cca725543a2a10b2cf8a224a-license.appsx
```
详细参考-> https://github.com/chasingboy/appsx/blob/main/activate.md


### config.yaml
```
# config yaml V2.0
name: APPSX CONFIG

# setting work path where save results, default -> $HOME/desktop/xworks.
workpath: ""

# setting proxy eg: http://127.0.0.1:8080
proxy: ""

# tools path
chrome: ""

# setting nuclei poc.
file-poc-path: ""
http-poc-path: ""

# httpx running, filter title blacklist
title-blacks: 
  - "非法访问"
  - "页面不存在"

# filter domain when select links from javascript files.
domain-blacks: 
  - "github.com"
  - "google.com"
  - "google.cn"
  - "element-plus.org"
  - "angularjs.org"
  - ".gov.cn"
  - "apache.org"
  - "gitee.com"
  - "support.apple.com"
  - "bootcss.com"
  - "tiny.cloud"
  - "oasis-open.org"

# allow crawling extensions
allow-extensions:
  - ".js"
  - ".php"
  - ".html"
  - ".htm"
  - ".asp"
  - ".aspx"
  - ".jsp"
  - ".jspx"
  - ".do"
  - ".action"

# script blacklist
script-blacks:
  - "vue.min.js"
  - "axios.min.js"
  - "moment.min.js"
  - "jquery.min.js"
  - "jsencrypt.min.js"
```

### 敏感信息扫描
POC 来源 ——> 整合 nuclei POC + 个人编写 POC
* 识别用户信息-> 用户名｜密码｜邮箱｜key｜token｜...
* 识别内网 IP 泄露
* 识别文件名-> zip｜docx｜pdf｜excel｜...
* 识别 js.map 文件泄露

### TODO
* 漏洞扫描 | 指纹识别 POC

### appsx -h
```bash
kali$ appsx -h

          
       █████╗ ██████╗ ██████╗ ███████╗██╗  ██╗
      ██╔══██╗██╔══██╗██╔══██╗██╔════╝╚██╗██╔╝
      ███████║██████╔╝██████╔╝███████╗ ╚███╔╝ 
      ██╔══██║██╔═══╝ ██╔═══╝ ╚════██║ ██╔██╗ 
      ██║  ██║██║     ██║     ███████║██╔╝ ██╗
      ╚═╝  ╚═╝╚═╝     ╚═╝     ╚══════╝╚═╝  ╚═╝                                                                    
                                            1.1.0
                               xboy@追风少年

Usage:
  appsx [OPTIONS]

Common Options:
  -u, --url=              input url of target
  -l, --list=             input file containing list of target
      --title-len=        set title display length (default: 50)
  -t, --threads=          number of threads to use (default: 20)
      --timeout=          httpx running timeout in seconds (default: 5)
  -x, --excode=           specify the status codes that be filtered eg: 400,404 (default:
                          400,401,404,406,416,501,502,503)
      --config=           path to the configuration file
      --proxy=            set request proxy eg: --proxy http://127.0.0.1:8080
      --no-show-bar       disable show progress bar
      --target-dir=       set target directory to select router and test eg: --target-dir "./static"
      --crawling-timeout= common crawling timeout in seconds (default: 10)
      --crawling-threads= number of threads to crawling (default: 5)
  -m, --maxnum=           max number of links to crawl (default: 100)
      --headless          enable headless crawling
      --headless-timeout= headless crawling timeout in seconds (default: 10)
      --show-browser      show the browser on the screen with headless mode

Templates Options:
      --id=               templates to run based on template ids (comma-separated, file)
      --tags=             templates to run based on tags (comma-separated, file)
      --payload-threads=  number of threads to brute on poc payload  (default: 10)

Plugins Options:
      --crawler           only crawling web files|router|..., disable httpx|poc|...
      --select            enable select routers|password|email|.. from files
      --bypass            enable 40X bypass testing
      --pocscan           enable poc scanning

Activation Options:
      --activate          enable to activate appsx
      --activate-help     show activate help
      --license=          set license file eg: --license license.appsx
      --license-time      show license activated time and expiry time

Help Options:
  -h, --help              Show this help message
```
### 公众号
该公众号用于编写 Xtools 系列工具使用文档和工具更新通知

<p align="center"><img width="300" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/xsec.png"></p>

### 免责声明
请在使用本工具时遵循使用者以及目标系统所在国当地的相关法律法规，一切未授权测试均是不被允许的。对于因使用工具而引发的任何直接、间接、偶然、特殊性的损害均由**使用者承担责任**。
详细内容请查看@https://github.com/chasingboy/appsx/blob/main/assets/readme.md
