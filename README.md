# xiaozhi-esp32-qq-music
一个在 esp32 上运行 小智ai 的 QQ 音乐播放框架，整合了一些功能，你可以通过自行扩展能力

## 介绍

![随机播放个人歌单](demo.png)

这是一个由虾哥开源的[ESP32项目](https://github.com/78/xiaozhi-esp32)，更改而来，整合了 QQ 音乐播放功能，允许任何人免费使用，但是不可用于商业用途

本项目参考了以下项目：

    - [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32)
    - [xiaozhi-esp32-music](https://github.com/Maggotxy/xiaozhi-esp32-music)

本项目仅供学习和研究使用。项目不自带cookies，请自备cookies
如果有任何问题，请及时提出 Issues
项目主要贡献者：[qaq卟言](https://space.bilibili.com/86920865)（B站UP）

## 视频展示

👉 [小智ai播放QQ音乐，播放歌单（点歌）随机播放](https://www.bilibili.com/video/BV1h6HkzkEq6)

&emsp;

## 免责声明⚠️
1. 本项目仅供个人学习和技术研究使用
2. 不提供任何VIP/付费音乐资源，相关使用的任何VIP/付费音乐资源由第三方接口提供，并且不保证其接口稳定性
3. 禁止用于商业用途
4. 请遵守相关法律法规，不得用于任何违法用途
5. 做为一个音乐爱好者，我是支持付费的，使用本项目请支持正版音乐，购买相关音乐服务，鼓励大家在经济条件允许的情况下，支持正版音乐，为音乐产业的发展贡献一份力量
6. 建议在本地开发环境或个人服务器上部署使用
7. 本项目不提供线上 demo，请不要轻易信任使用他人提供的公开代理服务，以免发生安全问题
8. 本程序仅提供在线试听服务，未对音乐资源提供下载（存储），收集，传播等服务，所有音乐资源均标注原始链接，不提供任何形式的下载服务

&emsp;

## 项目结构

#### 目录结构
- esp32：ESP32 小智ai 端的音乐播放源代码
- qq_music：配套的音乐源代码
    - 主要文件
        - index.php：主要的服务器端文件，处理音乐请求和返回结果
        - xz.py：VIP/付费音乐资源 下载工具文件，用于下载VIP/付费音乐资源（支持批量下载）

&emsp;

## 改动范围

#### 新增
- main\boards\common\play_music.cc
- main\boards\common\play_music.h
- main\boards\common\music.h

#### 修改
- main\mcp_server.cc
- main\boards\common\board.cc
- main\boards\common\board.h
- main\audio\audio_codec.cc
- main\audio\audio_codec.h
- main\audio\audio_service.cc
- main\audio\audio_service.h
- main\application.cc
- main\application.h
- main\display\display.cc
- main\display\display.h
- main\display\lcd_display.cc
- main\display\lcd_display.h
- main\idf_component.yml

&emsp;

## 使用说明

1. 下载项目:
    - 源码地址： [upload.zip](https://qaqbuyan.com:88/乔安文件/文件/qq-music/upload.zip)
    - 固件版本：1.8.5

2. 解压到任意目录

3. 修改配置
    - 修改 index.php 音乐的 cookies
    - 修改 play_music.cc 的 Music_API 为自己的服务器地址
    - 修改 xz.py 的 Music_API 为自己的服务器地址

4. 上传 index.php 到服务器（需要安装curl扩展）

5. 编译并烧录 esp32 项目

6. 如果点歌功能失败，在人物介绍中填入
    - 收到点歌的需求时，立刻使用 MPC tool self.music.search_play_music 工具，同时禁止使用 search_music 功能。

7. 如果需要（批量）下载VIP/付费音乐资源，需要先运行 xz.py 脚本
    - 修改 xz.py 脚本中对应的 async def async_main() 函数中的 mids 定义
    - 运行 xz.py 脚本(python xz.py)
    - 脚本会自动下载音乐资源到当前目录
    - 下载完成后，将音乐资源上传到服务器 index.php 同级的 music 目录下

&emsp;

## 自带功能

- 音乐接口
    - 📁 音乐缓存
    - 🔍 音乐搜索
    - ❔  分享链接解析
    - 📊 排行榜获取
    - 📑 收藏歌单获取
    - 📰 推荐歌单获取
    - 📰 个人歌单获取
    - ⏰ 新歌获取
    - 💾 缓存仓库获取
    - 🎵 获取歌曲播放链接（支持多种音质）
    - 🎶 特定歌单获取
    - 🎧 获取歌曲音质列表
    - 📝 获取歌词
    - 📊 获取所有歌单信息、用户创建的歌单信息、用户收藏的歌单信息
    - 🖼️ 获取歌曲封面

- 音乐播放
    - [x] 🔍 点歌
    - [x] 🎵 批量播放（个人歌单、收藏歌单、排行榜、缓存仓库）
    - [x] 🔄 切换模式（顺序播放、随机播放）
    - [x] 📝 显示歌词
    - [ ] ⏸ 暂停播放
    - [ ] ⏭ 下一首
    - [ ] ⏮ 上一首

&emsp;

## 注意事项
1. 本项目不提供任何形式的技术支持：
    - 第三方接口问题
2. 若将服务部署到公网，强烈建议更改 UA 请求头(这样仅放行允许的 UA 的请求)限制请求范围，以防 api 被他人滥用，导致服务器响应慢或流量被占满等问题

&emsp;

## 其他问题
1. 为什么不直接将项目上传到 GitHub 或 Gitee 等平台？
    - 当然是因为方便我跑路啦，毕竟南山必胜客可不是白叫的，GitHub 上有人也逆向了，后面都停滞了几年不更新了（或者是向其他用户直接告诉，有人给我发律师函了🥴）
👉 [music](https://github.com/sunzongzheng/music)

&emsp;

## 如果代码能帮助到你，欢迎给个star