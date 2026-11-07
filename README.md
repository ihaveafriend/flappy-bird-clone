# Flappy Bird 复刻版

完整复刻经典 Flappy Bird 玩法的单文件 HTML5 游戏。

## 功能

- **原版玩法**：点击/空格/触摸让小鸟飞行，穿过管道。
- **排行榜**：
  - 历史总榜
  - 今日榜
  - 数据存储在浏览器 `localStorage`（本地演示）
- **登录**：
  - 支持微信、抖音、Google、X 四种方式（当前为演示模拟）
  - **推荐真实实现**：使用开源库 [JustAuth](https://github.com/justauth/JustAuth)
    - 支持微信、抖音、Google、Twitter/X 等 30+ 平台
    - Java 后端，API 极简
    - 官方文档：https://www.justauth.cn
- **分享**：
  - 一键分享到 X (Twitter)
  - 系统原生分享（Web Share API）
  - 复制链接（方便微信/抖音分享）

## 如何运行

直接用浏览器打开 `flappy-bird.html` 即可。

## 真实登录集成建议

1. 后端使用 JustAuth 生成授权 URL
2. 前端点击登录按钮后跳转到对应平台授权
3. 回调后获取用户信息，存入 session
4. 排行榜建议对接后端数据库（如 Redis / MySQL）实现全局榜单

## 参考开源项目

- 登录：[JustAuth](https://github.com/justauth/JustAuth)
- 分享按钮风格参考：[shareon](https://github.com/kytta/shareon)
- 游戏逻辑参考多个开源 Flappy Bird Canvas 实现

## 说明

当前版本为纯前端演示，所有数据均保存在本地。如需上线真实排行榜和登录，请配合后端服务使用。
