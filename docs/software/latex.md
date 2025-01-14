## Latex 

实际使用不需要去背符号，推荐一个[在线 Letex 公式编辑网站](https://www.latexlive.com/home)，先用起来，次数多了，观察的足够了，并且下意识能打出来时自然就会了。

本站用 mkdocs 的 material 主题，使用 Latex 按照官方给出的[配置选项](https://squidfunk.github.io/mkdocs-material/reference/math/)。

美中不足的一点，latex 公式渲染时会较小，当然可以在每个公式前手动添加 `\huge`，但太过麻烦，在给出的 js 中添加扩大比例，


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
  },
  chtml: {
    scale: 2.0 // 设置缩放比例
  }
};

document$.subscribe(() => { 
  MathJax.startup.output.clearCache()
  MathJax.typesetClear()
  MathJax.texReset()
  MathJax.typesetPromise()
})
```

