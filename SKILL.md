---
name: resume-publisher-cn
description: 中文简历内容优化与多格式交付。Use when Codex needs to create, optimize, rewrite, tailor, or publish a Chinese resume/CV for job applications, including ATS checks, STAR/量化成果改写, JD 定制, and generating synchronized A4 HTML, Word DOCX, and PDF resume outputs from Markdown + YAML sources. Trigger for 简历、CV、resume、求职、投递、岗位定制、项目经历优化、个人优势、技能描述、Word简历、PDF简历、网页版简历、A4在线简历.
---

# Resume Publisher CN

Use this skill to turn resume material into a polished Chinese A4 resume package: content source, HTML web resume, Word `.docx`, and PDF. Keep all formats synchronized from one `resume.yaml` plus optional `resume.md` source.

## Workflow

1. Ground the source material.
   - If the user provides a `.docx`, `.html`, `.pdf`, or existing `outputs/`, inspect it first and preserve factual claims.
   - Inspect source images. If a source resume includes an ID/profile photo, extract and preserve that photo; if no photo is provided, do not invent or generate one.
   - If starting from scattered notes, create a structured `resume.yaml` and optional `resume.md`.
   - If a JD is supplied, read `references/resume-writing.md` before rewriting.

2. Improve the resume content.
   - Prioritize target-role fit, concrete responsibilities, technical credibility, impact, and ATS readability.
   - Use STAR-style bullets only when the source supports the claim; do not invent metrics, employers, dates, awards, or skills.
   - For Chinese resumes, keep phrasing concise and delivery-oriented.

3. Generate synchronized outputs.
   - Use `scripts/generate_resume.py` for deterministic `html/docx/pdf` generation.
   - If `resume.yaml` includes `photo`, `avatar`, `portrait`, `证件照`, or `照片`, include that image in every generated format. HTML should embed or reliably reference it, DOCX should show it as an ID photo, and PDF should be exported from the image-bearing DOCX.
   - Default command:

```bash
python scripts/generate_resume.py --yaml resume.yaml --markdown resume.md --outdir outputs --formats html docx pdf
```

4. Verify before delivering.
   - HTML: UTF-8 Chinese text is readable, A4 page sizing works, print CSS is present, and mobile does not overflow.
   - DOCX: A4 page size, Chinese fonts, heading hierarchy, bullets, links, margins, ID photo placement, and page breaks are acceptable.
   - PDF: Prefer export from the DOCX using Microsoft Word so the submission file matches the Word version, including any ID photo.
   - Photo rule: When the source had a photo, visually confirm the delivered HTML/DOCX/PDF all still show it. When no photo was supplied, confirm no placeholder photo was added.
   - If PDF export fails because Word is unavailable, deliver HTML and DOCX and clearly state the PDF blocker.

## Source Contract

Use `resume.yaml` for structured facts and `resume.md` for long-form or draft sections.

Recommended `resume.yaml` shape:

```yaml
name: "张三"
target_role: "嵌入式工程师"
photo: "assets/id-photo.jpg" # optional; only use a real source/provided photo
theme:
  accent: "#1F4E79"
contact:
  phone: "13800000000"
  email: "zhangsan@example.com"
sections:
  - title: "个人优势"
    items:
      - "具备嵌入式设备研发经验，覆盖驱动、通信、UI、测试与交付。"
  - title: "重点项目"
    entries:
      - heading: "多参数监护仪 | RTOS / LVGL / WiFi / 蓝牙"
        bullets:
          - "负责测量流程、UI交互、通信上报和版本升级相关功能开发。"
```

For `resume.md`, parse headings as sections and bullet lines as section items.

## Resources

- Read `references/resume-writing.md` for ATS, JD tailoring, STAR bullets, and Chinese resume content rules.
- Read `references/a4-web-resume.md` when changing HTML, print CSS, mobile layout, or SEO metadata.
- Use `assets/templates/a4-resume.css` as the default web and print styling reference.
- Use `assets/templates/resume.example.yaml` and `assets/templates/resume.example.md` as source examples.
- Use `scripts/extract_docx_text.py` to extract plain text from a `.docx` when converting an old resume into the source format.

## Output Rules

- Default filenames: `outputs/<姓名>-<岗位>-简历.html`, `.docx`, `.pdf`.
- Keep generated files UTF-8 and avoid garbled Chinese.
- Preserve provided ID/profile photos across all deliverables. If the source contains multiple images, keep the candidate photo and ignore purely decorative lines/backgrounds unless the user asks otherwise.
- Do not recursively delete or batch-delete generated files. If cleanup is required, delete only one explicit file path at a time or ask the user to clean manually.
- Prefer one-page A4 for early-career resumes; allow two pages only when the user asks or the career history truly needs it.
- Preserve privacy: do not publish phone, email, address, ID number, or private links to a public website unless the user explicitly approves.
