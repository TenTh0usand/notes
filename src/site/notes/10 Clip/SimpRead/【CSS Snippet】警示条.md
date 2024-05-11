---
{"dg-publish":true,"permalink":"/10-clip/simp-read/css-snippet/","title":"[转载]【CSS Snippet】警示条","tags":["simpread","clipping"]}
---



- 🗒️**File Info**
- 📋转载日期: 2024-05-07 21:09:10
- 🔗原文链接: [untitled](https://zji.me/c13f85d3-4edc-401d-9e46-804c8750f1b3.html)
- 📑原文标题: untitled
- 🤵作者: zji.me
- 🏡源站: zji.me
- 📃简介: 


>本文由 [10k](https://tenthousand.cn) 使用 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址: [untitled](https://zji.me/c13f85d3-4edc-401d-9e46-804c8750f1b3.html)
# 【CSS Snippet】警示条

工事中 - 立入禁止

将如下代码保存到 `.obsidian/snippets/WarningStrip.css` 文件中（自行创建文件），然后在 Obsidian 设置——外观——代码片段中开启。即可使用 `warning-strip` 类型 callouts 创建这种警示条效果了。

```
/**
 * 警告条
 * @author: 稻米鼠
 * @description: 用于显示警告条的 callout 视图
 * @created: 2022-11-23 20:35:16
 * @updated: 2024-05-05
 * @version: 0.0.1
 */
.callout[data-callout="warning-strip"] {
  --stop-yellow: #feab38;
  --stop-black: #333338;
  --stop-width: 36px;
  --stop-border-width: 2px;
  --stop-paper-rotate: 3deg;
  position: relative;
  background: none;
  padding: 10px;
}
.callout[data-callout="warning-strip"]::before,
.callout[data-callout="warning-strip"]::after {
  position: absolute;
  top: 0;
  content: " ";
  width: var(--stop-width);
  height: 100%;
  box-sizing: border-box;
  border: var(--stop-border-width) solid var(--stop-black);
  border-radius: 3px;
}
.callout[data-callout="warning-strip"]::before {
  left: 0;
  border-right: 0;
}
.callout[data-callout="warning-strip"]::after {
  right: 0;
  border-left: 0;
}
.callout[data-callout="warning-strip"] > .callout-title {
  display: flex;
  background: repeating-linear-gradient(-45deg, var(--stop-yellow), var(--stop-yellow) 15px, var(--stop-black) 15px, var(--stop-black) 30px);
  justify-content: center;
  border-radius: 3px;
}
.callout[data-callout="warning-strip"] > .callout-title > .callout-icon {
  display: none;
}
.callout[data-callout="warning-strip"] > .callout-title > .callout-title-inner {
  background: #F3F3E6;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, .1), 0 0 3px rgba(0, 0, 0, .3);
  text-align: center;
  line-height: 1em;
  padding: 5px;
  transform: rotate(var(--stop-paper-rotate));
  color: var(--stop-black);
  stroke: var(--stop-black);
}

```

甚至还可以附带内容：

【NoEntry】内有恶犬

Meow~(这么可爱什么的，才不给你萌看呢！