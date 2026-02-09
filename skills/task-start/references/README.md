# Task-Start References

本目录包含 task-start skill 的详细参考资料，采用**渐进式披露**设计原则。

## 目录结构

```
references/
├── templates/           # 任务模板（按需加载）
│   ├── tech-bug-fix.md         # Bug修复模板
│   ├── tech-feature-dev.md     # 新功能开发模板
│   ├── tech-deploy.md          # 配置部署模板
│   ├── tech-performance.md     # 性能优化模板
│   ├── tech-research.md        # 需求调研模板
│   └── content-creation.md     # 内容创作模板
│
├── examples/           # 完整示例（参考学习）
│   └── content-creation-example.md  # 内容创作完整示例
│
└── task_template.md.backup    # 旧版模板备份
```

## 使用方式

### 对于用户
直接使用 `/task-start` 触发技能即可，系统会：
1. 询问任务类型
2. 自动加载对应的模板
3. 生成定制化的执行文档

### 对于 AI
根据用户选择的任务类型，读取对应的模板文件：

```
用户选择 "Bug修复" → Read("references/templates/tech-bug-fix.md")
用户选择 "新功能开发" → Read("references/templates/tech-feature-dev.md")
用户选择 "配置部署" → Read("references/templates/tech-deploy.md")
用户选择 "性能优化" → Read("references/templates/tech-performance.md")
用户选择 "需求调研" → Read("references/templates/tech-research.md")
用户选择 "内容创作" → Read("references/templates/content-creation.md")
```

## Token 效率

采用渐进式披露后的 Token 使用对比：

| 场景 | 旧版（一次性加载全部） | 新版（按需加载） | 节省 |
|------|----------------------|----------------|------|
| Bug修复 | 25KB | skill.md (3KB) + bug模板 (4KB) = 7KB | 72% |
| 内容创作 | 25KB | skill.md (3KB) + 创作模板 (5KB) = 8KB | 68% |

## 维护指南

### 添加新任务类型
1. 在 `templates/` 目录创建新模板文件（例如：`content-video.md`）
2. 在 `skill.md` 的 Step 2 中添加映射关系
3. （可选）在 `examples/` 添加完整示例

### 修改现有模板
直接编辑 `templates/` 目录下对应的模板文件即可，不影响其他模板。

## 设计原则

符合 [skills设计6个最佳实践原则](../../../1专业技能/AI辅助编程/ClaudeCode工具/技能Skills/[术-操作规范]-skills设计6个最佳实践原则.md) 的：
- **原则2：单一职责** - task-start 只做一件事：生成任务执行文档
- **原则3：渐进式披露** - 核心流程在 skill.md，详细模板在 references/
