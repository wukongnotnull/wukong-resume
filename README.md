<div align="center">

# 📄 悟空简历.SKILL

<br>

> **帮助毕业生或求职者生成专业简历，顺利找到满意工作的 智能体 技能**

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-orange.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![Skills](https://img.shields.io/badge/skills.sh-Compatible-green)](https://skills.sh)

<br>

**还在为简历发愁？** <br>
**设计不好看、格式不规范、内容不专业？** <br>
**这里有你需要的全部解决方案。**

<br>

不只是模板，更是 **专业的简历构建系统** —— <br>
同一份内容，同时生成给人看的精美 PDF 和给 ATS 看的优化文档。

---

**快捷导航**

[功能特点](#功能特点) | [快速开始](#快速上手) | [安装](#安装) | [风格选择指南](#风格选择指南) | [依赖说明](#依赖说明) | [使用技巧](#使用技巧) | [安全声明](#安全声明) | [设计理念](#设计理念) | [关于我](#关于我)

<br>

</div>

---

## 功能特点

| 特性 | 说明 |
|------|------|
| 🎨 **6种预设风格** | tech、creative、business、finance、academic、literary |
| 🇨🇳 **中英文双语** | 自动切换语言、纸张、文案 |
| 📱 **2种模板** | 单栏简约版、双栏侧边栏版 |
| 📄 **双输出格式** | HTML（打印PDF）+ Word（ATS友好） |
| 🛡️ **安全设计** | 身份证号绝对不存储 |

---

## 快速上手

在 智能体 中说：

```
用户      ❯ 帮我做份简历
用户      ❯ 帮我更新简历
用户      ❯ 我要做一份前端工程师简历
```

AI 会引导你完成：

1. 选择语言（中文/英文）
2. 选择模板（单栏/双栏）
3. 选择风格（6种预设或自定义）
4. 提供个人信息

最后获取结果：
- HTML 格式（可直接打印 PDF）
- Word 格式（国内求职常用）

## 安装

### 方式一：技术人员(命令行)

直接用 npx 安装：

```bash
npx skills add wukongnotnull/wukong-resume
```

### 方式二：文科生（对话式）
```txt
帮我安装该 Skill：https://github.com/wukongnotnull/wukong-resume

```


---

## 风格选择指南

| 风格 | 适用岗位 | 特点 |
|------|---------|------|
| **tech** | 程序员、工程师、数据分析师 | 蓝色系，现代科技感 |
| **creative** | UI/UX设计师、创意总监 | 紫色系，大胆创意 |
| **business** | 项目经理、企业高管 | 深蓝黑，专业稳重 |
| **finance** | 金融分析师、咨询顾问 | 绿金色，高端精致 |
| **academic** | 研究员、教师、教授 | 深灰色，简洁严谨 |
| **literary** | 作家、编辑、记者、文案 | 米黄棕，书卷气 |

---

## 依赖说明

- **PDF 输出**：零依赖，任何现代浏览器（Chrome/Safari/Edge/Firefox）
- **Word 输出**：需要 pandoc
  - macOS：`brew install pandoc`
  - Windows：下载 https://pandoc.org/installing.html
  - Linux：`sudo apt install pandoc`

---

## 使用技巧

### 打印 PDF 的最佳实践

1. 在浏览器中打开 HTML 文件
2. 按 `Cmd/Ctrl + P` 打开打印对话框
3. 选择「打印背景图形」
4. 取消勾选「页眉和页脚」
5. 纸张选择 A4（中文）或 Letter（英文）
6. 选择「保存为 PDF」

### 简历更新流程

```
用户      ❯ 把电话改成 xxx
用户      ❯ 加一条最近的工作经历
用户      ❯ 换用 literary 风格
用户      ❯ 生成英文版本
```

---

## 安全声明

| 保障 | 说明 |
|------|------|
| **绝不存储身份证号** | 如果用户提供，会明确拒绝并解释原因 |
| **隐私保护** | 所有数据本地处理，不上传 |
| **可选择性** | 照片、国内字段等都是可选的 |

---

## 设计理念

通过「结构化 YAML 数据源 + 双渲染器」工作流，把同一份简历内容生成两份各自最优的产出：

- **给人看的漂亮 PDF**：HTML + CSS，浏览器打印，零依赖。
- **给 ATS 投递的朴素 docx**：pandoc 生成，ATS 友好。

支持中英双语切换、单栏极简 / 双栏侧边栏两套模板。

---


## 关于我

**悟空非空也** — AI之道创始人，独立开发者，Up主。

| 平台 | 链接 |
|------|------|
| 🌐 官网 | [AI之道官网](https://waytoai.cn) |
| 𝕏 Twitter | [悟空非空也](https://x.com/wukongnotnull) |
| 📺 B站 | [悟空非空也](https://space.bilibili.com/456634391) |
| ▶️ YouTube | [悟空非空也](https://www.youtube.com/@wukongnotnull) |
| 📕 小红书 | [悟空非空也](https://www.xiaohongshu.com/user/profile/5ca89c2f000000001100952b) |
| 💬 公众号 | 微信搜「悟空非空也」 |




---

<div align="center">

Apache-2.0 license © [悟空非空也](https://github.com/wukongnotnull)

</div>
