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

## 🚀 Getting Started <!-- by 李镭雨 -->

### Installation

1. Install Python Dependencies
Navigate to the project root directory in the command line (the directory containing the requirements.txt file) and run the following command to install the required Python dependencies:
```bash
pip install -r requirements.txt
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
If the command prompt does not find the cp command (which may occur in Windows systems), you can manually copy the config.example.yml file and rename it to config.yml, placing it in the project's root directory.

### Configuration

Edit config.yml to set：
- Download URLs
- Save path
- Cookie (from browser DevTools)
Cookie Retrieval Steps:
1.Press F12 → DevTools
2.Go to Application/Storage tab
3.Select "Cookies"
4.Copy target site's cookie names/values

### Execution

**Method 1: Config File (Recommended)**
Enter the project root directory in the command line and execute the following command to run.：
```bash
python DouYinCommand.py
```
During the operation, the tool will automatically download content according to the configuration in the config.yml file.

**Method 2: CLI Arguments**
Enter the project root directory in the command line and execute the following command, where -C True means to enable cookies (which can be omitted if cookies are not needed), -l is followed by the Douyin share link, and -p is followed by the download path.：
```bash
python DouYinCommand.py -C True -l "抖音分享链接" -p "下载路径"
```
​
### Troubleshooting
- Runtime error ModuleNotFoundError: indicates that some Python modules are missing. Confirm whether you have correctly executed 'pip install -r requirements.txt' to install the dependencies. If they are already installed, check if the Python environment is correct. You can try recreating and activating the virtual environment, then install the dependencies again.
- Download failed prompt: Cookie is invalid: re-obtain the latest Cookie, ensure that the Cookie has not expired, and make sure there are no missing or extra characters during the copying process.
- Download content is missing or incomplete: Check if there is enough disk space in the save path. If the network is unstable, try reducing the number of threads or downloading in batches.

## 📦 Project Structure

```
douyin-downloader/
├── apiproxy/               # Core modules
|   ├── common/
|   |   ├── __init__.py
|   |   ├── config.py
|   |   └── utlis.py 
|   ├──douyin/
|   |   ├── __init__.py
|   |   ├── database.py
|   |   ├── douyin.py 
|   |   ├── douyinapi.py   #API handler
|   |   ├── download.py    #Multithreaded downloader
|   |   ├── result.py
|   |   └── urls.py 
|   ├── tiktok/
|   |   ├── __init__.py
|   |   └── __init__.py 
├── docs/
|   ├──examples.md          #Usage examples
├── img/                    
├── utlis/ 
|   ├── logger.py           #Logging system (debug levels)
├── DouYinCommand.py        #Main entry
├── README.md
├── config.example.yml      #Component
├── config.yml              #User config
└── requirements.txt        # Dependencies
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

