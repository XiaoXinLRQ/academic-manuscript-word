# Word 默认学术排版 Skill

为 Codex 新建 Word/DOCX 文件提供简洁、传统的默认格式：中文宋体/SimSun，英文 Times New Roman，A4，原生 Word Styles，集中参数配置和 PDF 逐页视觉验收。

本项目是一套可复用的 Skill 指令与配置，不是独立的 DOCX 转换程序。不修改已有 Word，也不强制生成摘要、关键词或参考文献。内容生成按用户任务授权执行，排版阶段保护已确定内容。

## 安装与使用

将 `academic-manuscript-word` 文件夹复制到个人 Codex skills 目录（通常为 `~/.codex/skills/`）。保留已有其他 Skill。新建任务后可以显式调用：

```text
使用 $academic-manuscript-word 生成一份 Word 文件。
```

自动发现已在 `agents/openai.yaml` 中启用。如希望所有新建 Word 都使用该格式，将 `AGENTS.example.md` 中的默认 Word 指令合并到个人 Codex 指令文件（通常为 `~/.codex/AGENTS.md`）；不要覆盖原有其他指令。按实际安装位置调整其中的 Skill 路径，并在新任务中检查是否加载。

用户明确指定其他模板、字体或版式时，该任务要求优先。

## 配置

- `academic-manuscript-word/assets/manuscript-defaults.json`：全部默认格式参数。
- `config/task-overrides.example.json`：任务覆盖示例；对象深度合并，数组整体替换，保存合并后的 `resolved-config.json`。
- `academic-manuscript-word/references/configuration.md`：单位、样式继承和配置优先级。

默认正文为 12 pt、1.5 倍行距、两个字符首行缩进、两端对齐；页边距为 25.4 mm。题目、四级标题、正文、摘要、关键词、图题、表题、参考文献均有独立样式。图表采用居中图片、三线表、原生 SEQ 题注和 REF 交叉引用。

参考文献可配置 GB/T 7714、APA、IEEE 等体例标签；默认保留条目内容。标签切换不等于完整引用体例转换，也不保证符合特定期刊官方规范。

## 生成与验收要求

先初始化样式，再写内容。标题必须在首次导出前清除字体主题、主题颜色和装饰边框，并检查有效继承；不能靠首轮视觉检查发现蓝色标题再常规返工。

完成 DOCX → PDF → 全部页面图像 → 逐页视觉检查。首轮通过即结束，只在发现实际问题或文件修改后重新导出检查。此规则避免已知问题造成多余工作，不取消视觉验收，也不保证所有复杂布局都无需修复。

需要 DOCX 生成/OOXML 工具、具备相关字体的 Word 或兼容 PDF 导出引擎，以及页面图像查看能力。数学对象或复杂域须保留兼容字体与结构。缺字体、无法更新域或无法渲染时应标记待验收，不能假报通过。

## 文件结构

```text
academic-manuscript-word/
  SKILL.md
  agents/openai.yaml
  assets/manuscript-defaults.json
  references/configuration.md
  references/word-implementation.md
  references/qa.md
AGENTS.example.md
config/task-overrides.example.json
```

本次发布前已通过 Skill 结构校验与 JSON 解析检查。此前生成的三页演示稿完成 Word 导出 PDF 和逐页检查，并验证了标题主题覆盖修复；这不是对所有稿件、渲染引擎或参考文献体例的全面兼容性承诺。
