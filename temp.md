# mkdocs-material 使用说明

## 创建文档项目

1. `python -m venv .venv`
2. `python -m pip install mkdocs-material`
3. `mkdocs new .`

## 配置项目

- 创建 `.vscode` 目录，创建 `settings.json` 文件，填入

```json
{
    "yaml.schemas": {
        "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
    },
    "yaml.customTags": [
        "!ENV scalar",
        "!ENV sequence",
        "tag:yaml.org,2002:python/name:materialx.emoji.to_svg",
        "tag:yaml.org,2002:python/name:materialx.emoji.twemoji",
        "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format"
    ]
}
```

- 在 `docs` 下创建 `javascripts` 目录，创建 `mathjax.js` 文件，填入

```js
window.MathJax = {
    tex: {
      inlineMath: [["\\(", "\\)"]],
      displayMath: [["\\[", "\\]"]],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      ignoreHtmlClass: ".*|",
      processHtmlClass: "arithmatex"
    }
  };
  
  document$.subscribe(() => {
    MathJax.typesetPromise()
  })
  
```

- 修改 `mkdocs.yml` 文件为

```yml
site_name: name_of_site
site_url: url_of_site
site_author: author_name
site_description: web_description

nav:
  - index: index.md
  
theme:
  name: material
  language: zh
  features:
    - navigation.instant

extra_javascript:
  - javascripts/mathjax.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js

markdown_extensions:

  # Python Markdown
  - abbr
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - toc:
      permalink: true

  # Python Markdown Extensions
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg
  - pymdownx.highlight
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde

plugins: 
  - search

```

- 创建 `.gitignore` 文件，填入 `.venv/`
- 创建一个 `python` 文件，选择 `.venv` 中的解释器，这样当打开终端时，vscode 会自动进入虚拟环境
