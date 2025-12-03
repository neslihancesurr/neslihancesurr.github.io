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

Unlike standard Penman notation (which uses parentheses for nesting), this project is designed to process data exported from **Google Sheets to CSV**. It relies on **indentation levels** (represented by empty CSV cells) to determine the parent-child relationships between concepts.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/google-sheet-input.jpg" title="Google Sheets Input" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/java-parser-logic.jpg" title="Java Parsing Logic" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amr-graph-output.jpg" title="AMR Graph Output" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The workflow: Raw data is entered in Google Sheets (Left), parsed by the FileReader algorithm (Middle), and reconstructed into a directed AMR Graph (Right).
</div>

## Input Format (The "Google Sheets" Notation)

The parser expects a **CSV file** exported from Google Sheets. The logic separates graphs by headers and determines hierarchy via column indentation.

### Spreadsheet View (Visual)

| Column A (ID/Root) | Column B (Lvl 1) | Column C (Lvl 2) | Note |
| :--- | :--- | :--- | :--- |
| **0463.train** | **SÜREKLİ İLGİLENDİ .** | | *Header Line* |
| `2/ilgilendi` | | | *Root Node (Indent 0)* |
| | `1/sürekli:frequency` | | *Child of ilgilendi (Indent 1)* |
| | `o:ARG0` | | *Child of ilgilendi (Indent 1)* |

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/csv-indentation-detail.jpg" title="Detailed CSV View" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Visualizing the Indentation Logic: The parser reads empty cells to calculate depth. '2/ilgilendi' is at indent 0, while '1/sürekli' is at indent 1.
</div>

## Parsing Logic & Algorithm

The `FileReader.java` uses a depth-based reconstruction algorithm to parse these nodes.
1.  **Intermediate Parsing:** It reads the CSV line by line, counting empty strings to determine the `indent` integer.
2.  **Graph Construction:**
    * It iterates through the list of `IndentNodes`.
    * If `nextNode` indent is **+1**, a direct edge is added.
    * If `nextNode` indent is **<= current**, the algorithm backtracks to find the correct parent.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/java-class-structure.jpg" title="Java Class Structure" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/console-output.jpg" title="Console Output" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The Project Structure (AMRGraph, AMRNode, IndentNode). Right: The resulting adjacency list printed to the console.
</div>

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
