# HTML 生成规范

生成阶段（SKILL.md 第三步）读这个文件。包含两套模板的 section 结构、class 命名、格式化逻辑。

## 总体结构

每个生成的 `index.html` 长这样：

```html
<!DOCTYPE html>
<html lang="{zh|en}" data-page="{a4|letter}">
<head>
  <meta charset="UTF-8">
  <title>{姓名} - Resume</title>
  <link rel="stylesheet" href="styles/base.css">
  <link rel="stylesheet" href="styles/{single-column|sidebar}.css">
</head>
<body class="template-{single|sidebar}">
  <!-- 模板专属结构 -->
</body>
</html>
```

## CSS 引用规则

- `base.css` 永远引入（共享字体、变量、打印规则）。
- `single-column.css` 或 `sidebar.css` 二选一，根据 `meta.template`。
- 根据用户选择的风格引入对应的 `style-*.css`（如 `style-tech.css`、`style-literary.css` 等）。
- 所有 CSS 文件复制到用户项目的 `styles/` 目录，HTML 用相对路径 `styles/xxx.css` 引用。

### 完整引用示例

```html
<link rel="stylesheet" href="styles/base.css">
<link rel="stylesheet" href="styles/single-column.css">
<link rel="stylesheet" href="styles/style-tech.css">
```

## @page 纸张设置

`base.css` 默认 `@page { size: A4; margin: 1.5cm 2cm; }`。

如果 `meta.page_size: Letter`，在生成的 `index.html` 的 `<style>` 标签里覆盖：

```html
<style>
  @page { size: Letter; margin: 1.5cm 2cm; }
</style>
```

放在 `<link>` 之后，覆盖 base.css 的默认值。

## 日期格式化

YAML 里统一存 `YYYY-MM`（如 `2022-03`）或 `至今`/`Present`。生成 HTML 时格式化：

**中文模板（`meta.language: zh`）：**
- `2022-03` → `2022.03`
- `至今` → `至今`
- 显示：`2022.03 – 至今`

**英文模板（`meta.language: en`）：**
- `2022-03` → `Mar 2022`
- `至今` → `Present`
- 显示：`Mar 2022 – Present`

月份英文缩写：Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec。

## 年龄计算

从 `birthdate: 1995-06` 计算当前年龄：

```
当前年份 - 出生年份 = 基础年龄
如果 当前月份 < 出生月份（或月份相同但日期未到）：基础年龄 - 1
```

生成时算一次写死（静态 HTML，不跑 JS）。HTML 里直接输出「28 岁」或「28」。

## 字段白名单实现

### 中文模板（`meta.language: zh`）

所有 basics 字段都渲染：
- photo → `<img class="photo">`（有值才渲染）
- 国内字段 → `<div class="domestic-fields">` 包裹（单栏）/ 放进侧栏（双栏）
- 联系方式 → 正常渲染

### 英文模板（`meta.language: en`）

**不输出这些节点的 HTML**（不是用 CSS 隐藏，是根本不生成）：
- `<img class="photo">`
- `<div class="domestic-fields">` 整段
- 侧栏里的「基本信息」section（双栏模板）

联系方式、headline、location、summary 正常渲染。

## 模板 A：单栏（template-single）

完整 section 结构：

```html
<body class="template-single">
  <header class="header">
    <div class="header-main">
      <h1 class="name">{姓名}</h1>
      <div class="headline">{headline}</div>
      <div class="contact-row">
        <span class="contact-item">{location}</span>
        <span class="contact-item">{email}</span>
        <span class="contact-item">{phone}</span>
        <span class="contact-item">{github}</span>
      </div>
      <!-- 中文模板才有： -->
      <div class="domestic-fields">
        <span>{年龄} 岁</span>
        <span>{gender}</span>
        <span>{political_status}</span>
        <span>{hometown}</span>
      </div>
    </div>
    <!-- photo 有值且中文模板才有 -->
    <img class="photo" src="{photo}" alt="头像">
  </header>

  <p class="summary">{summary}</p>

  <!-- 各 section，有内容才渲染 -->
  <section class="section">
    <h2 class="section-title">{工作经历|Experience}</h2>
    <div class="entry">
      <div class="entry-header">
        <div>
          <div class="entry-title">{company} · {role}</div>
        </div>
        <div>
          <span class="entry-date">{格式化日期}</span>
          <span class="entry-location">{location}</span>
        </div>
      </div>
      <ul class="highlights">
        <li>{成果1}</li>
        <li>{成果2}</li>
      </ul>
    </div>
  </section>

  <!-- education / projects / skills / awards / certifications / languages -->
</body>
```

### 单栏 skills 渲染

```html
<section class="section">
  <h2 class="section-title">{技能|Skills}</h2>
  <div class="skill-group">
    <span class="skill-category">{category}</span>
    <span class="skill-items">{item1, item2, item3}</span>
  </div>
</section>
```

items 用逗号 + 空格连接成字符串。

### 单栏 education 渲染

```html
<div class="entry">
  <div class="entry-header">
    <div>
      <div class="entry-title">{school} · {degree}</div>
    </div>
    <div>
      <span class="entry-date">{格式化日期}</span>
    </div>
  </div>
  <div class="entry-meta">GPA: {gpa}</div>
</div>
```

## 模板 B：双栏（template-sidebar）

完整 section 结构：

```html
<body class="template-sidebar">
  <!-- 左栏 -->
  <aside class="sidebar">
    <!-- photo 有值才渲染（中文模板） -->
    <img class="photo" src="{photo}" alt="头像">

    <!-- 中文模板才有 -->
    <div class="sidebar-section">
      <div class="sidebar-title">基本信息</div>
      <div class="domestic-fields">
        {年龄} 岁<br>
        {gender}<br>
        {political_status}<br>
        {hometown}
      </div>
    </div>

    <div class="sidebar-section">
      <div class="sidebar-title">{联系方式|Contact}</div>
      <ul class="contact-list">
        <li>{email}</li>
        <li>{phone}</li>
        <li>{github}</li>
        <li>{location}</li>
      </ul>
    </div>

    <div class="sidebar-section">
      <div class="sidebar-title">{技能|Skills}</div>
      <div class="sidebar-skills">
        <span class="sidebar-skill-category">{category1}</span>
        {items1}
        <span class="sidebar-skill-category">{category2}</span>
        {items2}
      </div>
    </div>

    <div class="sidebar-section">
      <div class="sidebar-title">{语言|Languages}</div>
      <div class="sidebar-skills">
        {lang1}<br>
        {lang2}
      </div>
    </div>
  </aside>

  <!-- 右栏 -->
  <main class="main">
    <header class="header">
      <h1 class="name">{姓名}</h1>
      <div class="headline">{headline}</div>
    </header>

    <p class="summary">{summary}</p>

    <section class="section">
      <h2 class="section-title">{工作经历|Experience}</h2>
      <div class="entry">
        <div class="entry-header">
          <div class="entry-title">{company}</div>
          <div class="entry-subtitle">{role}</div>
          <div class="entry-meta">{格式化日期} · {location}</div>
        </div>
        <ul class="highlights">
          <li>{成果}</li>
        </ul>
      </div>
    </section>

    <!-- education / projects / awards / certifications 在右栏 -->
  </main>
</body>
```

### 双栏与单栏的 section 分布差异

- **双栏**：photo、国内字段、联系方式、skills、languages 放**左栏**；experience、education、projects、awards、certifications 放**右栏**。
- **单栏**：所有内容单列流式排列。

### 双栏英文模板

左栏**不输出** photo 和「基本信息」section。其他 section（联系方式、技能、语言）正常。文案切换为 Contact/Skills/Languages。

## section 文案对照

| 中文 | 英文 |
|---|---|
| 工作经历 | Experience |
| 教育背景 | Education |
| 技能 | Skills |
| 项目 | Projects |
| 获奖 | Awards |
| 证书 | Certifications |
| 语言 | Languages |
| 联系方式 | Contact |
| 基本信息 | (英文模板不渲染) |

## 生成检查清单

生成完 `index.html` 后自检：
- [ ] `<html lang>` 和 `data-page` 与 `meta.language` / `meta.page_size` 一致
- [ ] 引用了 `base.css` 和正确的模板 CSS
- [ ] 日期已格式化（不是原始 `2022-03`）
- [ ] 年龄已从 birthdate 计算（不是原始 `1995-06`）
- [ ] 英文模板无 photo / domestic-fields 节点
- [ ] 可选段无内容时不渲染整个 section（不留空标题）
- [ ] highlights 是 `<ul class="highlights"><li>` 真列表
