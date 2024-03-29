---
title: CSS工具
---
CSS工具

![](../../.vuepress/public/fe/css.svg)

## less和sass
他们属于css中的预处理器，流程是 类css代码 => 预处理器 => css代码，预处理器普遍会具备这样的特性：

+ 嵌套代码的能力，通过嵌套来反映不同 css 属性之间的层级关系 ；
+ 支持定义 css 变量；
+ 提供计算函数；
+ 允许对代码片段进行 extend 和 mixin；
+ 支持循环语句的使用；
+ 支持将 CSS 文件模块化，实现复用。

可以优化css目录结构，让代码风格更清晰，维护性更高


## POSTCSS
PostCSS 是一个强大的 CSS 处理工具，它使用 JavaScript 插件来转换和优化 CSS 代码。PostCSS 本身是一个用于解析和处理 CSS 的框架，它的核心功能依赖于各种插件。这些插件可以帮助开发者自动添加浏览器前缀、优化 CSS 代码、支持新的 CSS 特性等。

以下是一些 PostCSS 的主要特点：

1. **插件式架构**：PostCSS 的核心功能依赖于各种插件，这些插件可以按需添加，从而实现定制化的 CSS 处理流程。

2. **高性能**：PostCSS 使用高效的 CSS 解析器，可以快速处理大量的 CSS 代码。

3. **灵活性**：PostCSS 支持各种 CSS 预处理器（如 Sass、Less 等）以及其他构建工具（如 Webpack、Gulp、Grunt 等）。

4. **支持未来 CSS 特性**：通过使用 PostCSS-preset-env 插件，PostCSS 可以让开发者提前使用最新的 CSS 特性，同时保证向后兼容。

5. **自动添加浏览器前缀**：Autoprefixer 插件可以根据开发者设置的浏览器支持情况，自动为 CSS 代码添加浏览器前缀。

6. **代码优化**：PostCSS 提供了一系列插件来优化 CSS 代码，例如 cssnano 可以压缩 CSS 代码，postcss-merge-rules 可以合并相同的 CSS 规则等。

要使用 PostCSS，你需要先安装它和相关插件，然后配置你的构建工具（如 Webpack、Gulp 或 Grunt）以使用这些插件。这样，在构建过程中，PostCSS 会自动处理你的 CSS 代码，使其更加高效、兼容和易于维护。

它和预处理器的不同就在于，预处理器处理的是 类CSS，而 PostCss 处理的就是 CSS 本身。Babel 可以将高版本的 JS 代码转换为低版本的 JS 代码。PostCss 做的是类似的事情：它可以编译尚未被浏览器广泛支持的先进的 CSS 语法，还可以自动为一些需要额外兼容的语法增加前缀。更强的是，由于 PostCss 有着强大的插件机制，支持各种各样的扩展，极大地强化了 CSS 的能力。
PostCss 在业务中的使用场景非常多：

提高 CSS 代码的可读性：PostCss 其实可以做类似预处理器能做的工作；
当我们的 CSS 代码需要适配低版本浏览器时，PostCss 的 Autoprefixer 插件可以帮助我们自动增加浏览器前缀；
允许我们编写面向未来的 CSS：PostCss 能够帮助我们编译 CSS next 代码

**webpack这种打包工具原生不具备打包css功能，但在loder的辅助下就可以了**

Webpack 中操作 CSS 需要使用的两个关键的 loader：css-loader 和 style-loader
+ css-loader：导入 CSS 模块，对 CSS 代码进行编译处理；
+ style-loader：创建style标签，把 CSS 内容写入标签。