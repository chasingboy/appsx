<h1 align="center">appsx</h1>
<h3 align="center">appsx 是一款自动化信息收集｜敏感信息识别｜未授权漏洞扫描工具</h3>
<p align="center">
  <img src="https://img.shields.io/badge/Version-V1.0.0-green?style=flat">
  <img src="https://img.shields.io/github/stars/chasingboy/appsx?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://img.shields.io/github/issues/chasingboy/appsx">
  <img src="https://img.shields.io/github/downloads/chasingboy/appsx/total?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=chasingboy.appsx&left_color=green&right_color=#66ccff">
</p>

<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/appsx.png">

### 即将发布
### 前言
在WEB渗透测试中，经常需要收集前端js文件中的信息，比如提取API信息｜URL信息｜敏感信息等。appsx 工具的核心理念就是把这一过程自动化，能够提升渗透测试的效率。

### 功能
* 爬虫提供普通模式和 headless 模式
* 自动爬取js| html| php| asp 等页面
* 自动识别 webpack 打包的 js 文件
* 下载爬取的文件并提取 API 信息
* 批量测试 URL 和 API 信息
* 默认调用 dirsx 进行扫描
* 启用 nuclei 进行敏感信息识别

### 基本使用
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/run.png">

* 默认爬虫模式
```
root$ appsx -u http://127.0.0.1
```
* headless 模式
```
# 需要在 config.yaml 中配置 nuclei 路径
root$ appsx -u http://127.0.0.1 --headless
```
* 启用 nuclei
```
root$ appsx -u http://127.0.0.1 --nuclei
```
* 自动提取 API 信息并进行探测未授权漏洞
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/resut.png">

### 结果保存
默认保存在桌面的 xworks 文件夹，可通过 config.yaml 文件配置
```
# crawler-urls.txt -> 爬取的 URL 结果
# select-results.txt -> 提取的 API 结果
# httpx-results.txt -> URL|API 探测结果
# static -> 下载的文件结果
2024-12-02-16-23-20-test.gzalkj.com_sadmin root$ tree .
.
├── crawler-urls.txt
├── httpx-results.txt
├── select-results.txt
└── static
    ├── 097628.chunk-2125b98f.99d70750.js
    ├── ... ...
```

### appsx -h
```
~ kali$ appsx -h

          
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
  -w, --wordlist=         appoint wordlist for scanning directory
      --title-len=        set title display length (default: 50)
  -t, --threads=          number of threads to use (default: 20)
      --timeout=          httpx running timeout in seconds (default: 5)
  -x, --excode=           specify the status codes that be filtered eg: 400,404 (default:
                          400,401,404,406,416,501,502,503)
      --config=           path to the configuration file
      --proxy=            set request proxy eg: --proxy http://127.0.0.1:8080
      --target-dir=       set target directory to select router and test eg: --target-dir "./static"
      --only-crawler      only crawling web files|router|..., disable httpx running
      --crawling-timeout= common crawling timeout in seconds (default: 10)
      --crawling-threads= number of threads to crawling (default: 5)
  -m, --maxnum=           maxnum links to crawl (default: 100)
      --headless          enable headless crawling
      --headless-timeout= headless crawling timeout in seconds (default: 10)
      --show-browser      show the browser on the screen with headless mode

Plugins Options:
      --no-dirsx          disable running dirsx default(enable)
      --nuclei            enable running nuclei
      --xray              enable running xray

Activation Options:
      --activate          enable to activate appsx
      --activate-help     show activate help
      --license=          set license file eg: --license license.appsx
      --license-time      show license activated time and expiry time

Help Options:
  -h, --help              Show this help message
```
