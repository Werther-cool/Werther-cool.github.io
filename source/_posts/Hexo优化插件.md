layout: '[layout]'
title: Hexo优化插件
date: 2017-02-20 16:34:29
tags:
---

<ul>
<li>1.安装Hexo</li>
<li>2.部署Hexo</li>
<li>3.Hexo命令</li>
<li>4.一些报错处理</li>
<li>5.博客管理</li>
<li>6.插件（RSS、Sitemap）</li>
<li>7.评论设置</li>
<li>8.404页面</li>
<li>9.统计</li>
<li>10.更新</li>
<li>11.总结</li>
<li>12.参考引用</li>
<li>13.搭建博客相关网站</li>
</ul>
<h3>简述</h3>
<p>本文主要讲解Hexo安装时遇到的坑，Hexo安装之后的使用教程，Hexo安装需要的环境和教程，请自行百度、谷歌。</p>
<h4>1.安装Hexo</h4>
<pre><code> $ npm install -g hexo</code></pre>
<h6>坑1</h6>
<p>这里可能安装失败，可能权限不够，在命令前加<code>sudo</code></p>
<pre><code> $ sudo npm install -g hexo</code></pre>
<h4>2.部署Hexo</h4>
<pre><code> $ hexo init</code></pre>
<h6>注：这个命令会初始化博客的目录，所以，执行这个命令时，在你想创建的目录下执行，就自动生成到对应目录下。</h6>
<p>执行命令生，会在当前命令的路径下，生成以下文件：</p>
<pre><code>    .
    ├── .deploy
    ├── public
    ├── scaffolds
    ├── scripts
    ├── source
    |   ├── _drafts
    |   └── _posts
    ├── themes
    ├── _config.yml
    └── package.json</code></pre>
<ul>
<li>.deploy：执行hexo deploy命令部署到GitHub上的内容目录</li>
<li>public：执行hexo generate命令，输出的静态网页内容目录</li>
<li>scaffolds：layout模板文件目录，其中的md文件可以添加编辑</li>
<li>scripts：扩展脚本目录，这里可以自定义一些javascript脚本</li>
<li>source：文章源码目录，该目录下的markdown和html文件均会被hexo处理。该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等都应该放这里，该目录下可新建页面目录。</li>
<li>_drafts：草稿文章</li>
<li>_posts：发布文章</li>
<li>themes：主题文件目录</li>
<li>_config.yml：全局配置文件，大多数的设置都在这里</li>
<li>package.json：应用程序数据，指明hexo的版本等信息，类似于一般软件中的关于按钮</li>
</ul>
<h4>3.Hexo命令</h4>
<p>Hexo下，通过 <code>_config.yml</code> 设置博客，可以想象成我们用的软件里的设置一样，只是它通过一个文件列出这些参数，然后让我们填写和修改。</p>
<ul>
<li>全局设置</li>
</ul>
<p>在你博客目录下有一个文件名<code>_config.yml</code>，打开可以配置信息。</p>
<ul>
<li>局部页面</li>
</ul>
<p>在你博客目录下 <code>\themes\你使用的主题\_config.yml</code> </p>
<ul>
<li>写博客相关命令</li>
</ul>
<pre><code>    Hexo常用命令：

    hexo new "postName"       #新建文章
    hexo new page "pageName"  #新建页面
    hexo generate             #生成静态页面至public目录
    hexo server               #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
    hexo deploy               #将.deploy目录部署到GitHub</code></pre>
<p>当然，如果每次输入那么长命令，那么一定想到用<strong>简写</strong>：</p>
<pre><code>    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy</code></pre>
<p>其它的，还可以<strong>复合命令</strong>：</p>
<pre><code>    hexo deploy -g
    hexo server -g</code></pre>
<p>有时候生成的网页出错了，而生成的rss其实没有清除，那么用下面的命令，在重新生成吧</p>
<pre><code>    $ hexo clean</code></pre>
<p>当本地调试出现诡异现象时候，请先使用 hexo clean 清理已经生成的静态文件后重试。</p>
<blockquote><p>注：Hexo原理就是hexo在执行hexo generate时会在本地先把博客生成的一套静态站点放到public文件夹中，在执行hexo deploy时将其复制到.deploy文件夹中。Github的版本库通常建议同时附上README.md说明文件，但是hexo默认情况下会把所有md文件解析成html文件，所以即使你在线生成了README.md，它也会在你下一次部署时被删去。怎么解决呢？<br>在执行hexo deploy前把在本地写好的README.md文件复制到.deploy文件夹中，再去执行hexo deploy。</p></blockquote>
<h3>4.一些报错处理</h3>
<h6>坑2</h6>
<ul>
<li>
<p>一</p>
<blockquote><p>ERROR Plugin load failed: hexo-server<br>原因：<br>Besides, utilities are separated into a standalone module. hexo.util is not reachable anymore.<br>解决方法，执行命令：<br>sudo npm install hexo-server</p></blockquote>
</li>
<li>
<p>二</p>
<blockquote><p>执行命令hexo server，有如下提示：<br>Usage: hexo<br>….<br>原因：<br>我认为是没有生成本地服务<br>解决方法，执行命令：<br>npm install hexo-server --save<br>提示：hexo-server@0.1.2 node_modules/hexo-server</p></blockquote>
</li>
</ul>
<ul>
<li>三<blockquote><p>白板和Cannot GET / 几个字<br>原因:<br>由于2.6以后就更新了，我们需要手动配置些东西，我们需要输入下面三行命令：</p></blockquote>
</li>
</ul>
<pre><code>    npm install hexo-renderer-ejs --save
    npm install hexo-renderer-stylus --save
    npm install hexo-renderer-marked --save
    这个时候再重新生成静态文件，命令：
    hexo generate （或hexo g）
    启动本地服务器：
    hexo server （或hexo s）</code></pre>
<h4>5.博客管理</h4>
<p>上面命令中，其实生成文章，可以直接把写好的文章插入到目录<code>/_posts</code> 下面，后缀为.MD就行，在文章头部固定格式：</p>
<pre><code>    title: Mac提高使用效率的一些方法   #文章的标题，这个才是显示的文章标题，其实文件名不影响
    date: 2015-09-01 20:33:26      #用命令会自动生成，也可以自己写，所以文章时间可以改
    categories: technology         #文章的分类，这个可以自己定义
    tags: [Mac,效率,快捷方式]        #tag，为文章添加标签，方便搜索
    ---</code></pre>
<p>当然，里面有很多东西的，如果你专注于写作，那么可以不用太关心了，比如tags标签可以写成下面那样，因为hexo文章的头部文件是用<a href="https://en.wikipedia.org/wiki/YAML" target="_blank">AML</a>来写的。</p>
<pre><code>    tags:
    - tag1
    - tag2</code></pre>
<p>如果在博客文章列表中，不想全文显示，可以增加 &lt;!--more--&gt;, 后面的内容就不会显示在列表。</p>
<pre><code>     &lt;!--more--&gt;</code></pre>
<h4>6.插件</h4>
<ul>
<li>
<p>安装插件</p>
<pre><code>  $ npm install &lt;plugin-name&gt; --save</code></pre>
</li>
<li>
<p>添加RSS</p>
<pre><code>  npm install hexo-generator-feed</code></pre>
<p>然后，到博客目录 /public 下，如果没有发现atom.xml，说明命令没有生效！！！(楼主就是在这里被坑了次)<br>解决方法：</p>
<pre><code>  $ npm install hexo-generator-feed --save</code></pre>
<p>这个命令来自<a href="https://www.npmjs.com/package/hexo-generator-feed" target="_blank">hexo-generator-feed</a></p>
<pre><code>  Install
     $ npm install hexo-generator-feed --save
   Hexo 3: 1.x
   Hexo 2: 0.x
  Options
     You can configure this plugin in _config.yml.

    feed:
       type: atom
       path: atom.xml
       limit: 20

      type - Feed type. (atom/rss2)
      path - Feed path. (Default: atom.xml/rss2.xml)
      limit - Maximum number of posts in the feed (Use 0 or false to show all posts)</code></pre>
</li>
</ul>
<p>其中可以选择：<br>然后在 Hexo 根目录下的 _config.yml 里配置一下</p>
<pre><code>    feed:
        type: atom
        path: atom.xml
        limit: 20
    #type 表示类型, 是 atom 还是 rss2.
    #path 表示 Feed 路径
    #limit 最多多少篇最近文章</code></pre>
<p>最后，在 <code>hexo generate</code>之后，会发现public文件夹下多了atom.xml！</p>
<p>例如要订阅我的blog只要输入<code>ihtc.cc/atom</code>就可以搜寻到啦！</p>
<ul>
<li>添加Sitemap<blockquote><p>Sitemap 的提交主要的目的，是要避免搜索引擎的爬虫没有完整的收录整个网页的内容，所以提交 Sitemap 是能够补足搜索引擎的不足，进而加速网页的收录速度，达到搜寻引擎友好的目的。</p></blockquote>
</li>
</ul>
<pre><code>    $ npm install hexo-generator-sitemap --save</code></pre>
<p>这个命令来自<a href="https://www.npmjs.com/package/hexo-generator-sitemap" target="_blank">hexo-generator-sitemap</a></p>
<pre><code>    Install
        $ npm install hexo-generator-sitemap --save

        Hexo 3: 1.x
        Hexo 2: 0.x
    Options
        You can configure this plugin in _config.yml.

        sitemap:
            path: sitemap.xml
        path - Sitemap path. (Default: sitemap.xml)</code></pre>
<p>同样可以选择：<br>在 Hexo 根目录下的 _config.yml 里配置一下</p>
<pre><code>        sitemap:
           path: sitemap.xml
           #path 表示 Sitemap 的路径. 默认为 sitemap.xml.</code></pre>
<p>对于国内用户还需要安装插件 hexo-generator-baidu-sitemap, 顾名思义是为百度量身打造的. 安装</p>
<pre><code>        $ npm install hexo-generator-baidu-sitemap --save</code></pre>
<p>然后在 Hexo 根目录下的 _config.yml 里配置一下</p>
<pre><code>       baidusitemap:
            path: baidusitemap.xml</code></pre>
<p>为了博客有更好的展示率, 最好的方式是通过搜索引擎, 提交 Sitemap文件是一个方式，具体可参考：</p>
<ul>
<li><a href="http://lukang.me/2015/optimization-of-hexo-2.html" target="_blank">Hexo 优化与定制(二) | Kang Lu's Blog</a></li>
<li>
<p><a href="http://fionat.github.io/blog/2013/10/23/sitemap/" target="_blank">｜Hexo优化｜如何向google提交sitemap（详细） | Fiona's Blog</a></p>
</li>
<li>
<p>其它插件<br><a href="https://github.com/hexojs/hexo/wiki/Plugins" target="_blank">Plugins · hexojs/hexo</a></p>
</li>
</ul>
<h4>7.评论设置</h4>
<p>在Hexo中，默认使用的评论是国外的Disqus,不过因为国内的”网络环境”问题，我们改为国内的<a href="http://duoshuo.com" target="_blank">多说</a>评论系统。</p>
<p>需要说明的是 <code>short_name:</code>字段，这个字段为你多说填写的站点名字，比如我的域名：ihtcboy.duoshuo.com，那么我的short_name:"ihtcboy"</p>
<h4>8.404页面</h4>
<blockquote><p>GitHub Pages 自定义404页面非常容易，直接在根目录下创建自己的404.html就可以。但是自定义404页面仅对绑定顶级域名的项目才起作用，GitHub默认分配的二级域名是不起作用的，使用hexo server在本机调试也是不起作用的。<br>其实，404页面可以做更多有意义的事，来做个404公益项目吧。</p></blockquote>
<p>腾讯公益 404.html :</p>
<pre><code>    &lt;html&gt;
    &lt;head&gt;   
        &lt;meta charset="UTF-8"&gt;
        &lt;title&gt;404&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
    &lt;br&gt;&lt;!--
    &lt;!DOCTYPE HTML&gt;
    &lt;html&gt;
    &lt;head&gt;
        &lt;meta charset="UTF-8" /&gt;
        &lt;title&gt;公益404 | 不如&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
    #404 Not found By Bruce
    &lt;h1&gt;404 Page Not Found&lt;/h1&gt;
    --&gt;&lt;br&gt;&lt;script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8"&gt;&lt;/script&gt;&lt;br&gt;&lt;!--
    公益404介接入地址
    益云公益404 http://yibo.iyiyun.com/Index/web404
    腾讯公益404 http://www.qq.com/404
    失蹤兒童少年資料管理中心404 http://404page.missingkids.org.tw
    --&gt;
    &lt;br&gt;
    &lt;/body&gt;
    &lt;/html&gt;</code></pre>
<p>复制上面代码，贴粘到目录下新建的404.html即可！</p>
<h4>9.统计</h4>
<blockquote><p>因Google Analytics偶尔被墙，故国内用百度统计</p></blockquote>
<p>最新的统计服务已经开放，两行代码轻松搞定，你可以直接使用：<a href="http://service.ibruce.info" target="_blank">不蒜子</a><br>本人墙裂推荐，只需要两行代码哦。各种用法实例和显示效果参考不蒜子文档中的实例链接。不蒜子，极客的算子，极简的算子，任你发挥的算子。</p>
<ul>
<li><a href="http://ibruce.info/2013/12/22/count-views-of-hexo/" target="_blank">为hexo博客添加访问次数统计功能 | 不如</a></li>
</ul>
<h4>10.更新</h4>
<ul>
<li>更新hexo：<pre><code>  npm update -g hexo</code></pre>
</li>
<li>更新主题：<pre><code>  cd themes/你的主题
  git pull</code></pre>
</li>
<li>更新插件：<pre><code>  npm update</code></pre>
</li>
</ul>
<h4>11.总结</h4>
<p>本文主要是解释了自己搭建过程中遇到的问题，还有综合了其它Hexo教程的总结，还有图床、搜索、CDN加速等内容没有说到，大家用到可以自行百度谷歌！</p>
<h3>12.参考引用</h3>
<p><a href="http://cnfeat.com/blog/2014/05/10/how-to-build-a-blog/" target="_blank">如何搭建一个独立博客——简明Github Pages与Hexo教程</a><br><a href="http://zipperary.com/2013/05/28/hexo-guide-1/" target="_blank">hexo系列教程：（一）hexo介绍 | Zippera's blog</a><br><a href="http://zipperary.com/2013/05/28/hexo-guide-2/" target="_blank">hexo系列教程：（二）搭建hexo博客 | Zippera's blog</a><br><a href="http://ibruce.info/2013/11/22/hexo-your-blog/" target="_blank">hexo你的博客 | 不如</a><br><a href="http://yangjian.me/workspace/building-blog-with-hexo/" target="_blank">使用hexo搭建博客 | Alimon's Blog</a><br><a href="http://blog.sunnyxx.com/2014/02/27/hexo_startup/" target="_blank">hexo边搭边记 | sunnyxx的技术博客</a><br><a href="http://code.wileam.com/build-a-hexo-blog-and-optimize/" target="_blank">hexo搭建静态博客以及优化 | Joanna's coding blog</a><br><a href="http://www.jianshu.com/p/465830080ea9/comments/550752#comment-550752" target="_blank">HEXO+Github,搭建属于自己的博客 - 简书</a><br><a href="http://code.kpman.cc/2013/05/08/%E5%9C%A8hexo%E8%87%AA%E8%A8%82rss/" target="_blank">在hexo自訂rss | kpman | code</a><br><a href="http://michaelhsu.tw/2013/05/05/rssatom-sitemap-for-seo/" target="_blank">RSS/Atom、Sitemap for SEO | Michael Hsu.tw</a><br><a href="http://lukang.me/2015/optimization-of-hexo-2.html" target="_blank">Hexo 优化与定制(二) | Kang Lu's Blog</a><br><a href="http://ijiaober.github.io/categories/hexo/" target="_blank">Hexo | { GoonX }</a><br><a href="http://ibruce.info/2015/04/04/busuanzi/" target="_blank">不蒜子 | 不如</a></p>


