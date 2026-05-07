# A4 Web Resume Reference

Use this reference when generating or revising the HTML resume output.

## Layout Defaults

- Use a single static HTML file with embedded CSS by default.
- Page size should mimic A4: `210mm` wide, `297mm` minimum height.
- Use print CSS so browser printing keeps white paper, no shadow, and A4 dimensions.
- Keep body text readable: 12-13px for dense A4 resumes, larger on narrow screens.
- Use one restrained accent color per target role; avoid decorative gradients or card-heavy landing-page styling.

## HTML Structure

- Use semantic sections with real text:
  - `header` for name, target role, contact.
  - `section` for resume sections.
  - `h2` for section titles.
  - `h3` for project/work entry headings.
  - `ul/li` for bullets.
- Set `<html lang="zh-CN">`, `<meta charset="utf-8">`, and responsive viewport.
- Use a descriptive `<title>`: `<姓名>-<岗位>-简历`.

## Mobile Behavior

- On small screens, let the page become full width.
- Reduce margins and remove page shadow.
- Do not require horizontal scrolling for normal reading.
- Keep contact items wrapping cleanly.

## Print Behavior

Include:

```css
@page { size: A4; margin: 0; }
@media print {
  body { background: #fff; }
  .page { width: 210mm; min-height: 297mm; box-shadow: none; margin: 0; }
}
```

## Privacy and Public Sharing

- Public personal sites should not expose full phone numbers, private email aliases, home addresses, ID numbers, or private repository links without explicit approval.
- A4 HTML intended only for local preview may include the same contact details as the DOCX/PDF.
