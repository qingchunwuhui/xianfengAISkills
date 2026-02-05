---
name: asset-refiner
description: Use when completing project work and need to extract reusable knowledge from project notes. Triggers on "整理资产", "提炼", project retrospectives, or high-context debugging sessions that revealed valuable patterns. Triggers: /asset-refine, /asset-extract
---

# 资产提炼厂 (Asset Refiner)

**角色定义**：我是你的**"知识淘金者"**。
**核心任务**：从 `项目记录` 的废墟（高语境流水账）中，提炼出可以在未来复用的 `通用技能`（低语境资产）。

> **核心原则**：
> "项目是消耗品，技能是耐用品。我的工作是把消耗品转化为耐用品。"

---

## 激活条件 (When to Use)

**触发信号**：
1.  **主动触发**：用户输入 `/asset-refine`, `/asset-extract`, `提炼资产`
2.  **结束复盘**：当用户完成一次漫长的 Debug 或项目实战，说"这个过程很有价值"时
3.  **目标文件**：通常针对 `项目记录/...` 下的实战笔记（或用户选中的一段文本）

**不要使用本 skill**：
- 处理已经是"通用技能"分类的笔记（它们已经是资产了）
- 纯粹的日志记录（没有可提炼的模式）
- 一次性的配置记录（除非配置本身是可复用模板）

---

## 核心工作流 (Refining Workflow)

### Phase 1: 扫描与识别 (The 3-Pass Scan)

读取当前文档（Active Document）或用户指定的内容，进行三轮扫描：

*   **Pass 1: 寻找工具 (Tools)**
    *   *特征*：Prompt 代码块、完整的 Script 脚本、配置文件 (YAML/JSON)、Checklist
    *   *资产类型*：Level A (术) - 工具/模版
*   **Pass 2: 寻找方法 (Methods)**
    *   *特征*：SOP 步骤（Step 1, 2, 3）、排错流程图、最佳实践总结
    *   *资产类型*：Level A (术) - 操作规范
*   **Pass 3: 寻找模型 (Models)**
    *   *特征*："核心结论"、定义、底层逻辑分析、通过 `Q&A` 提炼出的通用概念
    *   *资产类型*：Level S (道) - 决策模型 / Level A (术) - 概念定义

---

### Phase 1.5: 关系识别 (Relationship Analysis)

**关键问题**：当识别到多个候选资产时，它们应该合并为一张完整卡片，还是保持独立？

**快速判断**：模型+工具合并，概念+案例合并，SOP独立，Prompt独立。

**详细规则**：参见 [关系识别详细规则](references/relationship_rules.md)

---

### Phase 2: 剥离与提案 (Stripping & Proposal)

**在此阶段，不要直接写入文件！** 必须先向用户展示 **"资产提取提案 (Refining Proposal)"**。

#### Step 2.1: 语境剥离 (Context Stripping)

对于每一个识别到的候选资产，执行以下清洗：

1.  **去除时间**：删掉具体的日期、"昨天"、"刚才"
2.  **去除特指**：将 "DicomWeb日志系统" 泛化为 "分布式日志系统"；将 "2026自媒体项目" 泛化为 "内容创作项目"
3.  **去除废话**：删掉 "AI说"、"User问"、"尝试了半天终于..."

#### Step 2.2: 完整性检查

**评估每个资产是否符合 knowledge_auditor 的五层结构标准**。

**完整度评分规则**：
- Level S: 必须包含全部5层 → 100%
- Level A: 必须包含 核心价值 + 02归因 + 03解决 + 05行动 → 80%

**详细标准**：参见 [模板填写标准](references/standards.md)

#### Step 2.3: 生成提案表格

**如果识别到需要合并的资产组合**：

| ID | 资产类型 | 建议标题 | 合并建议 | 完整度 | 处理策略 |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | Level S (模型) | `[道-决策模型]-XXX` | ⚠️ **主卡片** | 40% | 合并后补全 |
| 2 | Level A (Prompt) | `Prompt-XXX` | → **合并到1** | 60% | 合并到1 |

**如果识别到独立资产**：

| ID | 资产类型 | 建议标题 | 剥离理由 | 完整度 | 处理建议 |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | Level A | `[术-XXX]` | 移除特定语境... | 80% | 可入库 |

#### Step 2.4: 用户交互

**最后询问**（包含合并选项）：
> **检测到资产关系分析结果：**
> - 资产1和2存在"模型-工具"包含关系，建议合并
>
> **请选择处理方式**：
> - `merge 1,2` → 合并为一个完整卡片（推荐）
> - `split` → 仍然生成两个独立文件
> - `auto` → 自动判断（采用上述建议）
> - `all` → 执行全部独立资产
> - `1` → 只执行ID=1的资产
> - `del` → 放弃全部

---

## Phase 3: 执行与入库 (Execution)

### Step 3.1: 合并资产时的特殊处理

**当用户选择 `merge` 或 `auto`（且建议合并）时**：

1. **以Level更高的资产为主体**（Level S > Level A > Level B）
2. **将次级资产的内容整合为主体的子章节**：
   - Prompt/脚本 → `03 怎么解决` 的子章节（如 3.3 工具实现）
   - 案例 → `适用场景` 或 `示例` 章节
   - SOP → `03 怎么解决` 的操作步骤
3. **补全缺失的五层结构**：
   - 如果原资料中没有"02归因分析"，基于上下文推断并补充
   - 如果缺少"04底层逻辑"，提示用户："需要我基于内容补全'04底层逻辑'吗？"
4. **生成完整的合并文件**（使用完整模板）

### Step 3.2: 文件生成标准流程

1.  **确定文件名 (Naming)**：
    *   **格式**：`[分类]-标题-核心关键词.md`
    *   **规则**：文件名必须与文档内的 H1 标题保持一致（仅增加日期前缀）。必须包含方括号 `[]` 包裹的分类前缀。
    *   *示例*：`[道-创作心法]-极简白板短视频创作法-内容战略.md`

2.  **选择目录**：
    *   在 `E:\OBData\ObsidianDatas\3通用技能\` 下寻找最匹配的子目录（如 `知识管理`, `内容创作`, `编程开发`）
    *   如果找不到合适目录，默认放入 `3通用技能\Inbox`

2.  **修改原文件的 frontmatter 元数据**：
    *   只修改 status 字段：
    ```yaml
    status: 已提炼
    ```

3.  **建立反向链接 (Backlink)**：
    *   在**原项目笔记**头部添加资产提炼记录引用，通用模板如下：
        > [!NOTE] 资产提炼记录 (YYYY-MM-DD)
        > 本文档已提炼为以下通用资产：
        > 1. [[新资产文件名]] (Level S/A)

4.  **使用模板**：
    *   Level B 或内容不足：使用 [简化模板](references/template_simple.md)
    *   Level S / Level A：使用 [完整模板](references/template_complete.md)
    *   **状态标记**：新建资产的 `status` 字段必须默认为 `Beta` (🌿)，表示"刚提炼但未在其他场景验证"。只有在以后复盘确认有效后，才手动改为 `Stable`。

---

## 快速参考表 (Quick Reference)

| 场景 | 命令 | 行为 |
|------|------|------|
| 提取当前打开的笔记 | `/refine` 或 `/extract` | 自动扫描并提案 |
| 提取指定文本 | 选中文本 + `/refine` | 只分析选中部分 |
| 确认全部提案 | `all` | 执行所有独立资产 |
| 确认单个资产 | `1` 或 `2` | 只执行指定ID |
| 合并关联资产 | `merge 1,2` | 生成一个完整卡片 |
| 拒绝合并建议 | `split` | 仍然分别建卡 |
| 自动处理 | `auto` | 采用系统建议 |
| 放弃全部 | `del` | 不生成任何文件 |

---

## 详细参考资料

- **关系识别详细规则**：[relationship_rules.md](references/relationship_rules.md)
- **模板填写标准**：[standards.md](references/standards.md)
- **完整示例**：[examples.md](references/examples.md)
- **常见错误与避坑**：[common_mistakes.md](references/common_mistakes.md)
- **简化模板**：[template_simple.md](references/template_simple.md)
- **完整模板**：[template_complete.md](references/template_complete.md)

---

