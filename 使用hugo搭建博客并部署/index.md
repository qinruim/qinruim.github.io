# 使用Hugo搭建博客并部署


# 使用Hugo搭建博客并部署（Dolt主题）

## 概述

Hugo是一个静态网站生成工具，可以用来方便、低成本地搭建一个个人博客。使用Hugo的理由：

1.编译、渲染快，据相关博主提供的数据，他200篇左右的博文用Hexo需要10分钟去生成静态网页，而Hugo 只需要10秒。

2.调试方便，在源文件处修改的内容可以实时地显示在网页上

3.主题多且好看

## 安装Hugo

根据自己的操作系统去[Hugo官网](https://gohugo.io/installation/)下载Hugo

比如Ubantu Linux用户可以直接使用apt安装：

```shell
sudo apt install hugo
```

但这并不是最新版本，如有需要可使用snap安装最新版本的Hugo：

```shell
//安装snap
sudo apt install snap
//使用安装Hugo
sudo snap install hugo
```

下载安装成功后，输入：

```shell
hugo version
```

如果出现版本信息则表示安装成功。

## 新建站点

在自己准备存放博客的目录下输入以下命令即可：

```sh
hugo new <siteName>
```

生成站点的目录结构：[Directory Structure]([Directory Structure | Hugo (gohugo.io)](https://gohugo.io/getting-started/directory-structure/))

然后在

## 安装主题

由于Hugo没有自带主题，所以建立完文件夹后要导入主题文件，否则打网站是一片空白。去[Hugo主题网站](https://themes.gohugo.io/)选择自己喜欢的主题，点击下载会跳转到主题的github主页，根据主题提供的方式下载主题，比如我使用的Dolt主题，可以将主题克隆到站点themes目录：

```sh
git clone https://github.com/HEIGE-PCloud/DoIt.git themes/DoIt
```

然后把主题提供的config.toml文件复制到站点目录，这是Hugo 站点的配置文件，已经写入了主题的可配置字段。

这是我的配置文件，仅供参考：

```toml
baseURL = "https://qinruim.github.io/"
# [en, zh-cn, fr, ...] 设置默认的语言
defaultContentLanguage = "zh-cn"
# 网站语言, 仅在这里 CN 大写
languageCode = "zh-CN"
# 是否包括中日韩文字
hasCJKLanguage = true
# 网站标题
title = "qinruim的笔记本"

# 更改使用 Hugo 构建网站时使用的默认主题
theme = "DoIt"
#theme = "DoIt-0.2.13"
#enableGitInfo = true

[params]
    # DoIt 主题版本
    #version = "0.2.X"
    version = "0.3.X"
    # 网站名称
    title = "qinruim的笔记本"
    # 网站描述
    description = "We will..."
    # 网站关键词
    keywords = ["qinrui", "学习","笔记","记录"]
    #  网站默认主题样式 ("light", "dark", "black", "auto")
    defaultTheme = "auto"
    # 公共 git 仓库路径, 仅在 enableGitInfo 设为 true 时有效
    gitRepo = "https://github.com/qinruim/qinruim.github.io.git"
    #  哪种哈希函数用来 SRI, 为空时表示不使用 SRI
    # ("sha256", "sha384", "sha512", "md5")
    fingerprint = ""
    #  日期格式
    dateFormat = "2006-01-02"
    # 网站图片, 用于 Open Graph 和 Twitter Cards
    images = ["/images/paqia.jpg"]
    #  开启 PWA 支持
    enablePWA = true
    #  版权信息
    license = '本博客所有文章除特別声明外，均采用 <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"> CC BY-SA 4.0 </a> 许可协议，转载请注明出处。'
    [params.app]
        # 当添加到 iOS 主屏幕或者 Android 启动器时的标题, 覆盖默认标题
        title = "qinruim的笔记本"
        # 是否隐藏网站图标资源链接
        noFavicon = false
        # 更现代的 SVG 网站图标(标题左侧的图标), 可替代旧的 .png 和 .ico 文件
        svgFavicon = "/images/paqia.jpg"
        # Safari 图标颜色
        iconColor = "#5bbad5"
        # Windows v8-10磁贴颜色
        tileColor = "#da532c"
    # 页面头部导航栏配置
    [params.header]
        # 桌面端导航栏模式 ("fixed", "normal", "auto")
        desktopMode = "fixed"
        # 移动端导航栏模式 ("fixed", "normal", "auto")
        mobileMode = "auto"
        #  主题切换模式
        # 主题切换模式 ("switch", "select")
        themeChangeMode = "select"
        #  页面头部导航栏标题配置
        [params.header.title]
        # LOGO 的 URL
        logo = ""
        # 标题名称
        name = "qinruim的笔记本"
        # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
        pre = ""
        # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
        post = ""
        #  是否为标题显示打字机动画
        typeit = true

    # 页面底部信息配置
    [params.footer]
        enable = true
        #  自定义内容 (支持 HTML 格式)
        custom = ''
        #  是否显示 Hugo 和主题信息
        hugo = true
        #  是否显示版权信息
        copyright = true
        #  是否显示作者
        author = true
        # 网站创立年份
        since = 2022
        # ICP 备案信息, 仅在中国使用 (支持 HTML 格式)
        icp = ''
        # 许可协议信息 (支持 HTML 格式)
        license = '本博客所有文章除特別声明外，均采用 <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"> CC BY-SA 4.0 </a> 许可协议，转载请注明出处。'

    #  Section (所有文章) 页面配置
    [params.section]
        # section 页面每页显示文章数量
        paginate = 15
        # 日期格式 (月和日)
        dateFormat = "01-02"
        # RSS 文章数目
        rss = 10
        #  最近更新文章设置
        [params.section.recentlyUpdated]
        enable = false
        rss = false
        days = 30
        maxCount = 10

    #  List (目录或标签) 页面配置
    [params.list]
        # list 页面每页显示文章数量
        paginate = 15
        # 日期格式 (月和日)
        dateFormat = "01-02"
        # RSS 文章数目
        rss = 10

    # 主页配置
    [params.home]
        #  RSS 文章数目
        rss = 10
        # 主页个人信息
        [params.home.profile]
            enable = true
            # Gravatar 邮箱, 用于优先在主页显示的头像
            gravatarEmail = ""
            # 主页显示头像的 URL
            # 将你的头像文件放置于 static 或者 assets 目录下
            # 文件路径是相对于 static 或者 assets 目录的
            avatarURL = "/images/paqia.jpg"
            #  主页显示的网站标题 (支持 HTML 格式)
            title = 'qinruim的笔记本'
            # 主页显示的网站副标题
            subtitle = "We will..."
            # 是否为副标题显示打字机动画
            typeit = true
            # 是否显示社交账号
            social = true
            #  免责声明 (支持 HTML 格式)
            disclaimer = ""
            # 主页文章列表
            [params.home.posts]
            enable = true
            # 主页每页显示文章数量
            paginate = 10
            #  被 params.page 中的 hiddenFromHomePage 替代
            # 当你没有在文章前置参数中设置 "hiddenFromHomePage" 时的默认行为
            defaultHiddenFromHomePage = false

    # 作者的社交信息设置
    [params.social]
        GitHub = "qinruim"
        Email = "mqinrui@163.com"
        RSS = true

    #  文章页面配置
    [params.page]
        #  是否在主页隐藏一篇文章
        hiddenFromHomePage = false
        #  是否在搜索结果中隐藏一篇文章
        hiddenFromSearch = false
        #  是否使用 twemoji
        twemoji = false
        # 是否使用 lightgallery
        lightgallery = false
        #  是否使用 ruby 扩展语法
        ruby = true
        #  是否使用 fraction 扩展语法
        fraction = true
        #  是否使用 fontawesome 扩展语法
        fontawesome = true
        # 是否在文章页面显示原始 Markdown 文档链接
        linkToMarkdown = true
        #  配置编辑文章的链接
        linkToEdit = false
        #  是否在 RSS 中显示全文内容
        rssFullText = false
        #  页面样式 ("normal", "wide")
        pageStyle = "normal"
        #  是否在文章开头显示系列导航
        seriesNavigation = true
        #  过时文章提示
        [params.page.outdatedArticleReminder]
            enable = false
            # 如果文章最后更新于 90 天之前，显示提醒
            reminder = 90
            # 如果文章最后更新于 180 天之前，显示警告
            warning = 180
        #  目录配置
        [params.page.toc]
            # 是否使用目录
            enable = true
            #  是否保持使用文章前面的静态目录
            keepStatic = false
            # 是否使侧边目录自动折叠展开
            auto = true
        #  代码配置
        [params.page.code]
            # 是否显示代码块的复制按钮
            copy = true
            # 默认展开显示的代码行数
            maxShownLines = 42
        #  KaTeX 数学公式
        [params.page.math]
            enable = true
            # 默认块定界符是 $$ ... $$ 和 \\[ ... \\]
            # blockLeftDelimiter = ""
            # blockRightDelimiter = ""
            # 默认行内定界符是 $ ... $ 和 \\( ... \\)
            # inlineLeftDelimiter = ""
            # inlineRightDelimiter = ""
            # KaTeX 插件 copy_tex
            copyTex = true
            # KaTeX 插件 mhchem
            mhchem = true
        #  Mapbox GL JS 配置
        [params.page.mapbox]
            # Mapbox GL JS 的 access token
            accessToken = ""
            # 浅色主题的地图样式
            lightStyle = "mapbox://styles/mapbox/light-v9"
            # 深色主题的地图样式
            darkStyle = "mapbox://styles/mapbox/dark-v9"
            # 是否添加 NavigationControl
            navigation = true
            # 是否添加 GeolocateControl
            geolocate = true
            # 是否添加 ScaleControl
            scale = true
            # 是否添加 FullscreenControl
            fullscreen = true
        #  文章页面的分享信息设置
        [params.page.share]
            enable = false
            Twitter = false
            Facebook = false
            Linkedin = false
            Whatsapp = false
            Pinterest = false
            Tumblr = false
            HackerNews = false
            Reddit = false
            VK = false
            Buffer = false
            Xing = false
            Line = true
            Instapaper = false
            Pocket = false
            Digg = false
            Stumbleupon = false
            Flipboard = false
            Weibo = true
            Renren = false
            Myspace = true
            Blogger = true
            Baidu = false
            Odnoklassniki = false
            Evernote = true
            Skype = false
            Trello = false
            Mix = false

    #  兼容性设置
    [params.compatibility]
        # 是否使用 Polyfill.io 来兼容旧式浏览器
        polyfill = false
        # 是否使用 object-fit-images 来兼容旧式浏览器
        objectFit = false

[menu]
    [[menu.main]]
        identifier = "posts"
        # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
        pre = ""
        # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
        post = ""
        name = "文章"
        url = "/posts/"
        # 当你将鼠标悬停在此菜单链接上时, 将显示的标题
        title = ""
        weight = 1
    [[menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "标签"
        url = "/tags/"
        title = ""
        weight = 2
    [[menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "分类"
        url = "/categories/"
        title = ""
        weight = 3
    [[menu.main]]
        identifier = "about"
        pre = ""
        post = ""
        name = "关于"
        url = "/about/"
        title = ""
        weight = 4



# Hugo 解析文档的配置
[markup]
    # 语法高亮设置
    [markup.highlight]
        codeFences = true
        guessSyntax = true
        lineNos = true
        lineNumbersInTable = true
        # false 是必要的设置
        # (https://github.com/dillonzq/LoveIt/issues/158)
        noClasses = false
    # Goldmark 是 Hugo 0.60 以来的默认 Markdown 解析库
    [markup.goldmark]
        [markup.goldmark.extensions]
            definitionList = true
            footnote = true
            linkify = true
            strikethrough = true
            table = true
            taskList = true
            typographer = true
        [markup.goldmark.renderer]
            # 是否在文档中直接使用 HTML 标签
            unsafe = true
    # 目录设置
    [markup.tableOfContents]
        startLevel = 2
        endLevel = 6

# 作者配置
[author]
    name = "qinruim"
    email = "mqinrui@163.com"
    link = ""
    avatar = "/images/paqia.jpg"
    gravatarEmail = ""

# 网站地图配置
[sitemap]
    changefreq = "weekly"
    filename = "sitemap.xml"
    priority = 0.5

# Permalinks 配置
[Permalinks]
    # posts = ":year/:month/:filename"
    posts = ":filename"

# 用于输出 Markdown 格式文档的设置
[mediaTypes]
    [mediaTypes."text/plain"]
    suffixes = ["md"]

# 用于输出 Markdown 格式文档的设置
[outputFormats.MarkDown]
    mediaType = "text/plain"
    isPlainText = true
    isHTML = false

# 用于 Hugo 输出文档的设置
[outputs]
    #
    home = ["HTML", "RSS", "JSON"]
    page = ["HTML", "MarkDown"]
    section = ["HTML", "RSS"]
    taxonomy = ["HTML", "RSS"]
    taxonomyTerm = ["HTML"]

# 用于分类的设置
[taxonomies]
    author = "authors"
    category = "categories"
    tag = "tags"
    series = "series"
```

## 本地构建

使用命令：

```sh
hugo server
```

就可以在本地运行服务了，跳转到`http://localhost:1313/`即可查看生成的站点

## 写博客

输入

```sh
hugo new posts/文章名称.md
```

这时候就会在文件夹 `content/posts`形成你要的markdown文件，打开进行编辑即可。

在文章里使用本地图片：

如果文章index.md所在文件夹为'directory'，里面放图片如叫做 picture.png 的图片，那么在index.md里面调用的时候可以这样写: ![](picture.png) 。

注意，markdown文件中的 `front matter` 部分有一个`draft` 参数，如果`draft`设置为`true` 则可正常渲染，如果设置为`false`则不予以渲染。相应的如果想查看全部效果则输入`hugo server -D` 表示将草稿文件也进行渲染。

## 部署到github

Github Pages功能可以托管静态页面进行自动渲染。首先在GitHub上创建一个Repository，命名为：`qinruim.github.io（qinruim替换为你的github用户名）。

在站点根目录执行 `Hugo` 命令生成最终页面：

```sh
hugo
```

如果一切顺利，所有静态页面都会生成到 `public` 目录，将pubilc目录里所有文件 `push` 到刚创建的Repository的 `main` 分支。

```sh
cd public
git init
git remote add origin https://github.com/qinruim/qinruim.github.io.git
git add -A
git commit -m "first commit"
git push -u origin master
```

浏览器里访问：`http://qinruim.github.io/`
