# resume.yaml 完整 Schema

本文档在用户首次建立 `resume.yaml`、或字段填错、或需要确认字段含义时读取。

## meta 段（必填）

控制全局行为。

| 字段 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `language` | `zh` \| `en` | 是 | 切换模板文案、纸张默认值、姓名选用。`zh` → 中文文案 + A4；`en` → 英文文案 + Letter（可被 `page_size` 覆盖）。 |
| `template` | `single` \| `sidebar` | 是 | 视觉模板。`single` 单栏极简；`sidebar` 双栏侧边栏。 |
| `style` | `tech` \| `creative` \| `business` \| `finance` \| `academic` \| `literary` \| `custom` | 是 | 简历风格。选择预设风格或自定义。 |
| `page_size` | `A4` \| `Letter` | 是 | 纸张大小。中文场景用 A4，美国用 Letter。 |
| `name_zh` | string | 否* | 中文姓名。`language: zh` 时必填。 |
| `name_en` | string | 否* | 英文姓名。`language: en` 时必填。 |

*`name_zh` 和 `name_en` 至少填一个，对应 `language` 的那个必填。

## basics 段（必填）

个人基础信息。

### 联系与定位（三处产出都显示）

| 字段 | 类型 | 必填 | 说明 |
|---|---|---|---|
| `headline` | string | 是 | 一句话职业定位，姓名下方显示。如「高级前端工程师」。 |
| `location` | string | 否 | 所在地，如「上海」「Shanghai」。 |
| `email` | string | 否* | 邮箱。 |
| `phone` | string | 否* | 电话。**必须加引号**，否则 YAML 把 `+` 当符号：`"+86 138-0000-0000"`。 |
| `website` | string | 否 | 个人网站。 |
| `github` | string | 否 | GitHub 主页，写 `github.com/username` 即可。 |
| `linkedin` | string | 否 | LinkedIn 主页。 |

*email/phone/website/github/linkedin 至少填一个。

### 国内特色字段（仅中文 HTML 模板显示）

这些字段在**英文 HTML 模板隐藏**、在**docx 始终剥离**（见 SKILL.md 字段白名单表）。

| 字段 | 类型 | 说明 |
|---|---|---|
| `photo` | string (路径) | 头像图片路径，相对 `resume.yaml`。单栏模板显示右上 60px 圆头像，双栏显示左栏 120px 圆头像。不要就删掉这行。 |
| `birthdate` | string `YYYY-MM` | 出生年月。**渲染器自动算年龄**，不要直接写年龄数字（会过期）。如 `1995-06`。 |
| `gender` | string | 性别，如「男」「女」。 |
| `political_status` | string | 政治面貌，如「中共党员」「群众」。国企/体制内常用。 |
| `hometown` | string | 籍贯，如「浙江杭州」。 |
| `marital_status` | string | 婚姻状况。部分岗位会问。 |

### 个人简介

| 字段 | 类型 | 说明 |
|---|---|---|
| `summary` | string (多行) | 2-4 句个人简介。用 YAML 的 `\|` 保留换行。 |

## experience 段（必填，数组）

工作经历，**最新的排在最前面**（倒序）。

每条结构：

```yaml
- company: 字节跳动          # 必填，公司名
  role: 高级前端工程师        # 必填，职位
  start: 2022-03            # 必填，YYYY-MM 格式
  end: 至今                 # 必填，"至今" | "Present" | YYYY-MM
  location: 上海            # 可选
  highlights:               # 必填，成果列表
    - 第一条成果
    - 第二条成果
```

**highlights 写法原则**：每条一个可量化的成就，不是职责描述。
- ✅ 好：「主导性能优化，首屏从 3.2s 降至 1.1s」
- ❌ 差：「负责前端开发工作」

## education 段（必填，数组）

```yaml
- school: 上海交通大学        # 必填
  degree: 计算机科学与技术 学士  # 必填
  start: 2014-09           # 必填
  end: 2018-06             # 必填
  gpa: 3.7/4.0            # 可选
  highlights: []          # 可选
```

## skills 段（必填，数组）

技能分组。

```yaml
- category: 前端
  items: [React, TypeScript, Vue, Webpack]
- category: 后端
  items: [Node.js, Python, PostgreSQL]
```

单栏模板：每组一行，分类名加粗。
双栏模板：放在左栏。
docx：用逗号分隔的纯文本，不用进度条/星级。

## 可选段

没有就留空数组 `[]`，**不要用注释掉**（`# awards:`）。渲染器看到空数组自动跳过。

### projects（项目/作品）

```yaml
projects:
  - name: 开源项目 XXX
    url: github.com/xxx        # 可选
    description: 一句话说明
    highlights:
      - GitHub 2.3k stars
```

### awards（获奖）

```yaml
awards:
  - title: 第一名
    issuer: 某比赛
    date: 2020-05            # 可选
```

### certifications（证书）

```yaml
certifications:
  - name: AWS Solutions Architect
    issuer: Amazon
    date: 2021-08
```

### languages（语言能力）

```yaml
languages:
  - 英语（流利）
  - 日语（N3）
```

简单字符串数组即可，每项一段。

## 常见错误

1. **phone 不加引号** → YAML 解析 `+86` 报错。修：`"+86 138-0000-0000"`。
2. **age 写数字** → 会过期。改用 `birthdate: YYYY-MM`。
3. **日期格式不统一** → 必须用 `YYYY-MM`（如 `2022-03`），渲染器负责显示格式化。
4. **可选段注释掉** → 用 `awards: []` 而不是 `# awards:`。
5. **highlights 写职责** → 改写成可量化成果。
6. **experience 顺序反了** → 最新的经历放数组第一个。
