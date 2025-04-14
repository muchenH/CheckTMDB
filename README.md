# CheckTMDB

每日自动更新TMDB，themoviedb、thetvdb 国内可正常连接IP，解决DNS污染，供tinyMediaManager(TMM削刮器)、Kodi的刮削器、群晖VideoStation的海报墙、Plex Server的元数据代理、Emby Server元数据下载器、Infuse、Nplayer等正常削刮影片信息。

## 一、前景

自从我早两年使用了黑群NAS以后，下了好多的电影电视剧，发现电视端无法生成正常的海报墙。查找资料得知应该是 themoviedb.org、tmdb.org 无法正常访问，因为DNS受到了污染无法正确解析到TMDB的IP，故依葫芦画瓢写了一个python脚本，每日定时通过[dnschecker](https://dnschecker.org/)查询出最佳IP，并自动同步到路由器外挂hosts，可正常削刮。

**本项目无需安装任何程序**

通过修改本地、路由器 hosts 文件，即可正常削刮影片信息。

## 文件地址

- tmdb ipv4 hosts文件：`https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv4` ，[链接](https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv4)
- tmdb ipv6 hosts：`https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv6` ，[链接](https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv6)

## 二、使用方法

### 2.1 手动方式

#### 2.1.1 IPv4地址复制下面的内容

```bash
# Tmdb Hosts Start
13.225.239.70               themoviedb.org
13.225.239.70               www.themoviedb.org
13.225.239.50               auth.themoviedb.org
18.239.208.24               api.themoviedb.org
13.225.239.39               tmdb.org
18.239.208.58               api.tmdb.org
143.244.50.91               image.tmdb.org
18.239.214.93               thetvdb.com
18.239.214.93               api.thetvdb.com
# Update time: 2025-04-15T06:11:52+08:00
# IPv4 Update url: https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv4
# IPv6 Update url: https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv6
# Star me: https://github.com/cnwikee/CheckTMDB
# Tmdb Hosts End

```

该内容会自动定时更新， 数据更新时间：2025-04-15T06:11:52+08:00

#### 2.1.2 IPv6地址复制下面的内容

```bash
# Tmdb Hosts Start
2600:9000:21d7:ee00:e:5373:440:93a1                themoviedb.org
2600:9000:21d7:9e00:e:5373:440:93a1                www.themoviedb.org
2600:9000:21d7:5c00:16:e4a1:eb00:93a1              auth.themoviedb.org
2600:9000:274d:cc00:c:174a:c400:93a1               api.themoviedb.org
2600:9000:21d7:f400:10:db24:6940:93a1              tmdb.org
2600:9000:274d:ee00:10:fb02:4000:93a1              api.tmdb.org
2400:52e0:1a01::987:1                              image.tmdb.org
# Update time: 2025-04-15T06:11:52+08:00
# IPv4 Update url: https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv4
# IPv6 Update url: https://github.com/cnwikee/CheckTMDB/blob/main/Tmdb_host_ipv6
# Star me: https://github.com/cnwikee/CheckTMDB
# Tmdb Hosts End

```

该内容会自动定时更新， 数据更新时间：2025-04-15T06:11:52+08:00

> [!NOTE]
> 由于项目搭建在Github Aciton，延时数据获取于Github Action 虚拟主机网络环境，请自行测试可用性，建议使用本地网络环境自动设置。

#### 2.1.3 修改 hosts 文件

hosts 文件在每个系统的位置不一，详情如下：

- Windows 系统：`C:\Windows\System32\drivers\etc\hosts`
- Linux 系统：`/etc/hosts`
- Mac（苹果电脑）系统：`/etc/hosts`
- Android（安卓）系统：`/system/etc/hosts`
- iPhone（iOS）系统：`/etc/hosts`

修改方法，把第一步的内容复制到文本末尾：

1. Windows 使用记事本。
2. Linux、Mac 使用 Root 权限：`sudo vi /etc/hosts`。
3. iPhone、iPad 须越狱、Android 必须要 root。

#### 2.1.4 激活生效

大部分情况下是直接生效，如未生效可尝试下面的办法，刷新 DNS：

1. Windows：在 CMD 窗口输入：`ipconfig /flushdns`

2. Linux 命令：`sudo nscd restart`，如报错则须安装：`sudo apt install nscd` 或 `sudo /etc/init.d/nscd restart`

3. Mac 命令：`sudo killall -HUP mDNSResponder`

**Tips：** 上述方法无效可以尝试重启机器。

## 三、参数说明

1. 直接执行`check_tmdb_github.py`脚本，同时查询IPv4及IPv6地址，目录生成`Tmdb_host_ipv4`文件，及`Tmdb_host_ipv6`文件；
2. 带`-G` 参数执行：`check_tmdb_github.py -G`，会在`Tmdb_host_ipv4`文件，及`Tmdb_host_ipv6`文件中追加 Github IPv4 地址；

## 其他

- [x] 自学薄弱编程基础，大部分代码基于AI辅助生成，此项目过程中，主要人为解决的是：通过 [dnschecker](https://dnschecker.org/) 提交时，通过计算出正确的udp参数，获取正确的csrftoken，携带正确的referer提交！
- [x] README.md 及 部分代码 参考[GitHub520](https://github.com/521xueweihan/GitHub520)
- [x] * 本项目仅在本机测试通过，如有问题欢迎提 [issues](https://github.com/cnwikee/CheckTMDB/issues/new)
