# DouYin Downloader

<a href="https://trendshift.io/repositories/13156" target="_blank"><img src="https://trendshift.io/api/badge/repositories/13156" alt="jiji262%2Fdouyin-downloader | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

DouYin Downloader 是一个用于批量下载抖音内容的工具。基于抖音 API 实现，支持命令行参数或 YAML 配置文件方式运行，可满足大部分抖音内容的下载需求。

## ✨ 项目特点

- **多种内容支持**
  - 视频、图集、音乐、直播信息下载
  - 支持个人主页、作品分享、直播、合集、音乐集合等多种链接
  - 支持去水印下载
  
- **批量下载能力**
  - 多线程并发下载
  - 支持多链接批量下载
  - 自动跳过已下载内容
  
- **灵活配置**
  - 支持命令行参数和配置文件两种方式
  - 可自定义下载路径、线程数等
  - 支持下载数量限制
  
- **增量更新**
  - 支持主页作品增量更新
  - 支持数据持久化到数据库
  - 可根据时间范围过滤

## 🚀 快速开始

### Installation

1. 安装 Python 依赖：
```bash
pip install -r requirements.txt
```
如果在安装过程中遇到网络问题，导致下载缓慢或失败，您可以尝试使用国内的镜像源，例如使用清华大学的镜像源：
```bash
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
若出现 Permission denied 权限错误（常见于 Linux 和 macOS 系统），可以在命令前添加 sudo 提升权限，但请注意，这可能需要您输入系统密码：
```bash
sudo pip install -r requirements.txt
```
If you encounter network issues during the installation process that result in slow or failed downloads, you can try using domestic mirror sources, such as Tsinghua University's mirror source:
```bash
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
If a Permission denied error occurs (common in Linux and macOS systems), you can add sudo before the command to elevate permissions, but please note that this may require you to enter your system password:
```bash
sudo pip install -r requirements.txt
```

2. Copy Config File：
```bash
cp config.example.yml config.yml
```

### 配置

编辑 `config.yml` 文件，设置：
- 下载链接
- 保存路径
- Cookie 信息（从浏览器开发者工具获取）
- 其他下载选项

### 运行

**方式一：使用配置文件（推荐）**
```bash
python DouYinCommand.py
```

**方式二：使用命令行**
```bash
python DouYinCommand.py -C True -l "抖音分享链接" -p "下载路径"
```

## 使用交流群

![fuye](img/fuye.png)

## 使用截图

![DouYinCommand1](img/DouYinCommand1.png)
![DouYinCommand2](img/DouYinCommand2.png)
![DouYinCommand download](img/DouYinCommanddownload.jpg)
![DouYinCommand download detail](img/DouYinCommanddownloaddetail.jpg)

## 📝 支持的链接类型

- 作品分享链接：`https://v.douyin.com/xxx/`
- 个人主页：`https://www.douyin.com/user/xxx`
- 单个视频：`https://www.douyin.com/video/xxx`
- 图集：`https://www.douyin.com/note/xxx`
- 合集：`https://www.douyin.com/collection/xxx`
- 音乐原声：`https://www.douyin.com/music/xxx`
- 直播：`https://live.douyin.com/xxx`

## 🛠️ 高级用法

### 命令行参数

基础参数：
```
-C, --cmd            使用命令行模式
-l, --link          下载链接
-p, --path          保存路径
-t, --thread        线程数（默认5）
```

下载选项：
```
-m, --music         下载音乐（默认True）
-c, --cover         下载封面（默认True）
-a, --avatar        下载头像（默认True）
-j, --json          保存JSON数据（默认True）
```

更多参数说明请使用 `-h` 查看帮助信息。

### 示例命令

1. 下载单个视频：
```bash
python DouYinCommand.py -C True -l "https://v.douyin.com/xxx/"
```

2. 下载主页作品：
```bash
python DouYinCommand.py -C True -l "https://v.douyin.com/xxx/" -M post
```

3. 批量下载：
```bash
python DouYinCommand.py -C True -l "链接1" -l "链接2" -p "./downloads"
```

更多示例请参考[使用示例文档](docs/examples.md)。

## 📋 注意事项

1. 本项目仅供学习交流使用
2. 使用前请确保已安装所需依赖
3. Cookie 信息需要自行获取
4. 建议适当调整线程数，避免请求过于频繁

## 🤝 贡献

欢迎提交 Issue 和 Pull Request。

## 📜 许可证

本项目采用 [MIT](LICENSE) 许可证。

## 🙏 鸣谢

- [TikTokDownload](https://github.com/Johnserf-Seed/TikTokDownload)
- 本项目使用了 ChatGPT 辅助开发，如有问题请提 Issue

## 📊 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=jiji262/douyin-downloader&type=Date)](https://star-history.com/#jiji262/douyin-downloader&Date)




# License

[MIT](https://opensource.org/licenses/MIT) 

<!-- 邹爱华主要功能使用教程 -->
（one） Configuration file format
Process: By creating and editing the config. yml configuration file, it is easy to manage download parameters.
Basic configuration: Set download link, save path, and download options (such as music, cover, avatar, etc.).
Download link: Supports work links or user homepage links.
Save Path: Specify the storage directory for the downloaded file.
Download options: You can choose whether to download music, cover, avatar, and save JSON data.
Time range filtering: Only download works within a specific time range.
Incremental Update: Supports incremental updates for publishing works, collections, etc.
Quantity limit: Limit the number of downloaded works, such as the latest 10 released works.
This is a complete configuration file and instructions of the Tiktok video download tool. Let me analyze the functions and implementation logic of each part in detail:
#Download link
link:
- " https://v.douyin.com/xxxxx/ # Work Link
- " https://www.douyin.com/user/xxxxx # User homepage
#Save Path
path: "./downloads"
#Download Options
Music: true # Download video soundtrack (MP3 format)
Cover: true # Download video cover (JPG/PNG)
Avatar: true # Download author avatar (valid in user homepage mode)
JSON: true # Save video metadata (author information, publication time, etc.)
Execute the following command:
python DouYinCommand.py
#Time range filtering
Only download works within the specified time range
Start_time: "2023-01-01" # Start time
End_time: "2023-12-31" # End time
#Or use 'now' to indicate the current time
end_time: "now"
#Incremental update
increase:
Post: true # Skip downloaded published works
Like: false # Always download liked works (without checking for duplicates)
Mix: true # Skip downloaded collection content
#Quantity restriction strategy
number:
Post: 10 # Retrieve 10 items in reverse order of publication time
Like: 5 # Download up to 5 like works
Mix: 3 # Only 3 videos per collection
（two） Command line mode
Single video: Download a single work.
User homepage: Download works posted or liked by users, supporting simultaneous downloading of multiple types.
Collection: Download the specified collection or all collections of the user.
Custom save options: You can set not to download music, cover art, or customize the save path.
Batch Download: Supports multi link batch download and multi-threaded acceleration.
#Download a single video
python DouYinCommand.py -C True -l " https://v.douyin.com/xxxxx/ "
Download user homepage works
#Download and publish works
python DouYinCommand.py -C True -l " https://www.douyin.com/user/xxxxx " -M post
#Download and like works
python DouYinCommand.py -C True -l " https://www.douyin.com/user/xxxxx " -M like
#Simultaneously download, publish, and like works
python DouYinCommand.py -C True -l " https://www.douyin.com/user/xxxxx " -M post -M like
Download Collection
#Download a single collection
python DouYinCommand.py -C True -l " https://www.douyin.com/collection/xxxxx "
#Download all user collections
python DouYinCommand.py -C True -l " https://www.douyin.com/user/xxxxx " -M mix
Customize save options
#Do not download music and covers
Python DouYinCommander. py - C True - l "Link" - m False - c False
#Customize save path
Python DouYinCommand. py - C True - l "Link" - p "./mydownloads
Batch download
#Download multiple links
Python DouYinCommander. py - C True - l "Link 1" - l "Link 2" - l "Link 3"
#Using multithreading
Python DouYinCommander. py - C True - l "Link" - t 10
（three）. Advanced usage
Cookie settings: Resolve access restriction issues.
Database support: Enable the database to support incremental updates.
Folder style: Control whether to create separate folders for each work.
Cookie settings: (Anti crawling)
#Cookie settings
If you encounter access restrictions, you can set cookies:
#Configuration file format:
cookies:
MsToken: "xxx" # Dynamic Token
Ttwid: "xxx" # Device Fingerprint
Odin_tt: "xxx" # User ID
#Command line method:
Python DouYinCommand. py - C True - l "Link" - cookie "msToken=xxx;  ttwid=xxx; "
#Database support
#Enable database to support incremental updates:
database: true
#Folder Style
#Control file saving structure:
Folderstyle: true # Create a separate folder for each work