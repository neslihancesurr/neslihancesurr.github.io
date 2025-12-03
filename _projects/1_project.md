---
layout: page
title: Custom AMR Graph Builder
description: A Java-based parser for transforming Google Sheets indentation into AMR Graphs
img: assets/img/amr-project-banner.jpg
importance: 1
category: work
related_publications: false
---

This Java project is designed to construct **Abstract Meaning Representation (AMR) Graphs** by parsing a specific, custom "Penman-like" notation.

**[View the Project on GitHub](https://github.com/neslihancesurr/AMRGraphProcessor)**

Unlike standard Penman notation (which uses parentheses for nesting), this project is designed to process data exported from **Google Sheets to CSV**. It relies on **indentation levels** (represented by empty CSV cells) to determine the parent-child relationships between concepts.

## Input Format (The "Google Sheets" Notation)

The parser expects a **CSV file** exported from Google Sheets. The logic separates graphs by headers and determines hierarchy via column indentation.

### Spreadsheet View (Visual)

| Column A (ID/Root) | Column B (Lvl 1) | Column C (Lvl 2) | Note |
| :--- | :--- | :--- | :--- |
| **0463.train** | **SÜREKLİ İLGİLENDİ .** | | *Header Line* |
| `2/ilgilendi` | | | *Root Node (Indent 0)* |
| | `1/sürekli:frequency` | | *Child of ilgilendi (Indent 1)* |
| | `o:ARG0` | | *Child of ilgilendi (Indent 1)* |

**Resulting Logic:**
1.  The parser reads `2/ilgilendi` at **Indent 0**.
2.  It reads `1/sürekli` at **Indent 1** with relation `frequency`. It links `ilgilendi` -> `frequency` -> `sürekli`.
3.  It reads `o` at **Indent 1** with relation `ARG0`. It links `ilgilendi` -> `ARG0` -> `o`.

## Parsing Logic & Algorithm

The `FileReader.java` uses a depth-based reconstruction algorithm to parse these nodes.

1.  **Intermediate Parsing:** It reads the CSV line by line, counting empty strings to determine the `indent` integer.
2.  **Graph Construction:**
    * It iterates through the list of `IndentNodes`.
    * If `nextNode` indent is **+1**, a direct edge is added.
    * If `nextNode` indent is **<= current**, the algorithm backtracks to find the correct parent.

### Usage Code

To run the parser, ensure your CSV is in the `files/` directory and run the main method:

{% raw %}

```java
// In FileReader.java
public static void main(String[] args) throws IOException {
    String csvFile = "files/amrtest7.csv";
    ArrayList<AMRGraph> graphs = processCSVFile(csvFile);
    for (AMRGraph graph : graphs) {
        graph.printGraph();
    }
}
```

{% endraw %}
