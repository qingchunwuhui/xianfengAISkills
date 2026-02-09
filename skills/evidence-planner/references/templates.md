# Evidence Planner Templates

该文件包含不同场景下的分镜表模板和示例。

## 1. 配图命名规范 (Naming Convention)

为了便于知识库检索与复盘，实战类配图建议遵循 **“线性排序 + 中文语义”** 的命名法：

> **格式**: `序号-关键对象-状态动作.png`
> **示例**: `01-网络-Ping超时.png`

---

## 2. 标准通用模板 (Standard Template)


```markdown
## Evidence Shot List (实战分镜表)
> **任务**: {TaskName}

### Must-Have (核心证据)
*缺失此类证据将导致无法复盘或证明问题已解决。*

- [ ] **{Item_Name_PascalCase}**
    - **建议文件名**: `{01-对象-动作.png}`
    - **Target**: {Description - 截哪里，包含什么关键信息}
    - **Role**: {Description - 这张图在文章/文档中起什么作用，如"证明故障复现"或"展示关键配置"}

### Nice-to-Have (辅助证据)
*有助于丰富上下文，但非阻断性证据。*

- [ ] **{Item_Name_PascalCase}**
    - **建议文件名**: `{02-对象-动作.png}`
    - **Target**: {Description}
    - **Role**: {Description}
```

## 3. 场景化最佳实践 (Scenario Examples)

### 场景: 排查 Webpack 打包卡死 (Debugging)
**Must-Have**:
- [ ] **Terminal_Freeze_Log**
    - **建议文件名**: `01-终端-构建卡死.png`
    - **Target**: 截取最后停止的 Log 输出行（需包含上一条正常 Log）。
    - **Role**: 在"故障复现"章节展示问题现场，证明进程确实卡死及卡死的具体位置。
- [ ] **Webpack_Config_Section**
    - **建议文件名**: `02-代码-Webpack配置.png`
    - **Target**: 截取 `webpack.config.js` 中 `plugins` 和 `loaders` 的配置代码块。
    - **Role**: 在"排查过程"章节作为分析对象，方便后续指出的配置错误。

**Nice-to-Have**:
- [ ] **System_Resource_Monitor**
    - **建议文件名**: `03-系统-内存占用.png`
    - **Target**: 任务管理器中 Node.js 进程的 CPU/内存占用波形图。
    - **Role**: 辅助证明是否因内存泄漏 (OOM) 导致的卡死。
- [ ] **Dependency_Tree**
    - **建议文件名**: `04-环境-依赖树.png`
    - **Target**: 命令行运行 `npm list` 或 `package.json` 的关键依赖版本。
    - **Role**: 记录环境版本信息，用于排除版本不兼容的可能性。

### 场景: 部署 Docker 容器失败 (Deployment)
**Must-Have**:
- [ ] **Container_Error_Logs**
    - **建议文件名**: `01-Docker-启动报错.png`
    - **Target**: `docker logs <container_id>` 输出的关键报错段落（Stack Trace）。
    - **Role**: 核心证据，在"问题分析"章节展示报错的根本原因。
- [ ] **Dockerfile_Content**
    - **建议文件名**: `02-代码-Dockerfile配置.png`
    - **Target**: 构建该镜像的 Dockerfile 内容，特别是 `CMD` 或 `ENTRYPOINT` 部分。
    - **Role**: 作为"代码审计"的依据，展示构建逻辑。

**Nice-to-Have**:
- [ ] **Container_Status_List**
    - **建议文件名**: `03-Docker-容器列表.png`
    - **Target**: `docker ps -a` 的输出列表截图。
    - **Role**: 展示容器的生命周期状态（Exited code），补充环境上下文。

### 场景: 前端 UI/CSS 还原 (Frontend)
**Must-Have**:
- [ ] **Figma_Design_Spec**
    - **Target**: Figma 中目标区域的设计规范（间距、颜色、字体）。
    - **Role**: 在"需求分析"章节作为标准参考图（Expected Result）。
- [ ] **Browser_Render_Result**
    - **Target**: 浏览器中实际运行的界面截图。
    - **Role**: 在"效果对比"章节作为实际结果图（Actual Result）。

**Nice-to-Have**:
- [ ] **DevTools_Computed_Styles**
    - **Target**: Chrome DevTools 中 Computed 标签页下的关键 CSS 属性计算值。
    - **Role**: 辅助解释为什么样式渲染不正确（如被权重覆盖）。

### 场景: 后端 API 联调 (Backend)
**Must-Have**:
- [ ] **Postman_Request_Details**
    - **Target**: Postman 的请求界面，包含 Headers 和 Body 参数。
    - **Role**: 证明请求参数构造的正确性。
- [ ] **Postman_Response_Error**
    - **Target**: 接口返回的状态码（如 500）和 JSON Error Message。
    - **Role**: 展示服务端返回的具体错误信息。
- [ ] **Database_State_Change**
    - **Target**: SQL 查询结果，展示数据在操作前后的变化（或未变化）。
    - **Role**: 验证接口逻辑是否真实落地到了数据库层面。
