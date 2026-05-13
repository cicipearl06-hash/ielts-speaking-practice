# 雅思口语每日打卡 · 使用指南

## 在线访问

👉 **https://cicipearl06-hash.github.io/ielts-speaking-practice/**

---

## 快速开始

### 1. 注册 / 登录
打开网页后，用**邮箱和密码**注册或登录（随便填邮箱即可，数据会自动创建在云端）

### 2. 配置 API Key（可选）
- 点击右下角 ⚙️
- 填入你的 Claude API Key（用于 AI 评分）
- 保存后所有设备同步

### 3. 开始打卡
登录后每天打开网址即可练习，数据自动云端同步到所有设备

---

## 多设备同步原理

```
你的手机  ──────┐
               ├─── Firebase 云端 ─── 你的电脑
你的平板  ──────┘
```

- 每个设备登录同一个账号
- 打卡记录、得分、进度、话题完成状态全部自动同步
- 数据永久保存在 Google Firebase 云端

---

## 功能一览

| 功能 | 说明 |
|------|------|
| 🎙️ 语音识别 | Web Speech API，实时转文字（Chrome 最佳） |
| ⏱️ 精准计时 | Part 1/3: 20秒 · Part 2: 1分钟准备+2分钟陈述 |
| 📊 AI 评分 | 接 Claude API，从流利度/词汇/语法/连贯性四维评分 |
| 📝 参考答案 | 根据你的回答延伸生成专属参考答案 |
| 📅 打卡日历 | 30天可视化打卡记录 |
| ☁️ 云端同步 | Firebase 实时同步，换设备不丢数据 |
| 📱 左右进度栏 | 显示所有话题完成状态 |

---

## 计时规则（可调整）

| 模块 | 默认时长 |
|------|----------|
| Part 1 | 20 秒/题 |
| Part 2 | 准备 1 分钟 + 陈述 2 分钟 |
| Part 3 | 20 秒/题 |

---

## 浏览器推荐

- **Chrome** — 语音识别完整支持，推荐 ✅
- **Edge** — 完整支持
- **Safari** — 部分支持

---

## 配置 Claude API Key（获取 AI 评分）

1. 访问 https://console.anthropic.com/
2. 创建 API Key（格式：`sk-ant-...`）
3. 打开网页 → ⚙️ → 粘贴 Key → 保存

> 免费额度足够日常练习。不填 Key 也能使用计时和录音功能。

---

## Firebase 安全规则

你的数据受到保护，只有登录同一账号才能访问。

规则文件：`firestore.rules`（已在仓库中）

如需手动设置：
1. 打开 https://console.firebase.google.com/
2. 进入你的项目 → Firestore Database → **规则**
3. 粘贴以下内容：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

---

## 开发说明

- 纯前端单文件应用（index.html）
- Firebase 实时数据库（Firestore）存储用户数据
- Firebase Authentication 管理用户账号
- 无需后端服务器
