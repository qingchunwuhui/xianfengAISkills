# C+I 结构详解 (Context + Insight Structure)

## 核心矛盾

在记录问答时，我们面临两难：

**精简了 → 看不懂**
- "修改配置文件就能解决"
- 两个月后：哪个配置文件？改什么？为什么？

**不精简 → 太啰嗦**
- 把整段对话原封不动粘贴上去
- 想快速查找答案时，被大段文字淹没

## C+I 结构的解决方案

**C+I = Context（上下文）+ Insight（洞察）**

采用**双层结构**：
1. **Insight层**（顶层）：干货结论，快速扫描
2. **Context层**（折叠）：原始对话，还原现场

### 为什么这样设计？

**快速查找时**：只看 Insight 层，一眼看到答案
**需要细节时**：展开 Context 层，看到完整的推理过程和实际案例

## 结构模板

```markdown
### Q: [问题摘要 - 用一句话概括问题]

**📝 核心结论**
[精简后的通用原理，不带具体案例细节]
[这里是"干货"，任何人看到都能理解]

````ad-note
collapse: false
title: 📸 当时的实战场景 (The Context)

[**一级指令：严禁精简**]
[此处必须直接 Copy-Paste 当时的原始对话片段]
[保留所有的代码块、报错原文、配置参数和具体的解释逻辑]
[**禁止**使用"AI解释了XX"、"用户询问了XX"这种第三人称总结]
[要原汁原味的对话流]

````

## 实战案例对比

### ❌ 错误示例（没有 C+I 结构）

```markdown
### Q: 为什么 CORS 报错？

需要在后端添加 CORS 头。
```

**问题**：
- 太精简，没有上下文
- 没有具体的代码示例
- 没有原始的报错信息

---

### ❌ 错误示例（有上下文但格式不对）

```markdown
### Q: 为什么 CORS 报错？

用户询问了为什么会出现 CORS 报错。AI 解释了 CORS 是浏览器的安全机制，
需要在服务器端添加 Access-Control-Allow-Origin 头。用户尝试了添加头，
问题解决了。
```

**问题**：
- 第三人称总结，丢失了原始对话的细节
- 没有具体的报错信息
- 没有具体的代码示例

---

### ✅ 正确示例（完整的 C+I 结构）

```markdown
### Q: React 调用后端 API 时的 CORS 报错如何解决？

**📝 核心结论**
CORS（跨域资源共享）是浏览器的安全机制。当前端（如 localhost:3000）调用不同源的后端 API（如 localhost:5000）时，浏览器会阻止请求，除非服务器响应头中包含 `Access-Control-Allow-Origin`。

解决方案：在后端添加 CORS 中间件，允许跨域请求。

````ad-note
collapse: false
title: 📸 当时的实战场景 (The Context)

**用户**：
我的 React 应用（运行在 localhost:3000）调用后端 API（localhost:5000）时报错：

```
Access to fetch at 'http://localhost:5000/api/users' from origin 'http://localhost:3000'
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on
the requested resource.
```

这是为什么？怎么解决？

**AI**：
这是 CORS（跨域资源共享）问题。浏览器出于安全考虑，默认阻止 JavaScript 从一个源（origin）访问另一个源的资源。

你的前端运行在 `http://localhost:3000`，后端在 `http://localhost:5000`，这是两个不同的源（端口不同），所以浏览器阻止了请求。

解决方案：在后端添加 CORS 头，告诉浏览器"允许这个跨域请求"。

如果你用的是 Express，可以使用 `cors` 中间件：

1. 安装依赖：
```bash
npm install cors
```

2. 在你的 Express app 中添加：
```javascript
const cors = require('cors');
const express = require('express');
const app = express();

// 在所有路由之前添加
app.use(cors());

// 你的其他路由...
app.get('/api/users', (req, res) => {
  // ...
});
```

3. 重启后端服务器

这样浏览器就会允许你的前端访问后端 API 了。

**用户**：
好的，添加了 `app.use(cors())`，重启后端，问题解决了！谢谢！
```
```

**为什么这个例子是正确的？**

1. **核心结论**：
   - 清楚说明了 CORS 是什么
   - 提供了通用的解决方案
   - 任何人看到都能理解

2. **Context 区块**：
   - 保留了完整的报错信息（带堆栈）
   - 保留了原始的对话流（用户问→AI答→用户确认）
   - 保留了具体的代码示例
   - 保留了环境信息（localhost:3000, localhost:5000, Express）

3. **格式正确**：
   - 使用了 ad-note 代码块
   - 标题清楚（📸 当时的实战场景）
   - collapse: false（默认展开）

---

## 填写指南

### Insight 层（核心结论）的写法

**DO（要这样写）**：
- ✅ "CORS 是浏览器安全机制，需要服务器响应头允许跨域"
- ✅ "useEffect 的依赖数组决定何时重新执行，漏掉依赖会导致闭包陷阱"
- ✅ "Promise.all 会并行执行所有 Promise，任何一个 reject 会导致整体 reject"

**DON'T（不要这样写）**：
- ❌ "在 app.js 第15行添加 app.use(cors())"（太具体，应该在 Context 里）
- ❌ "我遇到了一个问题，后来解决了"（太模糊）
- ❌ "参考官方文档"（没有实际内容）

### Context 层（实战场景）的写法

**DO（要这样写）**：
- ✅ 直接粘贴原始对话（用户的问题 + AI的回答）
- ✅ 保留完整的代码块
- ✅ 保留完整的报错信息
- ✅ 保留环境参数（版本号、配置等）

**DON'T（不要这样写）**：
- ❌ "用户询问了 CORS 问题，AI 解释了..."（第三人称总结）
- ❌ 精简掉代码块，只留一句话
- ❌ 精简掉报错信息，只写"报错了"

---

## ad-note 代码块语法

### 基础语法

```markdown
```ad-note
title: 标题
collapse: false

内容
```
```

### 参数说明

- **title**：代码块的标题（必填）
- **collapse**：是否默认折叠
  - `false`：默认展开（推荐，方便查看）
  - `true`：默认折叠（如果 Context 特别长，可以用）

### 为什么用 ad-note？

1. **视觉区分**：让 Context 部分有明显的视觉边界
2. **Obsidian 支持**：在 Obsidian 中会渲染成漂亮的卡片
3. **可折叠**：长内容可以折叠，不干扰阅读

---

## 常见问题

### Q1: 如果对话很长，Context 会不会太啰嗦？

**答**：
- 如果对话确实很长（比如超过200行），可以设置 `collapse: true`，默认折叠
- 但**不要精简内容**，完整性 > 简洁性
- 记住：两个月后你会感谢现在的自己没有删掉细节

### Q2: 核心结论应该多长？

**答**：
- 通常 1-3 句话
- 如果需要解释原理，可以写成 3-5 句话
- 关键是：**任何人看到都能理解，不依赖具体案例**

### Q3: 如果问题有多个解决方案怎么办？

**答**：
- Insight 层：列出所有方案的对比
- Context 层：保留完整的讨论过程

示例：
```markdown
**📝 核心结论**
处理异步错误有3种方式：
1. try-catch（同步风格）
2. .catch()（Promise链）
3. Promise.allSettled()（批量处理）

选择标准：单个异步用 try-catch，多个异步用 allSettled。

````ad-note
title: 📸 当时的实战场景
[保留完整的对话，包括为什么选了方案1而不是方案2]
````
````

---

## 总结

C+I 结构的本质是：**干货在前，现场在后**。

- **Insight**：给未来的你一个快速答案
- **Context**：给未来的你完整的推理过程

两者缺一不可：
- 只有 Insight → 看不懂为什么
- 只有 Context → 找不到答案在哪

结合使用 → **既快速又完整** ✅
