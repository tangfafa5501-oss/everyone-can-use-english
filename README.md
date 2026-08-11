<div align="center">
  <img src="./enjoy/assets/icon.png" alt="Clash" width="128" />
</div>

<h3 align="center">
AI 是当今世界上最好的外语老师，Enjoy 做 AI 最好的助教。
</h3>

[![Deploy 1000h website](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/deploy-1000h.yml/badge.svg)](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/deploy-1000h.yml)
[![Test Enjoy App](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/test-enjoy-app.yml/badge.svg)](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/test-enjoy-app.yml)
[![Release Enjoy App](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/release-enjoy-app.yml/badge.svg)](https://github.com/ZuodaoTech/everyone-can-use-english/actions/workflows/release-enjoy-app.yml)
![Latest Version](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fenjoy.bot%2Fapi%2Fconfig%2Fapp_version&query=%24.version&label=Latest&link=https%3A%2F%2F1000h.org%2Fenjoy-app%2Finstall.html)
![Recording Duration](https://img.shields.io/endpoint?url=https%3A%2F%2Fenjoy.bot%2Fapi%2Fbadges%2Frecordings)

---

## 网页版

Enjoy 全新版本已经上线，可访问 [https://enjoy.bot](https://enjoy.bot) 直接使用。

![](./enjoy/snapshots/screenshot-video.png)
![](./enjoy/snapshots/screenshot-ebook.png)
![](./enjoy/snapshots/screenshot-flashcard.png)
![](./enjoy/snapshots/screenshot-course.png)

## 浏览器插件

Enjoy 浏览器插件已经上线，支持 YouTube 和 Netflix。可访问 [Chrome Web Store](https://chromewebstore.google.com/detail/enjoy-echo/hiijpdndbjfnffibdhajdanjekbnalob) 安装使用。

![](./enjoy/snapshots/screenshot-youtube.png)
![](./enjoy/snapshots/screenshot-netflix.png)

---

## 桌面版

新版桌面版将会是对网页版的套壳和增强，即将发布。

## 开发与维护

本仓库是一个 Yarn monorepo，包含 Enjoy 桌面端、1000 小时内容站、门户页和 Cloudflare Worker 入口。

- [开发环境与启动说明](./DEVELOPMENT.md)
- [项目架构](./ARCHITECTURE.md)
- [参与贡献](./CONTRIBUTING.md)
- [Enjoy 桌面端说明](./enjoy/README.md)

> 注意：Enjoy 的云端 API、WebSocket 服务和网页版源码不在本仓库中。本仓库可以独立开发桌面端的本地能力和两个静态站点；完整联调云端账号、同步、社区及托管 AI 服务时，需要可用的 Enjoy 后端。


## 相关阅读

### 一千小时（2024）

- [简要说明](https://1000h.org/intro.html)
- [训练任务](https://1000h.org/training-tasks/kick-off.html)
- [语音塑造](https://1000h.org/sounds-of-american-english/0-intro.html)
- [大脑内部](https://1000h.org/in-the-brain/01-inifinite.html)
- [自我训练](https://1000h.org/self-training/00-intro.html)

### 人人都能用英语（2010）

- [简介](./book/README.md)
- [第一章：起点](./book/chapter1.md)
- [第二章：口语](./book/chapter2.md)
- [第三章：语音](./book/chapter3.md)
- [第四章：朗读](./book/chapter4.md)
- [第五章：词典](./book/chapter5.md)
- [第六章：语法](./book/chapter6.md)
- [第七章：精读](./book/chapter7.md)
- [第八章：叮嘱](./book/chapter8.md)
- [后记](./book/end.md)

## 常见问题

请查询 [文档 FAQ](https://1000h.org/enjoy-app/faq.html)。
