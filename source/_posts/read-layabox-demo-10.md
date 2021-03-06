---
title: 解读 Layabox 示例 10
tags:
  - es5
categories: layabox
date: 2018-06-21 10:50:32
---


本文解读第十个 layabox 引擎示例（`切换纹理`）

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
    <title>切换纹理</title>
    <script src='./LayaAirJS_1.7.19.1_beta/js/libs/laya.core.js'></script>
    <script src='./LayaAirJS_1.7.19.1_beta/js/libs/laya.webgl.js'></script>
  </head>
  <body>
    <script>
      (function() {
        var Sprite = Laya.Sprite
        var Stage = Laya.Stage
        var Texture = Laya.Texture
        var Browser = Laya.Browser
        var Handler = Laya.Handler
        var WebGL = Laya.WebGL

        var texture1 = './res/apes/monkey2.png'
        var texture2 = './res/apes/monkey3.png'
        var flag = false

        var ape

        ;(function() {

          // 不支持WebGL时自动切换至Canvas
          Laya.init(Browser.clientWidth, Browser.clientHeight, WebGL)

          Laya.stage.alignV = Stage.ALIGN_MIDDLE
          Laya.stage.alignH = Stage.ALIGN_CENTER

          Laya.stage.scaleMode = 'showall'
          Laya.stage.bgColor = '#232628'

          // 加载资源
          Laya.loader.load([ texture1, texture2 ], Handler.create(this, onAssetsLoaded))
        }());

        function onAssetsLoaded() {

          // 实例化一个猩猩
          ape = new Sprite()

          // 设置轴心点
          ape.pivot(55, 72)

          // 设置坐标位置
          ape.pos(Laya.stage.width / 2, Laya.stage.height / 2)

          // 添加到舞台中
          Laya.stage.addChild(ape)

          // 显示默认纹理
          switchTexture()

          // 点击时切换纹理
          ape.on('click', this, switchTexture)
        }

        function switchTexture() {
          var textureUrl = (flag = !flag) ? texture1 : texture2

          // 清空上一次绘制的图像
          ape.graphics.clear()

          // 加载新图像
          var texture = Laya.loader.getRes(textureUrl)

          // 绘制纹理
          ape.graphics.drawTexture(texture, 0, 0)

          // 重置绘制图像的宽高
          ape.size(texture.width, texture.height)
        }
      }())
    </script>
  </body>
</html>
```

# 参考资料

* [https://www.layabox.com](https://www.layabox.com)
* [https://layaair.ldc.layabox.com/demo/?category=2d&group=Sprite&name=SwitchTexture](https://layaair.ldc.layabox.com/demo/?category=2d&group=Sprite&name=SwitchTexture)
