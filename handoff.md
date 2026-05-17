# 个人求职站点 — Handoff 交接文档

## 项目状态：✅ MVP 已完成并上线

- 线上地址：https://my-site-sigma-eosin.vercel.app
- 本地开发：`cd my-site && npm run dev`（端口 3001）
- 部署命令：`cd my-site && npx vercel --yes --prod`

## Spec 完成度

| 模块 | 状态 | 说明 |
|------|------|------|
| 首页 Hero | ✅ | 左图右文，照片 + 定位 + 亮点标签 + 数据亮点 |
| 工作经历 | ✅ | 时间线布局，2 段详细 + 3 段早期经历 |
| 个人作品 | ✅ | 3 卡片，AI 日报工具已填内容，其余占位 |
| 联系方式 | ✅ | 邮箱 + 电话，可点击 |
| 导航 | ✅ | 固定顶部，锚点平滑滚动 |
| 响应式 | ✅ | PC + 移动端适配 |
| 部署 | ✅ | Vercel 静态部署 |

## 文件结构

```
my-site/
├── src/
│   ├── app/
│   │   ├── page.tsx          ← 单页主文件（Hero + 经历 + 作品 + 联系）
│   │   ├── layout.tsx        ← 根布局（字体加载）
│   │   ├── globals.css       ← 全局样式
│   │   ├── experience/page.tsx  ← 独立经历页（保留，可直链访问）
│   │   ├── works/page.tsx       ← 独立作品页
│   │   └── contact/page.tsx     ← 独立联系页
│   ├── components/
│   │   ├── NavBar.tsx        ← 固定顶部导航
│   │   ├── ScrollReveal.tsx  ← 滚动入场动画
│   │   ├── HighlightTag.tsx  ← 可展开的技能标签
│   │   └── EarlierRole.tsx   ← 早期经历卡片
│   └── _versions/            ← 历史版本备份
│       ├── v1.0/             ← 白底 Hello 大字
│       ├── v2.0/             ← 暖米底衬线标题
│       └── v3.0/             ← Luxury/Editorial 金色
├── public/
│   ├── avatar-v9.png         ← 当前使用的照片
│   └── avatar-v2~v8.png      ← 历史照片
└── CLAUDE.md                 ← AI 协作上下文
```

## 技术要点

- **框架**：Next.js 16 (App Router) + TypeScript
- **样式**：Tailwind CSS v4
- **字体**：Playfair Display（标题）、Inter（正文）、Geist Mono（标签）
- **部署**：Vercel，静态生成（SSG）
- **数据**：全部硬编码在 page.tsx 中，无数据库

## 如何继续迭代

### 改视觉 / 排版
直接修改 `src/app/page.tsx` 和 `src/app/globals.css`，改完本地预览满意后运行部署命令。

### 换照片
1. 新照片放入 `public/` 目录，命名 `avatar-vN.png`
2. 在 `page.tsx` 中更新 `src="/avatar-vN.png"`

### 加作品
在 `page.tsx` 的 `works` 数组中追加：
```ts
{
  tag: "PRD",
  title: "作品名称",
  description: "一句话描述",
  link: "https://...",
  ready: true,
}
```

### 回滚版本
历史版本在 `src/_versions/` 中，复制对应文件覆盖当前即可。

## 可继续优化的方向

- [ ] 视觉风格继续微调（字体、颜色、间距）
- [ ] 作品区填入真实内容和 demo 链接
- [ ] 添加 GitHub 链接
- [ ] 移动端进一步优化
- [ ] 暗色模式（spec 中标记为暂不处理）
- [ ] SEO 优化（title、description、OG 标签）
- [ ] 访问统计（Vercel Analytics 或 umami）

## 版本历史

| 版本 | 风格描述 | 备份位置 |
|------|----------|----------|
| v1.0 | 白底 + Hello 超大字 + 右侧照片 | `_versions/v1.0/` |
| v2.0 | 暖米底 + Playfair 衬线标题 + 顶部导航 | `_versions/v2.0/` |
| v3.0 | Luxury/Editorial + 金色点缀 + 纸张纹理 | `_versions/v3.0/` |
| v4.0（当前） | 左图右文分栏 + 滚动动画 + 单页滚动 | 当前线上版本 |
