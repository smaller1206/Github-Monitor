<div align="center">

# VIPKID GITHUB MONITOR

[![License](https://img.shields.io/badge/license-GPLv3-blue.svg)](./LICENSE)
[![](https://img.shields.io/badge/python-3.5+-yellow.svg)](https://www.python.org/)
[![](https://img.shields.io/badge/docker-latest-blue.svg)](https://www.docker.com/)
[![](https://img.shields.io/github/stars/VKSRC/Github-Monitor.svg?label=Stars&style=social?style=plastic)](https://github.com/VKSRC/Github-Monitor) 
[![](https://img.shields.io/github/issues/VKSRC/Github-Monitor.svg)](https://github.com/VKSRC/Github-Monitor)

![](docs/media/screenshot.jpg)

</div>

-----


## 系统特点
* 分钟级监控
* 简单且灵活的任务配置
* 邮件提醒
* github token管理
* 支持docker一键部署
* 运行十分稳定

## 安装指南


首先将代码clone到本地：

#### 修改配置文件

 首先复制根目录的`.env.docker`并重命名为`.env`，修改其中的`Email Settings`和`initial Administrator`配置。这两个配置分别控制邮件提醒，以及初始管理帐号密码。
 
 
**注意: 第一次启动由于mysql容器启动时间较久，可能会用30s左右的时间，页面才可以正常访问**
 

## 使用手册

### 1.添加Token

Github Monitor使用Github REST API v3接口进行搜索，所以需要预先配置Token进行认证。

首先登录Github，然后进入[Token配置页面](https://github.com/settings/tokens)创建Token。

随后把Token添加到Github Monitor中。

![](docs/media/token.jpg)

Github API有次数限制，1分钟最多请求30次，为了提高爬取速度，Github Monitor支持添加多个Token。


### 2.添加监控任务

如图：

![](docs/media/task.jpg)

- 任务名称：仅做标记使用,无实际意义。
- 关键词：支持多个关键词，每行一个，支持[Github REST API v3搜索语法](https://developer.github.com/v3/search/#search-code)，如：`vipkid extension:java`，只搜索java后缀文件。
- 忽略帐号：不支持模糊匹配，忽略指定帐号下的仓库，同样支持多个帐号，换行分隔。
- 忽略仓库：支持模糊匹配，比如：`github.io`，可忽略`test.github.io`、`vipkid.github.io`等仓库。
- 邮箱：可为空，不填则不会邮件提醒。
- 爬取页数：默认5页，每页50条数据。
- 爬取间隔：默认60分钟，可根据自己需求修改。


### 3.确认/忽略风险

如图：

![](docs/media/list.jpg)


爬虫爬取到的数据会入库，可以在`查询系统`中进行操作，进行`处理/加白/忽略仓库`操作。

- 处理：确认有风险，需要处理。
- 加白：确认无风险，以后不会再提醒，如果文件有修改，还是会再次提醒。
- 忽略仓库：批量加白该仓库下已经发现的信息。


