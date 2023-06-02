---
title: Hexo博客搭建
tags:
  - 博客
  - Hexo
categories:
  - 建站博客
abbrlink: b8f4bd70
swiper_index: 5
swiper_desc: Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
swiper_cover: '/assets/img/post/hexo2.webp'
date: 2020-07-07 20:48:56
---

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

# 安装

## 安装Git

- Windows：下载并安装 [git](https://git-scm.com/download/win).
- Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) 或者下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/)。
- Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

> Mac 用户
>
> 如果在编译时可能会遇到问题，请先到 App Store 安装 Xcode，Xcode 完成后，启动并进入 **Preferences -> Download -> Command Line Tools -> Install** 安装命令行工具。

> Windows 用户
>
> 对于中国大陆地区用户，可以前往 [淘宝 Git for Windows 镜像](https://npm.taobao.org/mirrors/git-for-windows/) 下载 git 安装包。

最后一步 添加路径 时选择 `Use Git from the Windows Command Prompt`，以后就可以直接在终端里打开git了。

检查是否安装成功，并查看版本号：

```bash
git --version
```

## 安装Node.js

Node.js 为大多数平台提供了官方的 [安装程序](https://nodejs.org/en/download/)。对于中国大陆地区用户，可以前往 [淘宝 Node.js 镜像](https://npm.taobao.org/mirrors/node) 下载。

其它的安装方法：

- Windows：通过 [nvs](https://github.com/jasongin/nvs/)（推荐）或者[nvm](https://github.com/nvm-sh/nvm) 安装。
- Mac：使用 [Homebrew](https://brew.sh/) 或 [MacPorts](http://www.macports.org/) 安装。
- Linux（DEB/RPM-based）：从 [NodeSource](https://github.com/nodesource/distributions) 安装。
- 其它：使用相应的软件包管理器进行安装，可以参考由 Node.js 提供的 [指导](https://nodejs.org/en/download/package-manager/)

对于 Mac 和 Linux 同样建议使用 nvs 或者 nvm，以避免可能会出现的权限问题。

> Windows 用户
>
> 使用 Node.js 官方安装程序时，请确保勾选 **Add to PATH** 选项（默认已勾选）

> For Mac / Linux 用户
>
> 如果在尝试安装 Hexo 的过程中出现 `EACCES` 权限错误，请遵循 [由 npmjs 发布的指导](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) 修复该问题。强烈建议 **不要** 使用 root、sudo 等方法覆盖权限

检查是否安装成功，并查看版本号：

```bash
node -v
npm -v
```

## 安装Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。会有几个警告，无视它(`npm install hexo-cli -g`)：

```bash
npm i hexo-cli -g
```

检查是否安装成功，并查看版本号(`hexo version`)：

```bash
hexo -v
```

# 建站

## 初始化

文件管理器新建一个文件夹，用于存放自己的博客文件：`D:\blog\ramsayi`。

在`D:\blog` 下右键 `ramsayi` 点击 `Git Bash Here`，打开git的控制台窗口，以后所有的操作都在git控制台进行。

初始化文件夹：

```bash
hexo init
```

安装必备的组件：

```bash
npm install
```

新建完成后，指定文件夹的目录如下：

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### _config.yml

网站的 [配置](https://hexo.io/zh-cn/docs/configuration) 信息，您可以在此配置大部分的参数。

### package.json

应用程序的信息。[EJS](https://ejs.co/), [Stylus](http://learnboost.github.io/stylus/) 和 [Markdown](http://daringfireball.net/projects/markdown/) renderer 已默认安装，您可以自由移除。

```json
package.json{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.8.0",
    "hexo-generator-archive": "^0.1.5",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.1",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-renderer-marked": "^0.3.2",
    "hexo-server": "^0.3.3"
  }
}
```

### scaffolds

[模版](https://hexo.io/zh-cn/docs/writing) 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。

Hexo的模板是指在新建的文章文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。

### source

资源文件夹是存放用户资源的地方。除 `_posts` 文件夹之外，开头命名为 `_` (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 `public` 文件夹，而其他文件会被拷贝过去。

### themes

[主题](https://hexo.io/zh-cn/docs/themes) 文件夹。Hexo 会根据主题来生成静态页面。

## 生成静态网页

生成静态文件`(hexo generate)`：

```bash
hexo g
```

| 选项                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| `-d`, `--deploy`      | 文件生成后立即部署网站                                       |
| `-w`, `--watch`       | 监视文件变动                                                 |
| `-b`, `--bail`        | 生成过程中如果发生任何未处理的异常则抛出异常                 |
| `-f`, `--force`       | 强制重新生成文件 Hexo 引入了差分机制，如果 `public` 目录存在，那么 `hexo g` 只会重新生成改动的文件。 使用该参数的效果接近 `hexo clean && hexo generate` |
| `-c`, `--concurrency` | 最大同时生成文件的数量，默认无限制                           |

## 启动本地服务器

启动本地服务器(hexo server)：

```bash
hexo s
```

| 选项             | 描述                           |
| :--------------- | :----------------------------- |
| `-p`, `--port`   | 重设端口                       |
| `-s`, `--static` | 只使用静态文件                 |
| `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |

默认情况下，访问网址为： `http://localhost:4000/`。

![img](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/Hexo%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA/%E6%89%B9%E6%B3%A8%202020-07-09%20193923.jpg)

按`ctrl+c`关闭本地服务器。

# 连接Github与本地

右键打开git bash，输入以下命令：

```bash
git config --global user.name "ramsayi"
git config --global user.email "ramsayi726@gmail.com"
```

生成密钥SSH key：

```bash
ssh-keygen -t rsa -C "ramsayi726@gmail.com"
```

网页打开[github](http://github.com/)，在头像下面点击`settings`，再点击`SSH and GPG keys`，新建一个SSH，名字任意。

git bash中输入以下命令：

```bash
cat ~/.ssh/id_rsa.pub
```

将输出的内容复制到 新建SSH 框中，点击确定保存。

输入`ssh -T git@github.com`，出现自己的用户名，就成功了。

![img](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/Hexo%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA/%E6%89%B9%E6%B3%A8%202020-07-09%20194604.jpg)

打开博客根目录下的`_config.yml`文件，这是博客的配置文件，在这里可以修改与博客相关的各种信息。

修改最后一行的配置：

```yml
deploy:
  type: git
  repo: git@github.com:ramsayi/ramsayi.github.io.git
  branch: master
```

repo(repository)修改为自己的github项目地址。

# 写文章

首先在博客根目录下右键打开git bash，安装一个扩展`npm i hexo-deployer-git`。

然后输入`hexo new post "article title"`，新建一篇文章。

然后打开`D:\blog\ramsayi\source\_posts`的目录，可以发现下面多了一个文件夹和一个`.md`文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦。

编写完markdown文件后，根目录下输入`hexo g`生成静态网页，然后输入`hexo s`可以本地预览效果，最后输入`hexo d`上传到github上。这时打开你的github.io主页就能看到发布的文章啦。

具体的Hexo命令 [点我](https://hexo.io/zh-cn/docs/commands)

## 新建文章

```bash
hexo new [layout] <title>
```

新建一篇文章。如果没有设置 `layout` 的话，默认使用博客根目录 [_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

```bash
hexo new "post title with whitespace"
```

| 参数              | 描述                                          |
| :---------------- | :-------------------------------------------- |
| `-p`, `--path`    | 自定义新文章的路径                            |
| `-r`, `--replace` | 如果存在同名文章，将其替换                    |
| `-s`, `--slug`    | 文章的 Slug，作为新文章的文件名和发布后的 URL |

默认情况下，Hexo 会使用文章的标题来决定文章文件的路径。对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件。你可以使用 `--path` 参数来覆盖上述行为、自行决定文件的目录：

```bash
hexo new page --path about/me "About me"
```

以上命令会创建一个 `source/about/me.md` 文件，同时 Front Matter 中的 title 为 `"About me"`

注意！title 是必须指定的！如果你这么做并不能达到你的目的：

```bash
hexo new page --path about/me
```

此时 Hexo 会创建 `source/_posts/about/me.md`，同时 `me.md` 的 Front Matter 中的 title 为 `"page"`。这是因为在上述命令中，hexo-cli 将 `page` 视为指定文章的标题、并采用默认的 `layout`。

## 发布

```bash
hexo publish [layout] <filename>
```

发表草稿。

## 部署

```bash
hexo deploy
```

部署网站。

| 参数               | 描述                     |
| :----------------- | :----------------------- |
| `-g`, `--generate` | 部署之前预先生成静态文件 |

该命令可以简写为：

```bash
hexo d
```

## 渲染

```bash
hexo render <file1> [file2] ...
```

渲染文件。

| 参数             | 描述         |
| :--------------- | :----------- |
| `-o`, `--output` | 设置输出路径 |

## 迁移

```bash
hexo migrate <type>
```

从其他博客系统 [迁移内容](https://hexo.io/zh-cn/docs/migration)。

## 清除缓存

```bash
hexo clean
```

清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

## 列出详情

```bash
hexo list <type>
```

列出网站资料。

## Hexo版本

```bash
hexo version
```

显示 Hexo 版本。

## 选项

### 安全模式

```bash
hexo --safe
```

在安全模式下，不会载入插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

```bash
hexo --debug
```

在终端中显示调试信息并记录到 `debug.log`。当您碰到问题时，可以尝试用调试模式重新执行一次，并 [提交调试信息到 GitHub](https://github.com/hexojs/hexo/issues/new)。

### 简洁模式

```bash
hexo --silent
```

隐藏终端信息。

### 自定义配置文件的路径

```bash
# 使用 custom.yml 代替默认的 _config.yml
hexo server --config custom.yml

# 使用 custom.yml 和 custom2.json，其中 custom2.json 优先级更高
hexo generate --config custom.yml,custom2.json,custom3.yml
```

自定义配置文件的路径，指定这个参数后将不再使用默认的 `_config.yml`。
你可以使用一个 YAML 或 JSON 文件的路径，也可以使用逗号分隔（无空格）的多个 YAML 或 JSON 文件的路径。例如：

```bash
# 使用 custom.yml 代替默认的 _config.yml
hexo server --config custom.yml

# 使用 custom.yml, custom2.json 和 custom3.yml，其中 custom3.yml 优先级最高，其次是 custom2.json
hexo generate --config custom.yml,custom2.json,custom3.yml
```

当你指定了多个配置文件以后，Hexo 会按顺序将这部分配置文件合并成一个 `_multiconfig.yml`。如果遇到重复的配置，排在后面的文件的配置会覆盖排在前面的文件的配置。这个原则适用于任意数量、任意深度的 YAML 和 JSON 文件。

### 显示草稿

```bash
hexo --draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

### 自定义 CWD

```bash
hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。

# 备份博客源文件

博客越写越多，将markdown源文件备份到github变得非常重要。github pages要求免费账户的username.github.io必须是public repository。网上主要有两种方案，一个是用hexo-git-backup插件，另一个是在username.github.io上创建另一个分支进行备份。

这两个方案都偏复杂，第一个引入了额外的依赖，而且看起来和使用的hexo版本还有点关系，第二个用一个branch进行备份略奇怪。

考虑到hexo-deployer-git使用的是.deploy_git目录，与源文件所在目录无关。那么最简单的方案是新开一个repository (public/private均可)，让本地博客文件夹直接track这个新的repository即可。同时注意把不必要的文件和目录用.gitignore去除。

## 常用命令

```bash
git add .
```

```bash
git commit -m "备份"
```

```bash
git push origin master
```

## .gitignore文件

```none
.DS_Store
Thumbs.db
db.json
*.log
*.png
*.jpg
node_modules/
public/
.deploy*/
```

## 查看当前的远程仓库

```shell
$ git remote -v
origin  git@github.com:finisky/finisky.github.io.git (fetch)
origin  git@github.com:finisky/finisky.github.io.git (push)
```

当前的远程仓库和.deploy_git中的远程仓库相同，所以从这里直接push origin master会让github pages失效。

## 在Github上新建一个仓库

点点鼠标即可。记下新仓库的地址`git@github.com:finisky/xxx.git`。

## 修改远程仓库url

```shell
git remote set-url origin git@github.com:finisky/xxx.git
```

查看是否修改成功：

```shell
$ git remote -v
origin  git@github.com:finisky/xxx.git (fetch)
origin  git@github.com:finisky/xxx.git (push)
```

然后直接`git push origin master`即可将博客备份到`git@github.com:finisky/xxx.git`仓库中。同时不影响`hexo deploy`的博客发布。

至于博客的恢复不再赘述，基本的git操作。

> 参考文章
>
> https://hexo.io/zh-cn/docs/
>
> https://godweiyang.com/2018/04/13/hexo-blog/