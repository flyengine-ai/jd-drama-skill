# 剪单短剧 Skill

剪单 AI 营销短剧创作平台官方 Agent Skill，用于指导 Codex、OpenClaw、TRAE 等智能体通过 `jd-drama` CLI 安全调用剪单短剧能力。

## 当前状态

- Skill 版本：`1.0.0-beta.3`
- CLI 包：`@flyengine/jd-drama-cli`
- 服务地址：[jiandan.flyengine.cn](https://jiandan.flyengine.cn/)
- 发布阶段：公开测试

公测版连接正式环境，会读取真实项目并使用真实创点。所有写操作都应先用 `--dry-run` 预览，再由用户明确同意后使用 `--confirm`。

## 支持能力

- 查询短剧项目和品牌。
- 根据创意或上传剧本创建短剧项目。
- 读取和管理剧本、大纲、角色、场景、道具与形象资产。
- 查询、优化和修改分镜。
- 生成视频并检查任务进度。
- 诊断失败任务并生成恢复建议。

## 安装 CLI

```bash
npm install -g @flyengine/jd-drama-cli@beta
jd-drama --version
```

## 安装 Skill

### Codex

```bash
jd-drama --json skill install --target codex --scope user --dry-run
jd-drama --json skill install --target codex --scope user --confirm
```

### OpenClaw

```bash
jd-drama --json skill install --target openclaw --scope user --dry-run
jd-drama --json skill install --target openclaw --scope user --confirm
```

### TRAE

在目标项目目录中执行：

```bash
jd-drama --json skill install --target trae --scope project --project-dir . --dry-run
jd-drama --json skill install --target trae --scope project --project-dir . --confirm
```

也可以使用目标智能体提供的 GitHub Skill 安装能力，直接从本仓库安装根目录下的 `SKILL.md`。

## 网页授权

```bash
jd-drama auth login
jd-drama --json release-check
```

授权在剪单网页完成。不要向智能体提供剪单密码、手工复制的 Token、授权码或本地配置文件。

## 快速验证

```bash
jd-drama --json projects list --limit 10
jd-drama --json brands list --limit 10
jd-drama --json ai-script options
```

只预览创建计划，不写入数据：

```bash
jd-drama --json ai-script create \
  --idea "一支突出产品卖点的都市反转营销短剧" \
  --episode-count 1 \
  --name "CLI公测项目" \
  --generate \
  --dry-run
```

## 安全边界

- 智能体调用统一使用 `--json`。
- 写操作先用 `--dry-run`，确认后再使用 `--confirm`。
- 不通过原始接口绕过 CLI 的安全限制。
- 不泄露密码、授权码、本地配置文件或 Token。
- 不在重要的正式项目上测试删除和批量修改。
- 品牌只能在第一次创建项目时关联。

完整智能体工作流见 [SKILL.md](./SKILL.md)。

## 使用许可

本仓库中的 Skill 文件按 [MIT-0 许可证](./LICENSE)发布。该许可证不适用于剪单服务、API、CLI 实现、商标、用户账号、额度或生成内容，具体边界见 [NOTICE](./NOTICE)。
