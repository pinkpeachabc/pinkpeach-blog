---
title: Blog定位方向和主题选择
date: 2020-02-08 15:40:13
tag: 
- hexo
- 小记
categories:
- 博客
thumbnail: https://cdn.jsdelivr.net/gh/pinkpeachabc/images/Blog-imgs/%E5%8D%9A%E5%AE%A22.png
sticky: 2
---

## 关于Blog

> 本站历史
<p>博客从<ahref="http://localhost:4000/2019/12/29/%E8%A7%86%E5%9B%BE%E7%9A%84%E6%93%8D%E4%BD%9C"><strong>2019.8.11</strong></a>至今已经运行<span id="htmer_time" style="color: #90CAF9; font-weight: bold;"></span>由于磕磕绊绊只能从19年开始计算😁</p>


- 2018.8月建立，使用开源博客程序Jekyll，托管于GIthub pages，域名为`pinkpeachabc.githu.io`
- 2018.12月，更换为开源博客程序hexo，托管于GIthub pages
- 2019.3月，由于访问速度原因，将博客迁移阿里云，域名为`pinkpeachabc.cn`
- 2020.2月，主题由[Archer](https://github.com/fi3ework/hexo-theme-archer)换为[Typography](https://github.com/SumiMakito/hexo-theme-typography)
- 2020.5月，很可惜[Typography](https://github.com/SumiMakito/hexo-theme-typography)对排版的支持很差，不得已抛弃，主题换为[inside](https://github.com/ikeq/hexo-theme-inside).

## 起步

>📝记录从初识到熟悉的过程

第一次搭建blog的准确时间是2018年的8月份，出于分享和写作。我初建是Github pages + Jekyll的组合方式。

- 博客版本管理
- 静态博客网站
- 不需要像WordPress那样繁琐(~~其实是比较懒~~)
- 可以直接在github网页版上编辑和发布博客

总之是把博客搭建好了，可之后的过程我变没在管过。由于各式各样的原因(~~就是玩去了~~)也不写文章，于是我的第一个博客也就经过长时间的吃土💸，直至我最终把它抛弃。

## 再次起步

![博客](https://tva1.sinaimg.cn/large/0082zybply1gbp30n0h1jj31ey0u0dqs.jpg)

由于上一次的失败，我便很久没有再次搭建博客的想法了。但是我本人喜欢看科技文章，看的久了也想自己写点把自己知道的分享给其他人。由于刚好那时候在学习前端的东西。于是我想不如在搭建一个吧。那时候想想其实写文章发布到网上的平台很多，没必要单独自己搭建一个。

- 博客园
- CSDN
- 简书
- 知乎

还有很多很多就不多赘述了，其实真正再次搭建是觉得自己操作可以学习Git和其他方面的只是于是就开始二次起步。

这一次使用的和第二次不同这次是Github + hexo的组合，搭建起来也是比较轻松。直接放到了github上面取名`Pinkpeachabc.github.io`并选择了[Archer](https://github.com/fi3ework/hexo-theme-archer)作为博客的主题。

出于Github的服务器在国外，国内的访问速度很缓慢（~~龟速~~）。于是我在阿里云购买了服务器，并且购买第一个域名`pinkpeachabc.cn`我也没辜负之死去的博客，从建站至今我还在更新着博客，虽然目前没什么技术含量。起码不会再让它吃土了😁

## 至今

可以看到现在的主题已经更换为 [Typography](https://github.com/SumiMakito/hexo-theme-typography)当然了我并不是喜新厌旧🌶，经过这几个月的运营博客来看，我太注重外观反而缺少了对阅读和观感体验（~~注重图片添加无用插件等等~~）。同样的我也开始想起建博客的初衷。这个是主题是我无意间看到了给我简洁而不失美观的感觉。想初衷的作者一样——**重新发现 文字之美**

很可惜[Typography](https://github.com/SumiMakito/hexo-theme-typography)对于排版不是很友好，并且不支持目录，我目前的能力没有办法完善，只能对它说抱歉了。由于疫情的原因，学校🏫也暂未开学。这期间我对博客以后的方向思考了很多，我将会把学习中的笔记整理发布在博客中(尽最大可能写优质)，我也会删除一些我自认为~~无用~~的文章，让整个博客看起来更高效优质——**2020-5-20**

## 致谢

对于以上的所有作者我由衷的表示感谢，**开源分享、技术无价**。同时本次应用的并不是原版的[Typography](https://github.com/SumiMakito/hexo-theme-typography)本是基于[journey.ad](https://imjad.cn/)修改过的版本。由于这次的主题`layout`里面是`jade`写的所以修改起来可能有点难度，所以我直接~~抄~~借鉴了过来。

<script>
function secondToDate(second) {
     if (!second) {
         return 0;
     }
     var time = new Array(0, 0, 0, 0, 0);
     if (second >= 365 * 24 * 3600) {
        time[0] = parseInt(second / (365 * 24 * 3600));
        second %= 365 * 24 * 3600;
    }
    if (second >= 24 * 3600) {
        time[1] = parseInt(second / (24 * 3600));
        second %= 24 * 3600;
    }
    if (second >= 3600) {
        time[2] = parseInt(second / 3600);
        second %= 3600;
    }
    if (second >= 60) {
        time[3] = parseInt(second / 60);
        second %= 60;
    }
    if (second > 0) {
        time[4] = second;
    }
    return time;
};
function setTime() {
         // 博客创建时间秒数，时间格式中，月比较特殊，是从0开始的，所以想要显示5月，得写4才行，如下
         var create_time = Math.round(new Date(Date.UTC(2019, 8, 11, 18, 37, 16)).getTime() / 1000);// 当前时间秒数,增加时区的差异
         var timestamp = Math.round((new Date().getTime() + 8 * 60 * 60 * 1000) / 1000);
         currentTime = secondToDate((timestamp - create_time));
         if (currentTime[0]==0){
             currentTimeHtml = currentTime[1] + '天'+ currentTime[2] + '时' + currentTime[3] + '分' + currentTime[4] + '秒';
         }else{
             currentTimeHtml = currentTime[0] + '年' + currentTime[1] + '天' + currentTime[2] + '时' + currentTime[3] + '分' + currentTime[4] + '秒';
         }
         // 兼容pjax，当htmer_time存在时输出，否则清空计时器
         if (document.getElementById("htmer_time")){
             document.getElementById("htmer_time").innerHTML = currentTimeHtml;
         }else{
              clearInterval(timer);
         }
}
var timer = setInterval(setTime, 1000);
</script>
