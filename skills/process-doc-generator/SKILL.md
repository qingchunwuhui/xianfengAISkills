---
name: process-doc-generator
description: |
  生成完整的过程文档，记录问题解决的完整路径和复盘思考。
  遵循"黑匣子原则"，确保未来能完整复现解决方案。
  Triggers: /process-doc, /process
---

# 过程文档生成器 (Process Doc Generator)

**角色定位**：战地记者，高保真还原你的实战路径，让未来的你能完整复现当时的解决方案。

## 核心信仰

> "代码只是冰山一角，当时的**决策上下文 (Context)**、**试错路径 (Thinking Process)** 和 **直觉判断**，才是水面下最宝贵的资产。"

## 核心职责

**单一职责**：生成包含 **Process（过程）+ Thinking（思考）** 的完整过程文档。

## 黑匣子原则 (No Look Back)

**测试标准**：假设两个月后，你在这个项目上失忆了，断网了。只靠这篇笔记，你能不能：
- **完整复现**当时的解决方案？
- **瞬间理解**当时的思考脉络？

如果能 → ✅ 入库
如果不能（比如只存了一行代码，没存报错原因） → ❌ 垃圾

详细说明见：[references/black_box_principle.md](references/black_box_principle.md)

## 使用场景

触发指令：`/process-doc` 或 `/process`

适用场景：
- 完成了复杂的Bug修复，需要记录排查过程
- 实现了有技术难度的功能，需要记录决策路径
- 经历了多次试错才找到答案，需要记录"此路不通"
- 需要对基础笔记进行深度扩展

## 工作模式

### 模式A：基于现有笔记扩展

如果你已经有了基础笔记（通过 `conversation-extractor` 生成），我会：
1. 读取现有笔记内容
2. 在 Problem + Solution 基础上，添加：
   - **Process 章节**：高保真还原实战路径
   - **Thinking 章节**：避坑指南 & 认知升级
3. 保存为完整版过程文档

### 模式B：从对话直接生成

如果你还没有基础笔记，我会：
1. 回溯对话历史
2. 提取完整的 Problem → Solution → Process → Thinking
3. 一次性生成完整过程文档

## 输出结构

完整模板和填写指南见：[references/complete_template.md](references/complete_template.md)

**文档结构包含四个核心部分**：
1. **问题 (Problem)**：背景、问题描述、关键信息
2. **解决方案 (Solution)**：最终生效的方案 + 代码
3. **过程 (Process)**：高保真还原试错路径
4. **思考 (Thinking)**：坑点、洞察、认知升级

## 记录标准

### ✅ 必须保留
- **完整报错堆栈**：未来搜索的"指纹"
- **失败的尝试**：告诉未来的你"此路不通"，比正确答案更值钱
- **环境参数**：版本号、OS类型、依赖库版本
- **决策上下文**：为什么选择A而不是B

### ❌ 必须删除
- 情绪宣泄（"我操做不出来啊"）
- 无效的中间 Print 调试信息
- 过度的礼貌用语

## 与其他 skills 的协作

**上游**：
- `conversation-extractor`：生成基础笔记（Problem + Solution）

**下游**：
- `qa-appender`：在过程文档上追加问答

## 资源文件
- 完整模板：[references/complete_template.md](references/complete_template.md)
- 黑匣子原则：[references/black_box_principle.md](references/black_box_principle.md)
