# 变更日志 (Changelog)

本文件记录所有重要变动。最近的变动在最前面。

---

## [Unreleased] - 2026-06-29

### 本次会话所有代码变动汇总

> 注：历史部分 commit message 因 Windows CMD GBK 编码导致中文乱码，
> 此文件作为权威变更记录，修复乱码问题。

### 基础设施
- **RustFS → MinIO 替换**：`docker-compose.dev.yml` 用 MinIO 替代 RustFS，
  新增 `createbuckets` 服务自动初始化 bucket
- **端口映射调整**：MinIO 端口统一为 `9002:9000`（API）/ `9003:9001`（控制台），
  同步更新 `application.yml`、`application-test.yml`、`docker-compose.yml`
- **Gradle 下载源**：从腾讯云镜像切回官方 `services.gradle.org`

### Gradle 构建优化（CI 友好）
- **仓库顺序调优**：`mavenCentral` 优先，阿里云镜像作为 fallback
- **pluginManagement 同步**：`settings.gradle` 中全局仓库优先
- **移除 metadataSources**：避免 Gradle 8.14 兼容性问题

### CI/CD 流水线修复
- **Node.js 升级**：22 → 24，消除 GitHub Actions deprecation 警告
- **前端依赖安装**：增加 `--frozen-lockfile` 失败后的 fallback 机制
- **pnpm-lock.yaml 更新**：同步 `remark-breaks@^4.0.0` 依赖
- **错误处理增强**：后端编译/打包增加 `BUILD FAILED` 硬性检查
- **前端构建**：vite build 增加退出码捕获和详细错误输出
- **日志输出**：所有步骤增加完整错误日志输出便于排查

### RAG 知识库统计修复
- **新增方法**：`RagChatMessageRepository.countByTypeAndUserId()` 按用户统计提问次数
- **修复跨用户数据**：`KnowledgeBaseListService` 统计消息数改为按当前用户过滤

### 前端 UI 改进
- **回答换行保留**：`InterviewDetailPanel.tsx` 添加 `whitespace-pre-wrap`
- **Loading 状态**：`InterviewPage.tsx` Session 未加载时展示 spinner，替代空白页

---

## 历史提交对照表（乱码修复）

| Commit | 实际内容 |
|--------|----------|
| `6ec5e3f` | fix: CI流水线失败问题全面修复（Node.js 24 + build.gradle + 错误处理） |
| `b18143e` | feat: RustFS替换为MinIO、Gradle构建CI优化、RAG统计按用户过滤、前端UI改进 |
| `19a3426` | fix: 修复CI流水线运行不了的问题 |
| `87c6dd4` | fix: 修复CI流水线 |
| `8374730` | fix: 修复流水线 |
| `645412f` | fix: 修复第一次点击文字面试出题时页面空白及文字面试用户面板提交文字描述不能换行、分段、隔空的问题 |
