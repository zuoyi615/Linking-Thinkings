---
tags:
  - Chart
created_at: 2026-01-14
category:
  - flowchart
published:
---
# 流程图

- 流程图是一个过程或者系统的一种视觉呈现，它使用符号和连接线演示过程中涉及的步骤顺序，分支以及操作。流程图在许多领域中被广泛地应用，包括商业/工程/软件开发/项目管理等，它以一种清晰且简单的方式来表达复杂的过程或者流程。
- 流程图由多个节点和边缘组成（线条或箭头），`Mermaid` 代码定义了节点和边缘如何生成，包含了不同的箭头类型，多向箭头，如何与子流程图相连

| 符号         | 名称    | 用途                  |
| :--------- | :---- | :------------------ |
| 圆角矩形       | 开始/结束 | 通常表示一个流程的开始和结束      |
| 矩形         | 行为操作  | 表示在这个节点需要做的操作或者执行任务 |
| 菱形         | 分支    | 表示流程在当前节点会有多个条件分支   |
| 平行四边形（斜切形） | 输入/输出 | 表述数据或者信息的输入输出       |
| 箭头         | 链接方向  | 链接不同的节点，表示流程的方向     |

## 基础

```mermaid
flowchart
	A[start]
	B
	A --> B & C
```

```mermaid
flowchart
	A[start]
	B
	A --> B
	A --> C
```

## 方向

- **TB**: Top to bottom
- **TD**: Top to down / same as top to bottom
- **BT**: Bottom to top
- **RL**: Right to left
- **LR**: Left to Right

```mermaid
flowchart LR
	A ---> B
	A ---> C
	C ---> D
```

## 节点文字


```mermaid
flowchart
	A[Family]
	B["Man 👨‍🦰"]
	C[Woman 👩‍🦰
		#quot;Bags#quot;
		shows
	]
	A --> B
	A --> C & D[children]
	C --> F[Married #9829;]
	B --> F
	D --> G["`__Girl__`"]
	D --> H["`***Boy***`"]
```

## 连接线

```mermaid
flowchart
	%% A <-.-> B // comment
	A <-.-> B
	C --o D
	E -.- F
	G x--x H
	I --关系--> J
	K -.->|关系| L
	M ~~~|relate| N
	

	%% O --> Q
	%% O --> P
	%% R --> Q
	%% R --> P
	
	O & R --> Q & P
```

```mermaid
flowchart LR
A1 --text--> B1 -- text1 --> C1 -.-> |text2| A1
```

```mermaid
flowchart
	A --> C
	A --> D
	B --> C
	B --> D
	C --> F --> H
	A -...-> G
```

## 子流程图

```mermaid
graph LR
	one("single")
	subgraph two["double"]
		direction TB
		B1 --> B2
	end
	subgraph three["triple"]
		%% direction LR
		direction TB
		C1 -.-> C2 & C3
	end
	subgraph multiple
		subgraph four
			D1 -.-> D2
		end
		subgraph five
			direction TB
			E1 -.-> E2
		end
	end
	six("end")
	
	one ---> two -.-> three --> multiple --> six
	
	style one fill:#bbf,stroke:#f66,stroke-width:0,color:#fff
	style six fill:#bbf,stroke:#f66,stroke-width:0,color:#fff
```

## 事件交互

```mermaid
graph
	A(["start"]) --> B --> C & D --> F
	%% class A internal-link;
	click B "https://www.google.com" "Goto github"
	%% 在 obsidian 中，有内部链接和外部链接两种方式可用
```

在 `obsidian` 中，有**内部链接**和**外部链接**两种交互方式可用

## 自定义样式

```mermaid
---
config:
  theme: base
  flowchart:
    curve: stepAfter
---
graph TB
    A([Start]) --> B[Input X]
    B --> C{"x > 5 ?"}
    C -..-> |yes| D([End])
    C --> |no| E[/print x/]
    E --> F[x=x+1]:::bigger
    F --> C
    
    linkStyle 0,1,5 stroke:#F00,stroke-width:0.2px
    %% style B stroke-width: 0
    %% style C stroke-width: 0
    
    classDef bigger font-size:15pt,stroke-width:10px
    %% classDef no-border stroke-width: 0
    %% class B,C no-border
    %% class A,E bigger
    %% 这是覆盖默认设置，影响所有图形
    classDef default stroke-width: 0
```


```mermaid
---
config:
  theme: 'base'
  themeVariables:
    primaryColor: '#BB2528'
    primaryTextColor: '#fff'
    primaryBorderColor: '#7C0000'
    lineColor: '#F8B229'
    secondaryColor: '#006100'
    tertiaryColor: '#fff'
---
graph TD
  A[Christmas] -->|Get money| B(Go shopping)
  B --> C{Let me think}
  B --> G[/Another/]
  C ==>|One| D[Laptop]
  C -->|Two| E[iPhone]
  C -->|Three| F[fa:fa-car Car]
  subgraph section[" "]
	C
	D
	E
	F
	G
  end

```

## 线条动画

obsidian 内置的 mermaid 暂时不支持线条动画，可以从官网文档中查看[线条动画](https://mermaid.js.org/syntax/flowchart.html#turning-an-animation-on)
