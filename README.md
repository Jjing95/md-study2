# 长图技术梳理
<a href="https://m.h5in.net/meituan_test/"><img src="./icon.jpg  " width="50px" height="50px" align="left" hspace="10" vspace="6"></a>
[美团美好生活长卷](https://m.h5in.net/meituan_test/)是我在学习长图项目中用来练手的第一个项目，接下来我将从我的角度出发以这个项目为基础来梳理我对长图项目的制作流程与相关技术点。
***
## 长图H5项目
我所掌握的长图项目是公司基于[cocos](https://www.cocos.com/)所搭建的框架来实现的，主要是通过**html**，**css**和**javascript**等一系列前端语言实现的一个移动端用户长屏H5互动页面。
## 目录
   * [简易操作流程图](https://github.com/Jjing95/md-study2/edit/main/README.md#1%E7%AE%80%E6%98%93%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%BE)
   * [长图设计稿处理规范问题](https://github.com/Jjing95/md-study2/edit/main/README.md#2%E9%95%BF%E5%9B%BE%E8%AE%BE%E8%AE%A1%E7%A8%BF%E5%A4%84%E7%90%86%E8%A7%84%E8%8C%83%E9%97%AE%E9%A2%98)
       - [psd目录结构示意图](https://github.com/Jjing95/md-study2/edit/main/README.md#1psd%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84%E7%A4%BA%E6%84%8F%E5%9B%BE)
       - [需要分部加载时的psd](https://github.com/Jjing95/md-study2/edit/main/README.md#2%E9%9C%80%E8%A6%81%E5%88%86%E9%83%A8%E5%8A%A0%E8%BD%BD%E6%97%B6%E7%9A%84psd)
       - [长图部分图层命名规范示意图与详解](https://github.com/Jjing95/md-study2/edit/main/README.md#3%E9%95%BF%E5%9B%BE%E9%83%A8%E5%88%86%E5%9B%BE%E5%B1%82%E5%91%BD%E5%90%8D%E8%A7%84%E8%8C%83%E7%A4%BA%E6%84%8F%E5%9B%BE%E4%B8%8E%E8%AF%A6%E8%A7%A3)
   * [帧动画、音效和分部加载配置文件的规范](https://github.com/Jjing95/md-study2/edit/main/README.md#3%E5%B8%A7%E5%8A%A8%E7%94%BB%E9%9F%B3%E6%95%88%E5%92%8C%E5%88%86%E9%83%A8%E5%8A%A0%E8%BD%BD%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E7%9A%84%E8%A7%84%E8%8C%83)
       - [帧动画配置文件（ani_config.js）](https://github.com/Jjing95/md-study2/edit/main/README.md#1%E5%B8%A7%E5%8A%A8%E7%94%BB%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6ani_configjs)
       - [音效配置文件（effect_config.js）](https://github.com/Jjing95/md-study2/edit/main/README.md#2%E9%9F%B3%E6%95%88%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6effect_configjs)
       - [分部加载配置文件（res_config.js）](https://github.com/Jjing95/md-study2/edit/main/README.md#3-%E5%88%86%E9%83%A8%E5%8A%A0%E8%BD%BD%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6res_configjs)
   * [项目代码中的关键文件]()
       - [index.html]()
### 1、简易操作流程图
下图是我对于长途项目的整体流程的一个简单描述，细节部分请接着往下看。
<img src="./sop.jpg" alt="image" width="474px" height="295px" align="center">
### 2、长图设计稿处理规范问题
#### 1）psd目录结构示意图
<img src="./eg_psd.jpg"></br>
**--type scene**</br>
表示最外层容器，其他所有的长图图层内容都放置于这个容器中，代码框架中也是根据这个**scene**来进行UI部分的页面适配</br></br>
**--type layer**</br>
上图中的`p0_0 --type layer`为一个透明的空白浮层，作为滑动浮层使用</br>
而`p0_2 --type layer`则是放置内容的图层文件，代表这个文件内的所有图层均处于同一页面上，长图项目则主要就为这一页。</br>
#### 2）需要分部加载时的psd
* **game.psd**  放置所有图层，只进行`npm run export2`操作，获取所有图层信息（位置，类型等）
* **game_n.psd**  根据图层的长度均分成n份，放置n份长图的图层，进行`npm run export2000 n`和`npm run pack2000`操作，获取精灵图和背景图（不需要管psd中图层的位置和层级）</br>
**注意：背景和所有的按钮需要放在一开始就加载的psd中**

#### 3）长图部分图层命名规范示意图与详解
* <img src="./eg_btn_ani.png" alt="image">
&emsp;&emsp;按钮相关的图层需要在文件名后面加上<strong>--type button</strong></br>
* <img src="./eg_ani.jpg">
&emsp;&emsp;帧动画的文件组名需要在名字后面加上<strong>--type animation</strong></br>
&emsp;&emsp;<strong>--rate</strong>后面的数字则是控制一秒内显示的图片数量，后面跟的数字越大，帧动画播放越快；反之，越慢。</br>
&emsp;&emsp;<strong>--loop</strong>后面的<strong>true</strong>或者<strong>false</strong>则代表帧动画是否需要循环播放，<strong>true</strong>为循环播放，<strong>false</strong>则为只播放一次。</br>
&emsp;&emsp;<strong>--autoplay</strong>后面的<strong>true</strong>或者<strong>false</strong>则代表的是帧动画是否需要自动播放，<strong>true</strong>为自动播放，<strong>false</strong>则为需要通过事件触发</br>
### 3、帧动画、音效和分部加载配置文件的规范
#### 1）帧动画配置文件（ani_config.js）
```javascript
var anis=[
[name,left,center,0,0,0,isplayed,isloop,1],
[name,left,center,0,0,0,isplayed,isloop,1],
...
]
//[name,left(帧动画的top值),center(帧动画的中心位置),0(移动的x),0(移动的y),0(移动的时间),isplayed(是否已经播放过),isloop(是否循环播放),times(如果为非循环的帧动画，需要重复展示帧动画的次数)]
```
#### 2）音效配置文件（effect_config.js)
```javascript
var effects=[
[name,y,y+h,0,null,loop],
[name,y,y+h,0,null,loop],
...
]
//[name,y（音乐开始播放的y）,y+h（音乐结束播放的y),0,null,isloop(是否循环播放)]
```
#### 3) 分部加载配置文件（res_config.js）
```javascript
game.resList=[
['1',0,4800,false,8], //fales可以直接改为true
['2',500,10000,false,2],
['3',2900,14318,false,2]
];
//123是psd处理时a后面的数字 0，500，2900是指开始加载的位置（提前加载），14318是最大的位置（也就是最后的位置），false代表是否加载过，8，2，2对应精灵图数分别有多少
```
### 4、项目代码中的关键文件
#### 1）index.html
设计实现项目加载页内容和适配原则以及引入原生css文件以及部分需要提前引入的js资源库，下方为简单示例
```html
<link type="text/css" rel="stylesheet" href="css/style.css">
<div id="loading">
  //加载页面的设计与实现
</div>
<script src="libs/Stage.js"></script>
<script src="libs/jquery-2.1.3.min.js"></script>
```
#### 2）BaseScene.js
```javascript
resize: function () {
    var w1 = window.innerWidth;
    var h1 = window.innerHeight;
    var w2 = cc.winSize.width; //750
    var h2 = cc.winSize.height; //1240
    var w3 = cc.visibleRect.width;
    var h3 = cc.visibleRect.height;
    var r1 = w1 / h1;
    var s = 1;
    var scale_level = -1;
    if (w1 > h1) {
        s = w3 / 750; //横屏
    } else {
        s = w3 / 750; //竖屏
    }
    this.scale = s;
    return;
}
```
#### 3）game.js
在这个文件里则主要放置项目所需的接口函数以及一些功能函数，以下是部分示例代码

* 微信端分享部分
```javascript
setShare: function (title, desc, desc2) {
    var link = h5_config.baseLink + h5_config.para;
    var imgUrl = (h5_config.baseUrl || h5_config.baseLink) + 'images/icon.jpg';
    var success1 = function () {
        game.log('meituan_test', "share_sussess" + "_time");
    };
    var success2 = function () {
        game.log('meituan_test', "share_sussess" + "_friend");
    };
    var cancel = function () {
        game.log('meituan_test', "share_sussess" + "_cancel");
    };
    wx.updateTimelineShareData({
        title: title, // 分享标题
        link: link, // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
        imgUrl: imgUrl, // 分享图标
        success: success1,
        cancel:cancel
    });
    wx.updateAppMessageShareData({ 
        title: title, // 分享标题
        desc: desc, // 分享描述
        link: link, // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
        imgUrl: imgUrl, // 分享图标
        success: success2,
        cancel: cancel
    })
}
```
* 通过后端给到的接口将图片转化成base64
```javascript
getBase64:function(data,callback){
    $.get('./api/getBase64/', {
        signature: data.signature,
        timestamp: data.timestamp,
        nonceStr: data.nonceStr,
        ukey:h5_config.ukey,
        url:h5_config.headimgurl
    }, function (res) {
        callback && callback(res);
    }, 'json');
},

```    
#### 4）TLayer.js
项目中的逻辑代码部分则主要在这个文件中实现,以下是部分功能函数代码展示。
