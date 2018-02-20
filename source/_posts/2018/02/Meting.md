---
title: Meting & APlayer
date: 2018-02-17 23:38:20
categories: 随笔
tags: [音乐, 游戏, 黑暗之魂, DarkSouls]
scroll2more: false
copyright:
    disable: true
---

<p align="center">
<img class="img-no-bd" src="https://user-images.githubusercontent.com/2666735/30651452-58ae6c88-9deb-11e7-9e13-6beae3f6c54c.png" alt="Meting">
</p>

<p align="center">
<a style="display: inline-block;" href="https://i-meto.com"><img class="img-no-bd" alt="Author" src="https://img.shields.io/badge/Author-METO-blue.svg?style=flat-square"/></a>
<a style="display: inline-block;" href="https://www.npmjs.com/package/meting"><img class="img-no-bd" alt="Version" src="https://img.shields.io/npm/v/meting.svg?style=flat-square"/></a>
<a style="display: inline-block;" href="https://travis-ci.org/metowolf/MetingJS"><img class="img-no-bd" alt="Travis" src="https://img.shields.io/travis/metowolf/MetingJS.svg?style=flat-square"></a>
<a style="display: inline-block;" href=""><img class="img-no-bd" alt="License" src="https://img.shields.io/npm/l/meting.svg?style=flat-square"/></a>
</p>

<!-- data-id="60198" -->

<div class="aplayer"
    data-id="1984937420"
    data-server="netease"
    data-autoplay="false"
    data-type="playlist">
</div>

<!-- more -->


# Meting
---

## Requirement
https://github.com/MoePlayer/APlayer

## CDN
https://cdn.jsdelivr.net/npm/meting/dist/Meting.min.js
https://unpkg.com/meting/dist/Meting.min.js

## Quick Start
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.6.0/APlayer.min.js"></script>

<div class="aplayer"
    data-id="60198"
    data-server="netease"
    data-type="playlist">
</div>
<script src="dist/Meting.min.js"></script>
```
https://music.163.com/#/playlist?id=60198

## Option

|option|default|description|
|:-----|:-------------:|:----------|
|data-id|**require**|song id / playlist id / album id / search keyword|
|data-server|**require**|music platform: `netease`, `tencent`, `kugou`, `xiami`, `baidu`|
|data-type|**require**|`song`, `playlist`, `album`, `search`, `artist`|
|data-mode|`circulation`|play mode, `circulation`, `random`, `single`, `order`|
|data-autoplay|`false`|autoplay song(s), not supported by mobile browsers|
|data-mutex|`true`|pause other players when this player playing|
|data-listmaxheight|`340px`|max height of play list|
|data-preload|`auto`|the way to load music, can be `none`, `metadata`, `auto`|
|data-theme|`#ad7a86`|theme color|

more https://aplayer.js.org/docs/#/?id=options

## Advanced

Use self music API, see also https://github.com/metowolf/Meting

```html
<script>
var meting_api='http://example.com/api.php?server=:server&type=:type&id=:id&r=:r';
</script>
<script src="dist/Meting.min.js"></script>
```

## Author

**MetingJS** © [metowolf](https://github.com/metowolf), Released under the [MIT](./LICENSE) License.<br>

> Blog [@meto](https://i-meto.com) · GitHub [@metowolf](https://github.com/metowolf) · Twitter [@metowolf](https://twitter.com/metowolf) · Telegram Channel [@metooooo](https://t.me/metooooo)




---



<p align="center">
<img src="https://ws4.sinaimg.cn/large/006tKfTcgy1fhu01y9uy7j305k04s3yc.jpg" alt="ADPlayer" width="100">
</p>

# APlayer
---

> Wow, such a lovely HTML5 music player

[![npm](https://img.shields.io/npm/v/aplayer.svg?style=flat-square)](https://www.npmjs.com/package/aplayer)
[![npm](https://img.shields.io/npm/l/aplayer.svg?style=flat-square)](https://github.com/MoePlayer/APlayer/blob/master/LICENSE)
[![npm](https://img.shields.io/npm/dt/aplayer.svg?style=flat-square)](https://www.npmjs.com/package/aplayer)
[![size](https://badge-size.herokuapp.com/MoePlayer/APlayer/master/dist/APlayer.min.js?compression=gzip&style=flat-square)](https://github.com/MoePlayer/APlayer/tree/master/dist)
[![Travis](https://img.shields.io/travis/MoePlayer/APlayer.svg?style=flat-square)](https://travis-ci.org/MoePlayer/APlayer)
[![devDependency Status](https://img.shields.io/david/dev/MoePlayer/aplayer.svg?style=flat-square)](https://david-dm.org/MoePlayer/APlayer#info=devDependencies)
[![donate](https://img.shields.io/badge/$-donate-ff69b4.svg?style=flat-square)](https://github.com/MoePlayer/APlayer#donate)

## Introduction

![image](https://i.imgur.com/JDrJXCr.png)

APlayer is a lovely HTML5 music player to help people build audio easily.

**APlayer supports:**

- Media formats
    - MP4 H.264 (AAC or MP3)
    - WAVE PCM
    - Ogg Theora Vorbis
- Features
    - Playlist
    - Lyrics

Using APlayer on your project? [Let me know!](https://github.com/MoePlayer/APlayer/issues/79)

**[Demo](http://aplayer.js.org)**

**[Docs](http://aplayer.js.org/docs)**

## Install

```
$ npm install aplayer --save
```

## Quick Start

```html
<div id="aplayer1" class="aplayer"></div>
<script src="dist/APlayer.min.js"></script>
```

```js
var ap = new APlayer({
    element: document.getElementById('aplayer1'),
    music: {
        title: 'Preparation',
        author: 'Hans Zimmer/Richard Harvey',
        url: 'Preparation.mp3',
    }
});
```

## Usage

[Read the Docs](http://aplayer.js.org/docs)

## CDN

- [jsDelivr](https://www.jsdelivr.com/package/npm/aplayer)
- [cdnjs](https://cdnjs.com/libraries/aplayer)
- [unpkg](https://unpkg.com/aplayer/)

## Join the Discussion

- [Telegram Group](https://t.me/adplayer)
- [QQ Group](https://shang.qq.com/wpa/qunwpa?idkey=bf22213ae0028a82e5adf3f286dfd4f01e0997dc9f1dcd8e831a0a85e799be17): 415835947

## Related Projects

- [APlayer-Typecho-Plugin](https://github.com/zgq354/APlayer-Typecho-Plugin)
- [hexo-tag-aplayer](https://github.com/grzhan/hexo-tag-aplayer)
- [163music-APlayer-you-get-docker](https://github.com/YUX-IO/163music-APlayer-you-get-docker)
- [Hermit-X(APlayer for WordPress)](https://github.com/liwanglin12/Hermit-X)
- [vue-aplayer](https://github.com/SevenOutman/vue-aplayer)
- [APlayer_for_Z-BlogPHP](https://github.com/fghrsh/APlayer_for_Z-BlogPHP)
- [php-aplayer](https://github.com/Daryl-L/php-aplayer)
- [react-aplayer](https://github.com/sabrinaluo/react-aplayer)
- [vue-aplayer](https://github.com/MoeFE/vue-aplayer)
- [APlayer-Controler](https://github.com/Mashiro-Sorata/APlayer-Controler)
- [APlayerHandle](https://github.com/kn007/APlayerHandle)
- [MetingJS](https://github.com/metowolf/MetingJS)
- Feel free to submit yours in [`Let me know!`](https://github.com/MoePlayer/APlayer/issues/79)

## Who use APlayer?

- [站长之家](http://www.chinaz.com/15year/index.html)
- [TheFatRat](http://thefatrat.cn/)
- [Jelly Rue](http://jellyrue.com/)
- [Justice_Eternal吧曲谱资源站](http://lightmoon.pw)
- [Justice_Eternal吧曲谱资源站(移动端)](https://justice-eternal.github.io/)
- [歌词千寻](https://www.lrcgc.com/diy)
- [iSearch](http://i.oppsu.cn)
- [LRC歌词编辑器](https://github.com/MoeFE/Lyric)
- [LLSupport](https://www.lovelivesupport.com/)
- [Аэростатика](https://aerostatica.ru/)
- Feel free to submit yours in [`Let me know!`](https://github.com/MoePlayer/APlayer/issues/79)

## Donate

- [Donate via OpenCollective](https://opencollective.com/aplayer)
- [Donate via Paypal](https://www.paypal.me/DIYgod)
- [Donate via WeChat Pay](https://ws4.sinaimg.cn/large/006tKfTcgy1fhu1uowywej307s07st8h.jpg)
- [Donate via Alipay](https://ws4.sinaimg.cn/large/006tKfTcgy1fhu1vf4ih7j307s07sdfm.jpg)
- Donate via Bitcoin: 13CwQLHzPYm2tewNMSJBeArbbRM5NSmCD1

## Sponsor

Thank you to all our sponsors!

<table>
  <tbody>
    <tr>
      <td align="center" valign="middle">
        <a href="https://console.upyun.com/register/?invite=BkLZ2Xqob" target="_blank">
          <img width="222px" src="https://imgur.com/apG1uKf.png">
        </a>
      </td>
    </tr>
  </tbody>
</table>

## Contributors

This project exists thanks to all the people who contribute.

<a href="https://github.com/MoePlayer/APlayer/graphs/contributors"><img src="https://opencollective.com/APlayer/contributors.svg?width=890" /></a>

## Backers

Thank you to all our backers!

<a href="https://opencollective.com/APlayer#backers" target="_blank"><img src="https://opencollective.com/APlayer/backers.svg?width=890"></a>

## Author

**APlayer** © [DIYgod](https://github.com/DIYgod), Released under the [MIT](./LICENSE) License.<br>
Authored and maintained by DIYgod with help from contributors ([list](https://github.com/DIYgod/APlayer/contributors)).

> [Blog](https://diygod.me) · GitHub [@DIYgod](https://github.com/DIYgod) · Twitter [@DIYgod](https://twitter.com/DIYgod) · Telegram Channel [@awesomeDIYgod](https://t.me/awesomeDIYgod)
