# course-material

一套把**讲义 / 论文 PDF/PPTX** 变成**复习资料、深度讲解（深讲）、论文读讲、组会报告、课程综述**的 DSH skill：固定七步流水线，交付 Markdown + Word。

核心不是「让模型自由发挥」，而是把流程固化下来：

```text
读讲义 → 定范围 → 写 SPEC → 分章派发 → 统稿 → 配图 → 转 docx → 交付清单
```

每一步都有检查点，SPEC、任务书、质检清单、交付格式都给了模板，照抄即可。

## 安装

### DSHM

DSHM 的 `$DSH_HOME/skills/` 是**一个技能一个 `.md` 文件**（扁平目录），把 `SKILL.md` 复制成同名文件即可：

```bash
cp SKILL.md "$DSH_HOME/skills/course-material.md"
```

重开 DSHM（或新会话）后，技能列表里就会出现 `course-material`。

### Claude Code

Claude Code 使用 `skills/<name>/SKILL.md` 的目录结构，放到用户级或项目级目录即可：

```bash
mkdir -p ~/.claude/skills/course-material
cp SKILL.md ~/.claude/skills/course-material/SKILL.md
```

> 不同版本的 skills 目录约定可能不同，以所用工具的文档为准；本 skill 本身只是纯 Markdown 指令，不依赖特定运行时。

## 适用场景

| 场景 | 产出 |
|---|---|
| 课程 PDF/PPTX 讲义 → 复习资料 / 期末复习 / 章节总结 | 按章 md + docx |
| 某一节要「讲透」 → 深度讲解（深讲） | 推导链完整的 md + docx |
| 例题 / 作业 → 例题讲解、作业答案 | 题目 + 思路 + 推导 + 结果 |
| 中学物理补习 → 串讲方案 + 学生讲义 + 授课 PPT | 方案、讲义、PPT |
| 科研论文 / 预印本 / 综述 → 论文读讲、组会报告、读书笔记、课程综述 | 读讲稿 / 报告 / 综述 + 引用表 |
| 学术论文写作（结构、引用、图表规范） | 论文草稿 + 检查清单 |

**不适用**：单点知识问答、只做 PDF→Word 转换（用 `pdf-convert`）、只核文献真假（用 `literature-verify`）、只改 PPT 排版（用 `make-ppt`）。

## 依赖的其他 skill

| skill | 是否必需 | 用途 |
|---|---|---|
| `md2docx` | **必需**（要 docx 时） | Markdown/LaTeX → Word，公式转原生 OMML，`--strict` 验收 |
| `make-ppt` | 可选 | 课程 PPT、教学示意图 / 电路图 |
| `ohos-doc-read` | 可选 | 读 PDF/PPTX、扫描页导出。**DSHM 专属**；没有它时可用任意 PDF 文本提取工具（`pdftotext`、PyMuPDF、`pdfplumber` 等）替代，按页输出 `--- [page N] ---` 分隔即可 |
| `scifig` / `diagram` | 可选 | 数据图 / 函数图（教学插图档）、流程示意图 |
| `agent-teams` | 可选 | 多章并行写作时的团队模板与任务书 |
| `literature-verify` | 可选 | 论文读讲前先核查事实与引用 |

缺少可选 skill 时，skill 正文里的对应步骤按「用等价工具 + 保留同一检查点」执行；`md2docx` 是唯一影响最终交付格式的硬依赖。

## 许可

MIT，见 [LICENSE](LICENSE)。
