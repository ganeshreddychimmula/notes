
2025-07-09 18:41

Status:

Tags:

---
# Mermaid Syntax - Guide
Mermaid is a Markdown-inspired tool that renders text into diagrams. For example, Mermaid can render flow charts, sequence diagrams, pie charts and more. For more information, see the [](https://mermaid-js.github.io/mermaid/#/).

Mermaid is a JavaScript based diagramming and charting tool that uses Markdown-inspired text definitions and a renderer to create and modify complex diagrams. The main purpose of Mermaid is to help documentation catch up with development.

[Live Examples](https://mermaid.live/)

## Diagram Syntax

Syntax, together with Deployment and Configuration constitute the whole of Mermaid.

### Syntax Structure

All **Diagrams definitions begin** with a declaration of the **diagram type**, followed by the definitions of the diagram and its contents.
This declaration notifies the parser which kind of diagram the code is supposed to generate. The only exception to this a [](https://mermaid.js.org/intro/syntax-reference.html#frontmatter-for-diagram-code) configuration.

Line comments can ignore anything on the line after `%%`.

Unknown words and misspellings will break a diagram, while parameters silently fail.

### Diagram Breaking

One should **beware the use of some words or symbols** that can break diagrams. These words or symbols are few and often only affect specific types of diagrams. The table below will continuously be updated.


|Diagram Breakers|Reason|Solution|
|---|---|---|
|**Comments**|||
|[`%%{``}%%`](https://github.com/mermaid-js/mermaid/issues/1968)|Similar to [Directives](https://mermaid.js.org/config/directives.html) confuses the renderer.|In comments using `%%`, avoid using "{}".|
|**Flow-Charts**|||
|'end'|The word "End" can cause Flowcharts and Sequence diagrams to break|Wrap them in quotation marks to prevent breakage.|
|[Nodes inside Nodes](https://mermaid.js.org/syntax/flowchart.html?id=special-characters-that-break-syntax)|Mermaid gets confused with nested shapes|wrap them in quotation marks to prevent breaking|
### Frontmatter for diagram code

Frontmatter is the term for adding YAML metadata at the start of code. This allows for reconfiguration of a diagram before it is rendered. You can pass metadata Frontmatter with your definition by adding `---` to the lines before and after the definition. This 'triple dash' MUST be the only character on the first line.

Frontmatter uses YAML syntax. It requires any indentation to be consistent and settings are case sensitive. Mermaid will silently ignore misspelling, but badly formed parameters will break the diagram.
```
---
title: Frontmatter Example
displayMode: compact
config:
  theme: forest
gantt:
    useWidth: 400
    compact: true
---
gantt
    section Waffle
        Iron  : 1982, 3y
        House : 1986, 3y

```


## Diagram Types

### [Flowchart](https://mermaid.js.org/syntax/flowchart.html?id=flowcharts-basic-syntax)

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

 ### [Sequence diagram](https://mermaid.js.org/syntax/sequenceDiagram.html)
 - This looks great for instances where you have 2 or more layers where there multiple to and from actions happens.
 
```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop HealthCheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!

```

### [Gantt diagram](https://mermaid.js.org/syntax/gantt.html)

```mermaid
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d

```
### [Class diagram](https://mermaid.js.org/syntax/classDiagram.html)

```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label


```

### [Git graph](https://mermaid.js.org/syntax/gitgraph.html)

```mermaid
    gitGraph
       commit
       commit
       branch develop
       commit
       commit
       commit
       checkout main
       commit
       commit
```
### [Entity Relationship Diagram - ❗ experimental](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses

```

### [User Journey Diagram](https://mermaid.js.org/syntax/userJourney.html)

```mermaid
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
```

### [Quadrant Chart](https://mermaid.js.org/syntax/quadrantChart.html)

```mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
    Campaign C: [0.57, 0.69]
    Campaign D: [0.78, 0.34]
    Campaign E: [0.40, 0.34]
    Campaign F: [0.35, 0.78]

```

### [XY Chart](https://mermaid.js.org/syntax/xyChart.html)

```mermaid
xychart-beta
    title "Sales Revenue"
    x-axis [jan, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec]
    y-axis "Revenue (in $)" 4000 --> 11000
    bar [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]
    line [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]


```


## Deploying Mermaid

To Deploy Mermaid:

1. You will need to install node v16, which would have npm
2. Install mermaid
    - NPM: `npm i mermaid`
    - Yarn: `yarn add mermaid`
    - Pnpm: `pnpm add mermaid`

### [Mermaid API](https://mermaid.js.org/config/setup/README.html):

**To deploy mermaid without a bundler, insert a `script` tag with an absolute address and a `mermaid.initialize` call into the HTML using the following example:**

```
<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true });
</script>
```

**Doing so commands the mermaid parser to look for the `<div>` or `<pre>` tags with `class="mermaid"`. From these tags, mermaid tries to read the diagram/chart definitions and render them into SVG charts.**

---
## References