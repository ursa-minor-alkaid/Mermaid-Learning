# Mermaid 2：流程图

流程图（flow chart），也称为graph，是各个领域中最常见和最通用的图表之一

流程图由边和节点组成。The Mermaid code defines how nodes and edges are made and accommodates different arrow types, multi-directional arrows, and any linking to and from subgraphs.

## 起始语法

### 流程图方向

flowchart 关键字或 graph 关键字用于表示流程图定义的开始

流程图的方向定义如下：

- TD - 从上到下
- BT - 从下到上
- RL - 从右到左
- LR - 从左到右

### title

可以用 `---` 包裹 `title`

- *官方文档说还可以包括 `theme` 和 `look`，但是vscode里面好像不能实现这两个功能*

```
---
title: A
%% 记得冒号后有空格
---
```

代码示例：

```mermaid
---
title: node
---

flowchart BT
    Watermelon --> Banana;
```

## 节点形状

默认是矩形，除此之外的形状展示在下方代码中

注意：
- 自定义形状的话需要写node的id
- id与后面的符号之间不能有空格
- id类似于别的语言中的id，是唯一的，不能给两个节点命名同一个id

```mermaid
graph RL
    id1(圆角矩形);
    id2([带长边的椭圆（？），官方叫“体育场形”]);
    C{菱形，这个比较好记}-->4((圆形，这个也好记));
    a>这个莫名其妙的形状]-->id3{{六边形}};
    id4[/平行四边形/]-->id5[/梯形\]-->id6[(数据库形)];
    %%还有些少见的就没放上来
```

现在mermaid支持新的写法：`id@{ shape: 形状, label: "内容" }`

代码示例

```mermaid
graph TD
    A@{ shape: hourglass, label: "Collate" }-->B@{ shape: braces, label: "Comment" }
```

## Links between nodes

### 连线类型

见下方代码示例：

```mermaid
flowchart LR
    A-->B---C
    D-->|text|E---|text|F
    G-.->H==>I
    J-.->|text|K==>|text|L
    M~~~N 
    %%这个是隐形线
    O --o P --x Q
    R o--o S<-->T x--x U
    %%ox的这两个最好带空格，不然可能识别成id了
```

### "Network"

可以实现复杂的连线效果
- `-` 越多，连线越长
- 具体见下方代码示例：

```mermaid
flowchart LR
   a --> b & c--> d
   A & B--> C & D------>E
```

另一复杂示例：

```mermaid
flowchart TD
    A[Start] --> B{Is it?}
    B -- Yes --> C[OK]
    C --> D[Rethink]
    D --> B
    B -- No ----> E[End]
```

### 连线id

还可以给连线加id，通过@实现

- 结合前面的（借助@实现节点样式），这似乎是mermaid的一个语法格式： `id@{ 键值对 }`
- 可以借此实现动画（这有啥用？）

```mermaid
flowchart LR
  A e1@==> B
  e1@{ animate: true }
```

### 转义

*Special characters that break syntax*

使用 `"text"` 双引号来确保内容一定被识别成文字，而不是特殊字符

## 子图（subgraphs）

### 基本语法

```
subgraph title
    graph definition (contents)
end
```

示例如下：

```mermaid
flowchart TB
    c1-->a2
    subgraph one
    a1-->a2
    end
    subgraph three
    c1-->c2
    end
```

```mermaid
flowchart TB
    c1-->a2
    subgraph ide1 [one]
    a1-->a2
    end
```

### 子图间连线

子图间也可以连线
- 写在最后
- 示例如下：

```mermaid
flowchart TB
    c1-->a2
    subgraph one
    a1-->a2
    end
    subgraph two
    b1-->b2
    end
    subgraph three
    c1-->c2
    end
    one --> two
    three --> two
    two --> c2
```

### 子图内方向

子图内可以定义与外面不同的方向
- 使用 `direction`
- 示例如下：

```mermaid
flowchart LR
  subgraph TOP
    direction TB
    subgraph B1
        direction RL
        i1 -->f1
    end
    subgraph B2
        direction BT
        i2 -->f2
    end
  end
  A --> TOP --> B
  B1 --> B2
```
### 一个来自AI的语法建议

- 可以先写出所有的节点（`= 质料`），再在最下面写出节点之间的关系（`= 形式`）
- 示例代码如下

```mermaid
graph LR
    %% 所有node
    P(哲学)
    P1(欧陆)
    P2(精分)
    P3(辅修)

    P1a(先验观念论)
    P1b(精神现象学)
    P1c(逻辑学)
    P1d(小逻辑)
    P1e(法哲学原理)
    P1f(世界时代)
    P1g(现象学)
    P1h(海德格尔)
    P1i(生存论)

    P2a(Nobus拉康)
    P2b("“重启”弗洛伊德")
    P2c(结构主义)
    P2d(拉康)
    P2e(齐泽克)

    P3a(还原论及等级系统)
    P3b(康吉莱姆)
    P3c(组学时代发展历史)
    P3d(毕设及模型构建)

    M(马)

    %% 三个分支
    P --> P1
    P --> P2
    P --> P3

    %% 分支1路线
    P1 --> P1a --> P1b --> P1c --> P1d --> P1e
    P1e --> P1f
    P1e --> P1g
    P1g --> P1h --> P1i

    %% 分支2路线
    P2 --> P2a --> P2b --> P2c --> P2d --> P2e

    %% 分支3路线
    P3 --> P3a --> P3d
    P3 --> P3b --> P3c --> P3d

    %% 分支间路线
    P1b -.-> P2d
    P1d -.-> P2e
    P1f -.-> M
    P1i -.-> M
    P2e -.-> M

    style P fill:#4F46E5,color:#fff
    style M fill:#FBBF24,color:#000
```

## Styling and classes

待补充，详见官网文档

## 其他

还有如下内容，此处略，详见官网文档：https://mermaid.js.org/syntax/flowchart.html
- 使用markdown（倒反天罡（bushi）
- Interaction（链接）