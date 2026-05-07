# Resume Publisher CN

`resume-publisher-cn` 是一个用于中文简历优化与多格式交付的 Codex Skill。它可以把已有简历、零散素材或岗位定制需求整理为结构化简历源文件，并生成同步的 A4 HTML、Word DOCX 和 PDF 版本。

## 功能特点

- 面向中文求职场景优化简历内容，支持岗位定制、个人优势、技能描述、项目经历和实习/工作经历改写。
- 使用 `resume.yaml` 和可选 `resume.md` 作为统一数据源，避免 HTML、DOCX、PDF 多版本内容不一致。
- 生成适合投递的一页 A4 简历，默认支持中文字体、打印样式、章节层级和项目条目。
- 支持证件照：原简历或源文件提供照片时，生成的 HTML、DOCX、PDF 都会保留；未提供照片时不会生成占位图。
- 支持从旧 DOCX 提取文本，辅助把旧简历转换成可维护的结构化源文件。

## 目录结构

```text
resume-publisher-cn/
├── SKILL.md                         # Codex Skill 主说明
├── agents/openai.yaml               # Codex UI 元信息
├── assets/templates/                # A4 简历样式与示例源文件
├── references/                      # 简历写作与 A4 网页简历参考
└── scripts/                         # 简历生成与 DOCX 文本提取脚本
```

## 快速使用

准备 `resume.yaml`：

```yaml
name: "张三"
target_role: "电气工程师助理"
photo: "assets/id-photo.jpg"
contact:
  phone: "13800000000"
  email: "zhangsan@example.com"
sections:
  - title: "个人优势"
    items:
      - "具备电气图纸识读、布线接线、设备装配和基础调试经验。"
  - title: "核心技能"
    items:
      - "电气装配与调试：电气图纸识读、接线工艺、通电测试。"
```

生成 HTML、DOCX 和 PDF：

```bash
python scripts/generate_resume.py --yaml resume.yaml --outdir outputs --formats html docx pdf
```

如果还需要从旧 DOCX 中提取文本：

```bash
python scripts/extract_docx_text.py old-resume.docx --output resume-source.txt
```

## 证件照规则

- 如果源简历中包含证件照或 `resume.yaml` 中配置了 `photo`、`avatar`、`portrait`、`证件照`、`照片` 字段，生成结果必须保留照片。
- 如果源文件包含多张图片，应优先保留候选人证件照，忽略装饰线、背景图等非必要图片。
- 如果没有提供真实照片，不生成、补画或放置占位照片。

## 导出说明

- HTML 使用内嵌样式，适合浏览器预览和打印。
- DOCX 使用 A4 页面、中文字体和简洁章节排版。
- PDF 优先由 Microsoft Word 从 DOCX 导出，保证投递版本和 Word 版本一致。
- 在非 Windows 或无 Microsoft Word 环境下，PDF 导出可能不可用，此时可先交付 HTML 和 DOCX。

## 适用场景

- 中文简历内容优化
- 针对 JD 的求职简历定制
- Word/PDF/HTML 简历同步生成
- 早期职业、实习、校招简历整理
- 需要保留证件照的中文投递简历

## License

本项目使用仓库中的 `LICENSE` 许可。
