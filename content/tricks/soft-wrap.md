---
title: "Soft Wrap in Zed Text Editor"
date: "2025-02-18"
summary: "Soft Wrap in Zed Text Editor"
# description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["zed", "soft wrap", "css"]
showTags: false
hideBackToTop: false
---

# Soft Wrap in Zed Text Editor
---

## What is Soft Wrap?
Soft wrap is a feature that allows you to wrap long lines of text so that they fit within the width of the editor window. This can be useful when working with long lines of code or text that would otherwise extend beyond the visible area of the editor.

## How to Enable Soft Wrap in Zed Text Editor

1. Open Zed Text Editor.
2. Click `Ctrl` + `Shift` + `P` to open the command palette.
3. Type `Settings` and select `zed: open settings`.
4. Add the following line to the settings file:
```css
"soft_wrap": "editor_width"
```
5. Save the settings file.
