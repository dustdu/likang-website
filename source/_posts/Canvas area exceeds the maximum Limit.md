---
title: Canvas area exceeds the maximum Limit
date: 2022-10-11 16:51:21
tags: canvas
categories: canvas
keywords: canvas
description: Canvas area exceeds the maximum Limit
top_img:
cover:
---

## Canvas area exceeds the maximum Limit

目前是{% label 2022 orange %}年，Safari仍然将Canvas画布限制在{% label 16777216 orange %}像素。我们所绘制的画布超出这一限制，打开控制台就会看到警告
        
        Canvas area exceeds the maximum Limit(width*height > 16777216)

 [目前在微信小程序中也有限制，根据社区里的发现，宽高限制在了4096，4096*4096 = 16777216](https://developers.weixin.qq.com/community/develop/doc/0008cabf8c05589f1aec3da6959c00?highLine=canvas%25204000)

## 创建画布

- 在创建画布时，需要把像素保持在这个范围内，虽然微信对宽高进行了限制，但在Safari里，只需限制width*height即可
- 如果需要根据图片进行绘制，就需要根据图片比例进行计算得到width和height后绘制

        function limitSize(width, height, maximumPixels = 16777216) {
            const pixels = width * height;

            if (pixels <= maximumPixels) {
                return { width, height };
            } else {
                const scalar = Math.sqrt(maximumPixels) / Math.sqrt(pixels);
                return {
                    width: Math.floor(width * scalar),
                    height: Math.floor(height * scalar),
                };
            } 
        }

