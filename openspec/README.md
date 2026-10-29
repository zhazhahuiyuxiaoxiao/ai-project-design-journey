# OpenSpec 使用约定

2026-10-29 接入，采用 `spec-driven`。本轮是既有项目的文档与核心流程基线补录，不把历史工作伪装成事前设计。版本与证据见 [工程基线](../docs/engineering-baseline.md)。

- `config.yaml`：项目上下文和产物规则。
- `specs/<capability>/spec.md`：已核对的核心约定；源码/证据与规格冲突时先记录差异。
- `changes/<change-name>/`：后续变更的 proposal、必要的 delta specs、design、tasks；归档后保留历史。

## 下一次修改

先读取 AGENTS、相关规格、源码及测试，再创建范围明确的变更：

```sh
openspec new change <change-name>
openspec status --change <change-name>
openspec instructions proposal --change <change-name>
```

根据指令补齐 proposal、specs、design、tasks。业务结果、安全或数据兼容变化先确认；小文档修订可以简写。需求使用 `### Requirement:`，正文包含 `SHALL` 或 `MUST`，场景使用 `#### Scenario:` 和 WHEN/THEN。新能力用 ADDED，修改用 MODIFIED，移除必须交代理由和迁移办法。

实施后先验证并更新任务，再归档：

```sh
openspec validate --all --strict --no-interactive
# 仅当本次任务及必需验收完成后执行；有业务 delta 时会同步长期规格
openspec archive <change-name>
```

纯文档变更可明确 `skip_specs: true` 并使用 `archive --skip-specs`，不编造产品需求。不能归档其他未完成变更。归档不等于授权提交、合并、发布或部署。以上命令已按本机 OpenSpec 1.14.2 帮助核对；无需将它加入应用运行依赖。

[官方既有项目指南](https://github.com/Fission-AI/OpenSpec/blob/main/docs/existing-projects.md) · [规格格式](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md)

格式校验只检查规范结构。文档更新检查相对链接、命令来源和 `git diff --check`；业务变化另按项目规则运行测试。
