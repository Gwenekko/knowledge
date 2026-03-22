# 上传到 GitHub 的文件清单（约 17 个）

**⚠️ 不要上传 `node_modules` 和 `dist` 文件夹！** Vercel 会自动安装依赖并构建。

## 必须上传的文件

```
kato-knowledge/
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
├── README.md（可选）
├── public/
│   ├── favicon.svg
│   └── kato.png
└── src/
    ├── main.js
    ├── App.vue
    ├── style.css
    └── components/
        ├── ChatArea.vue
        ├── KatoMascot.vue
        ├── KnowledgeBase.vue
        ├── KnowledgeDetail.vue
        └── Onboarding.vue
```

**总计约 17 个文件**，远低于 100 个限制。

## 推荐方式：用 Git 命令行上传

使用 Git 时，`.gitignore` 会自动排除 `node_modules` 和 `dist`，无需手动选择：

```bash
cd C:\Users\lily_\Desktop\temp\kato-knowledge
git init
git add .
git status   # 确认没有 node_modules 和 dist
git commit -m "Initial commit"
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

## 如果用网页拖拽上传

只选择并拖入上述列出的文件和文件夹，**不要**拖入 `node_modules` 和 `dist`。
