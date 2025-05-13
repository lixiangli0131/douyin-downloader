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

## 🚀 快速开始 <!-- by 李镭雨 -->

### 安装

1. 安装 Python 依赖
在命令行中进入项目根目录（即包含 requirements.txt 文件的目录），执行以下命令安装所需 Python 依赖：
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

2. 复制配置文件：
```bash
cp config.example.yml config.yml
```
若执行命令提示没有找到 cp 命令（可能出现在 Windows 系统），可以手动将 config.example.yml 文件复制一份，并命名为 config.yml ，放置在项目根目录下。

### 配置

编辑 `config.yml` 文件，设置：
- 下载链接
- 保存路径
- Cookie 信息（从浏览器开发者工具获取）
从浏览器开发者工具获取Cookie步骤:
1.打开开发者工具(F12)
2.转到"Application"或"存储"选项卡
3.选择"Cookies"
4.复制相关站点的Cookie名称和值
- 其他下载选项

### 运行

**方式一：使用配置文件（推荐）**
在命令行中进入项目根目录，执行以下命令运行：
```bash
python DouYinCommand.py
```
运行过程中，工具将根据 config.yml 文件的配置，自动进行内容下载

**方式二：使用命令行**
在命令行中进入项目根目录，执行以下命令，其中 -C True 表示启用 Cookie（若不需要 Cookie 可省略），-l 后面接抖音分享链接，-p 后面接下载路径：
```bash
python DouYinCommand.py -C True -l "抖音分享链接" -p "下载路径"
```
​
### 常见的问题及解决方法
- 运行报错 ModuleNotFoundError：表示缺少某些 Python 模块，确认是否已正确执行 pip install -r requirements.txt 安装依赖，若已安装，检查 Python 环境是否正确，可尝试重新创建并激活虚拟环境后再次安装依赖。​
- 下载失败提示 Cookie 无效：重新获取最新的 Cookie，确保 Cookie 未过期，并且在复制过程中没有遗漏或添加多余字符。​
- 下载内容缺失或不完整：检查保存路径是否有足够的磁盘空间，若网络不稳定，可尝试降低线程数或分批下载。

## 📦 项目结构

```
douyin-downloader/
├── apiproxy/               # 静态资源
|   ├── common/
|   |   ├── __init__.py
|   |   ├── config.py
|   |   └── utlis.py 
|   ├──douyin/
|   |   ├── __init__.py
|   |   ├── database.py
|   |   ├── douyin.py 
|   |   ├── douyinapi.py
|   |   ├── download.py
|   |   ├── result.py
|   |   └── urls.py 
|   ├── tiktok/
|   |   ├── __init__.py
|   |   └── __init__.py 
├── docs/
|   ├──examples.md          #使用实例
├── img/                    #图片
├── utlis/ 
|   ├── logger.py
├── DouYinCommand.py        #运行
├── README.md
├── config.example.yml      # 组件
├── config.yml
└── requirements.txt
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

