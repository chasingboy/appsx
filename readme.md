<h1 align="center">appsx</h1>
<h3 align="center">appsx 是一款自动化信息收集｜敏感信息识别｜未授权漏洞扫描工具</h3>
<p align="center">
  <img src="https://img.shields.io/badge/Version-V1.1.0-green?style=flat">
  <img src="https://img.shields.io/github/stars/chasingboy/appsx?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://img.shields.io/github/issues/chasingboy/appsx">
  <img src="https://img.shields.io/github/downloads/chasingboy/appsx/total?style=flat&labelColor=rgb(41%2C52%2C52)&color=green">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=chasingboy.appsx&left_color=green&right_color=#66ccff">
</p>

<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/appsx.png">

### 前言
在WEB渗透测试中，经常需要收集前端js文件中的信息，比如提取API信息｜URL信息｜敏感信息等。appsx 工具的核心理念就是把这一过程自动化，能够提升渗透测试的效率。

### 功能
* 爬虫提供普通模式和 headless 模式
* 自动爬取js｜html｜php｜asp 等页面
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
  > fofa 任意找的 WEB
<img width="1154" alt="image" src="https://github.com/chasingboy/appsx/blob/main/assets/result.png">

### chromium 下载
--headless 模式需要在 config.yaml 文件配置 chromium

**不要下载新版本, 新版本在爬取 http 链接时会自动转为 https, 导致访问出错, 108.x.x.x 以下的版本都是可以的**

Chromium@https://vikyd.github.io/download-chromium-history-version/#/

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

### 激活方式
执行命令生成 **activate.appsx 文件**, 通过邮件或者微信群提交 **activate.appsx文件** 获取 license

⚠️注意: **linux 系统需要在root权限下才能运行**
```bash
# appsx -h
Activation Options:
      --activate          enable to activate appsx
      --activate-help     show activate help
      --license=          set license file eg: --license license.appsx
      --license-time      show license activated time and expiry time

# 在当前目录生成 activate.appsx 文件, 通过邮件或者微信群提交该文件获取 license
root$ appsx --activate

# 激活 appsx
root$ appsx --license license.appsx
```
详细参考-> https://github.com/chasingboy/appsx/blob/main/activate.md

### TODO
* 增加基础漏洞扫描模块
* 增加 pdf｜docx 报告导出模块
* ... ...

### config.yaml
```
# 设置 js 等文件下载路径，如果没有设置, 默认存放在桌面的 xworks 文件夹
# setting work path where save results, default -> $HOME/desktop/xworks.
workpath: ""

# 设置 nuclei 和 chromium 浏览器的路径
nuclei: "/tools/nuclei/nuclei"
chrome: "/tools/chrome/Chromium.app/Contents/MacOS/Chromium"

# 自定义添加 dirsx 扫描字典, 文件模式｜字符串
dirsx:
  payloads-file: "/tools/poc/wordlist.txt"

  payloads:
  - "admin"
  ... ...

# 设置爬虫允许后缀
allow-extensions:
  - ".js"
  - ".php"
  ... ...

# 设置过滤的 js 文件
script-blacks:
  - "vue.min.js"
  - "axios.min.js"
  ... ...

# 其他设置 ... ...
```

### 敏感信息扫描
poc 来源 ——> 整合 nuclei file 类型 POC + 个人编写 POC
* 识别用户信息-> 用户名｜密码｜邮箱｜key｜token｜...
* 识别内网 IP 泄露
* 识别文件名-> zip｜docx｜pdf｜excel｜...
* 识别 js.map 文件泄露

### appsx -h
```bash
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

### 免责声明
请在使用本工具时遵循使用者以及目标系统所在国当地的相关法律法规，一切未授权测试均是不被允许的。对于因使用工具而引发的任何直接、间接、偶然、特殊性的损害均由**使用者承担责任**。
详细内容请查看@https://github.com/chasingboy/appsx/blob/main/assets/readme.md
