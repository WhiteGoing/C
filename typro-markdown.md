Typora编辑器，使用Markdown语法

１．基本语法：

２．绘图工具：

Markdown有绘图的语法，但较为复杂，mermaid解决这个痛点，这是一个类似markdown语法的脚本语言，通过JavaScript实现图表的生成。Typora支持mermaid语法。

[mermaid官方网址](https://mermaidjs.github.io/)

流程图基本语法：

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

甘特图：

```mermaid
gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid
        section A section
        Completed task            :done,    des1, 2014-01-06,2014-01-08
        Active task               :active,  des2, 2014-01-09, 3d
        Future task               :         des3, after des2, 5d
        Future task2               :         des4, after des3, 5d
        section Critical tasks
        Completed task in the critical line :crit, done, 2014-01-06,24h
        Implement parser and jison          :crit, done, after des1, 2d
        Create tests for parser             :crit, active, 3d
        Future task in critical line        :crit, 5d
        Create tests for renderer           :2d
        Add to mermaid                      :1d
```

等