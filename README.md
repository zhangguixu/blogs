# Zhangguixu's Blogs

[Zhangguixu's Blogs](https://zhangguixu.github.io/)

使用hexo+github创建自己的个人网站。[详细教程](https://github.com/zhangguixu/hexo-github-notes)

## 安装

预先需要安装hexo

```shell
npm install -g hexo-cli
```

clone项目到本地

```shell
git clone https://github.com/zhangguixu/blogs.git
```

下载NexT主题，需要注意两点：

1. 需要先下载主题NexT

    ```shell
    git clone https://github.com/iissnan/hexo-theme-next themes/next
    ```

2. 将根目录下的next.conf.yml的内容替换/themes/next/_config.yml，统一配置

安装npm包，

```shell
npm install
```

运行hexo，本地预览已有的博客

```shell
hexo generate
hexo server -s
```

在浏览器打开`localhost:4000`，即可看到效果。

*如果一直打不开，使用-p换一个端口，默认的4000端口在windows下可能被占用了*

目前只能在linux下部署

```shell
hexo deploy
```

估计是插件`hexo-deloyer-git`有问题

## 第三方服务

网站分析

[腾讯分析](http://v2.ta.qq.com/analysis/index)

评论和分享

[多说](http://dev.duoshuo.com/)

本地搜索

```shell
npm install --save hexo-generator-searchdb
```

在站点配置文件`_config.yml`中添加

```yml
# local search
search :
  path : search.xml
  field : post
  format: html
  limit : 10000
```

百度索引(暂时搞不定，算了)

1. 在根目录下添加验证站点文件baidu_verify_xxx.html

## 模板

面试题模板

```shell
hexo new interview 'post'
```

linux模板

```shell
hexo new linux 'linux'
```

数据结构

```shell
hexo new sa 'sa'
```

## 内部文章链接

{% post_link filename title %}

*注意，文件名不用加后缀。*