# 创建GitHub Pages博客

个人博客选择GitHub Pages是方便，适合程序猿，编写MD文件push触发Action完成编译，10秒刷新页面博客就更新了。Mkdocs/Mkdocs Material比较大方美观，是Google推行的Material Design样式。

## 安装需要的软件包
需要python3.x和pip 3.x安装。

    $ python --version
    Python 3.8.2
    $ pip --version
    pip 20.0.2 from /usr/local/lib/python3.8/site-packages/pip (python 3.8)

## 新建GitHub项目
项目名字需要谨慎，因为名字是最终的pages的路径，格式是这样的：`https://<username>.github.io/<projectName>`。并在master下创建下面两个文件。

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.


`mkdocs.yml`内容：

    site_name: My Docs

`index.md`内容：
    
    # Welcome to MkDocs

    For full documentation visit [mkdocs.org](https://www.mkdocs.org).

    ## Commands

    * `mkdocs new [dir-name]` - Create a new project.
    * `mkdocs serve` - Start the live-reloading docs server.
    * `mkdocs build` - Build the documentation site.
    * `mkdocs -h` - Print help message and exit.

    ## Project layout

        mkdocs.yml    # The configuration file.
        docs/
            index.md  # The documentation homepage.
            ...       # Other markdown pages, images and other files.


## 配置流水线
![](https://img.alicdn.com/imgextra/i3/O1CN016FJ1c71IAG7tolImQ_!!6000000000852-2-tps-1116-232.png)

选择简单的流水线即可
![](https://img.alicdn.com/imgextra/i2/O1CN01uslMcl1P94PORKA2A_!!6000000001797-2-tps-778-448.png)
填上下面的代码，会自动触发编译，输出静态HTML文件到`gh-deploy`分支，这个在开启pages是否需要之一，需要选定这个分支。

    name: ci
    on:
    push:
        branches:
        - master
        - main
    jobs:
    deploy:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - uses: actions/setup-python@v2
            with:
            python-version: 3.x
        - run: pip install mkdocs-material
        - run: mkdocs gh-deploy --force

## 开启Pages
![](https://img.alicdn.com/imgextra/i2/O1CN01OMnNCK28klicUrehn_!!6000000007971-2-tps-1366-134.png)

主要看分支

![](https://img.alicdn.com/imgextra/i4/O1CN01OuP68R1PhsVegPZqL_!!6000000001873-2-tps-1480-580.png)

## 看效果
![](https://img.alicdn.com/imgextra/i3/O1CN01P99uR11VfwWvn9T0W_!!6000000002681-2-tps-2482-1252.png)

另外，上传代码后触发部署，看下流水线的效果，啧啧，方便。

![](https://img.alicdn.com/imgextra/i4/O1CN01LSx55a1wHClOQmJhV_!!6000000006282-2-tps-2784-1056.png)