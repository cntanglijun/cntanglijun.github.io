---
title: 解读 Layabox 示例 09
tags:
  - es5
categories: layabox
date: 2018-06-21 10:38:18
---


本文解读第八个 layabox 引擎示例（`轴心点`）

<!-- more -->

# 示例效果

![result](./result.gif)

# 概念简介

本示例中的概念均在示例一中描述。[查看](/2018/05/25/read-layabox-demo-1/#概念简介)

# 示例代码

```html
<!DOCTYPE html>
<html lang='en' dir='ltr'>
  <head>
    <meta charset='utf-8'>
    <title>轴心点</title>
    <script src='./LayaAirJS_1.7.19.1_beta/js/libs/laya.core.js'></script>
    <script src='./LayaAirJS_1.7.19.1_beta/js/libs/laya.webgl.js'></script>
  </head>
  <body>
    <script>
      (function() {
        var Sprite = Laya.Sprite
        var Stage = Laya.Stage
        var Browser = Laya.Browser
        var WebGL = Laya.WebGL

        var sp1, sp2

        ;(function() {

          // 不支持WebGL时自动切换至Canvas
          Laya.init(Browser.clientWidth, Browser.clientHeight, WebGL)

          Laya.stage.alignV = Stage.ALIGN_MIDDLE
          Laya.stage.alignH = Stage.ALIGN_CENTER

          Laya.stage.scaleMode = 'showall'
          Laya.stage.bgColor = '#232628'

          createApes()
        }());

        function createApes() {

          // 设置间隔距离 300
          var gap = 300

          // 加载猩猩 1，并设置轴心点
          sp1 = new Sprite()
          sp1.loadImage('./res/apes/monkey2.png', 0, 0)
          sp1.pos((Laya.stage.width - gap) / 2, Laya.stage.height / 2)
          sp1.pivot(55, 72)
          Laya.stage.addChild(sp1)

          // 加载猩猩 2，不设置轴心点，默认为左上角
          sp2 = new Sprite()
          sp2.loadImage('./res/apes/monkey2.png', 0, 0)
          sp2.pos((Laya.stage.width + gap) / 2, Laya.stage.height / 2)
          Laya.stage.addChild(sp2)

          // 添加逐帧动画
          Laya.timer.frameLoop(1, this, animate)
        }

        function animate(e) {

          // 以轴心点旋转
          sp1.rotation += 2

          // 以左上角旋转
          sp2.rotation += 2
        }
      }())
    </script>
  </body>
</html>
```

# 参考资料

* [https://www.layabox.com](https://www.layabox.com)
* [https://layaair.ldc.layabox.com/demo/?category=2d&group=Sprite&name=Pivot](https://layaair.ldc.layabox.com/demo/?category=2d&group=Sprite&name=Pivot)
