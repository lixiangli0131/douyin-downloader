<!-- 邹爱华的主要功能实现描述 -->
（一）配置文件方式
过程：通过创建和编辑 config.yml 配置文件，可以方便地管理下载参数。

基础配置：设置下载链接、保存路径及下载选项（如音乐、封面、头像等）。
下载链接：支持作品链接或用户主页链接。
保存路径：指定下载的文件存储目录。
下载选项：可以选择是否下载音乐、封面、头像、以及保存 JSON 数据。
时间范围过滤：仅下载特定时间范围内的作品。
增量更新：支持增量更新发布作品、合集等。
数量限制：限制下载的作品数量，如最新的10个发布作品等。
这是一个完整的抖音视频下载工具的配置文件和使用说明，我来详细解析每个部分的功能和实现逻辑：


# 下载链接
link:
  - "https://v.douyin.com/xxxxx/"  # 作品链接
  - "https://www.douyin.com/user/xxxxx"  # 用户主页
  # 保存路径
path: "./downloads"
 # 下载选项
music: true    # 下载视频原声（MP3格式）
cover: true    # 下载视频封面（JPG/PNG）
avatar: true   # 下载作者头像（用户主页模式有效）
json: true     # 保存视频元数据（作者信息、发布时间等）
通过如下命令执行：
python DouYinCommand.py
#  时间范围过滤
仅下载指定时间范围内的作品
start_time: "2023-01-01"  # 开始时间
end_time: "2023-12-31"    # 结束时间
# 或使用 "now" 表示当前时间
end_time: "now"
#  增量更新
increase:
  post: true   # 跳过已下载的发布作品
  like: false  # 始终下载点赞作品（不检查重复）
  mix: true    # 跳过已下载的合集内容
#   数量限制策略
number:
  post: 10     # 按发布时间倒序取10条
  like: 5      # 最多下载5个点赞作品  
  mix: 3       # 每个合集只下3个视频



（二）命令行方式

单个视频：下载单个作品。
用户主页：下载用户发布或点赞的作品，支持同时下载多种类型。
合集：下载指定合集或用户的所有合集。
自定义保存选项：可设置不下载音乐、封面或自定义保存路径。
批量下载：支持多链接批量下载及多线程加速。
# 下载单个视频
python DouYinCommand.py -C True -l "https://v.douyin.com/xxxxx/"
下载用户主页作品
# 下载发布作品
python DouYinCommand.py -C True -l "https://www.douyin.com/user/xxxxx" -M post

# 下载点赞作品
python DouYinCommand.py -C True -l "https://www.douyin.com/user/xxxxx" -M like

# 同时下载发布和点赞作品
python DouYinCommand.py -C True -l "https://www.douyin.com/user/xxxxx" -M post -M like
下载合集
# 下载单个合集
python DouYinCommand.py -C True -l "https://www.douyin.com/collection/xxxxx"

# 下载用户所有合集
python DouYinCommand.py -C True -l "https://www.douyin.com/user/xxxxx" -M mix
自定义保存选项
# 不下载音乐和封面
python DouYinCommand.py -C True -l "链接" -m False -c False

# 自定义保存路径
python DouYinCommand.py -C True -l "链接" -p "./my_downloads"
批量下载
# 下载多个链接
python DouYinCommand.py -C True -l "链接1" -l "链接2" -l "链接3"

# 使用多线程
python DouYinCommand.py -C True -l "链接" -t 10

3. 高级用法
Cookie 设置：解决访问限制问题。
数据库支持：启用数据库以支持增量更新。
文件夹风格：控制是否为每个作品创建独立文件夹。
Cookie设置：（反反爬）
# Cookie 设置
如果遇到访问限制，可以设置 Cookie：

# 配置文件方式：

cookies:
  msToken: "xxx"    # 动态令牌
  ttwid: "xxx"      # 设备指纹
  odin_tt: "xxx"    # 用户标识

# 命令行方式：

python DouYinCommand.py -C True -l "链接" --cookie "msToken=xxx; ttwid=xxx;"
# 数据库支持
# 启用数据库以支持增量更新：
database: true
# 文件夹风格
# 控制文件保存结构：
folderstyle: true  # 每个作品创建独立文件夹



