# task-capture 模板库（v1.1）

本文档提供 `task-capture` 的完整模板：
- Base（通用骨架）
- dev（编程开发插件）
- tool-demo（工具演示插件）
- mixed（混合插件）

使用规则：
- 所有任务都使用：`Base`
- 再按类型追加：`dev` 或 `tool-demo` 或 `mixed`

---

## 1) Base 通用模板（必选）

```markdown
# {YYYY-MM-DD}-{任务名称}

---
type: 沉淀/工具
tags:
  - {核心关键词1}
  - {核心关键词2}
create_date: {YYYY-MM-DD}
status: 待日清
---

## 🎬 演示目标
- 面向对象：{audience}
- 本次要解决：{goal}
- 预期产出：{deliverable}

## ✅ 成功判定（Done）
- [ ] 关键流程完整演示一遍
- [ ] 观众可按步骤复现
- [ ] 核心结果达到预期

## ⏱ 时间预算
- 总时长：{duration} 分钟
- 主流程时长：{main_flow_duration} 分钟
- 预留缓冲：{buffer} 分钟

## 🧭 关键帧计划（录制前）
- 00:00 - 开场：问题与目标
- {t1} - 场景背景/前置说明
- {t2} - 核心步骤开始（⏰关键帧）
- {t3} - 结果验证（⏰关键帧）
- {t4} - 收尾总结

## 📝 实时日志（录制中）
- MM:SS - 动作/讲解
- MM:SS - 关键变化（⏰）
- MM:SS - 异常/偏差
- MM:SS - 修正动作与结果

---

```ad-note
collapse:true
title: 采集提示清单（可选参考）

录制过程中可留意这些关键时刻（记录时间点方便后续定位）：

- [ ] 🔥 痛苦现场：首次报错/卡壳的时间点
- [ ] 🧪 试错过程：失败尝试的时间点和方法
- [ ] 📚 转折点：找到关键文档/灵感的时刻
- [ ] ✅ 最终方案：代码/配置运行成功的时间点

> 提示：记下 MM:SS + 关键词，后续找视频关键帧更快
```

<!-- 复盘内容由 /task-close 触发后追加 -->
```

---

## 2) dev 插件模板（编程开发）

```markdown
## 🧪 环境快照（最小）
- Branch: {branch}
- Version: {version}
- Runtime: {runtime}
- Dependency: {dependency}
- Input Sample: {input_sample}

## 🔁 复现与修复路径
- 复现步骤：
  1. {step1}
  2. {step2}
- 预期错误/现象：{expected_issue}

## 🧠 H/A/O/D 记录（关键节点）
- [H] 假设：{hypothesis}
- [A] 动作：{action}
- [O] 观察：{observation}
- [D] 决策：{decision}

## 🧾 证据原文（建议粘贴）
- 报错日志：
  ```
  {error_log}
  ```
- 关键命令输出：
  ```
  {command_output}
  ```

## ✅ 验证清单
- [ ] 单点验证通过
- [ ] 回归关键路径通过
- [ ] 边界/异常路径已检查
```

---

## 3) tool-demo 插件模板（工具演示）

```markdown
## 🧰 前置条件
- 工具名称/版本：{tool_name} {tool_version}
- 账号与权限：{account_role}
- 初始状态：{initial_state}
- 网络/环境要求：{requirements}

## ▶ 标准演示步骤
1. {step1}
   - 预期：{expected1}
   - 实际：{actual1}
2. {step2}
   - 预期：{expected2}
   - 实际：{actual2}
3. {step3}
   - 预期：{expected3}
   - 实际：{actual3}

## 🛟 失败兜底话术（可选）
- 若失败：{fallback_line}
- 替代路径：{fallback_path}

## ♻ 复位步骤（演示后）
1. {reset1}
2. {reset2}
```

---

## 4) mixed 插件模板（开发 + 工具混合）

```markdown
## 🔀 混合场景说明
- 开发段落时长：{dev_part_time}
- 工具段落时长：{tool_part_time}
- 过渡语：{transition_line}

## ✅ 双重验收
- [ ] 代码逻辑解释清楚
- [ ] 工具操作可复现
```

---

## 5) 自动判定提示词（可嵌入 skill）

```text
请根据任务名称判定模板类型：
- 若偏向代码修复/调试/测试，判定 dev
- 若偏向操作演示/配置讲解，判定 tool-demo
- 若两者均明显存在，判定 mixed
判定后请先询问用户是否确认该类型，用户确认优先。
```