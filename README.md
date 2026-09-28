<p align="center">
  <img src="images/talos_logo.png" alt="TALOS AI4SSH logo" width="220">
</p>

<h1 align="center">TALOS RDF Graph Viewer</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3-blue.svg" alt="Python 3">
  <img src="https://img.shields.io/badge/backend-Flask-black.svg" alt="Flask">
  <img src="https://img.shields.io/badge/RDF-RDFLib-orange.svg" alt="RDFLib">
  <img src="https://img.shields.io/badge/visualization-PyVis-green.svg" alt="PyVis">
  <img src="https://img.shields.io/badge/query-SPARQL-purple.svg" alt="SPARQL">
</p>

The **TALOS RDF Graph Viewer** is a Python application with a browser-based interface for visualizing, exploring, and querying RDF graphs.

Developed for the [TALOS AI4SSH Lab](https://www.talos-lab.eu/), the application supports research in **Digital Humanities**, **Knowledge Representation**, and **AI for the Social Sciences and Humanities (AI4SSH)**. It includes OTV-aware labeling for exploring ontoterminologies, including data produced with the TEDI environment.

Users can upload an RDF file, inspect its metadata and statistics, select properties to visualize, explore an interactive network, and execute SPARQL queries against the uploaded graph.

The application runs through a local Flask server. No frontend framework or JavaScript build step is required.

---

## Features

- **RDF/XML, Turtle, and JSON-LD input**
- **Interactive, directed graph visualization**
- **Property selection and filtering**
- **Graph statistics and metadata inspection**
- **Dublin Core metadata from ontology declarations**
- **Namespace inspection for RDF/XML files**
- **OTV-aware node labels and tooltips**
- **Case-insensitive search with wildcard support**
- **Draggable nodes and adjustable graph layout**
- **Freeze and unfreeze controls**
- **Removal of nodes from the current visualization**
- **Built-in SPARQL query interface with examples**

---

## Supported Formats

The parser is selected from the uploaded file's extension.

| Format | File extensions |
| --- | --- |
| RDF/XML | `.rdf`, `.xml` |
| Turtle | `.ttl` |
| JSON-LD | `.jsonld` |

Use the extension corresponding to the file's actual serialization.

---

## Getting Started

### Requirements

- Python 3 with `pip`.
- A modern web browser.
- Flask, RDFLib, and PyVis.

The supplied documentation identifies Python 3.12 as the development version. Dependency versions are not pinned in the supplied application.

### Install dependencies

From the directory containing `Talos_RDF_Viewer.py`, run:

```bash
python -m pip install flask rdflib pyvis
```

For an isolated installation, create a virtual environment first:

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.\.venv\Scripts\Activate.ps1
```

Or on macOS and Linux:

```bash
source .venv/bin/activate
```

Then install the dependencies using the command above.

### Launch

```bash
python Talos_RDF_Viewer.py
```

The application starts a local server and attempts to open your default browser at:

```text
http://127.0.0.1:5000
```

If the browser does not open automatically, visit this address manually.

Keep the terminal running while using the application. Press `Ctrl+C` to stop the server.

> On systems where Python is invoked as `python3`, replace `python` with `python3` in the commands above.

---

## Usage

### 1. Upload a graph

Click **Select RDF File**, choose a supported file, and select **Upload and Analyze**.

After loading the file, the application provides access to:

- **Select Properties**
- **View Graph**
- **SPARQL Endpoint**
- **Show Metadata**

### 2. Inspect metadata

Select **Show Metadata** to inspect:

- Total number of triples.
- Counts of distinct properties in the application's categories.
- Dublin Core metadata associated with an `owl:Ontology` resource.
- Namespace declarations extracted from the RDF/XML header.

Dublin Core extraction currently covers the `http://purl.org/dc/elements/1.1/` vocabulary and the first ontology resource found. It does not collect all `dcterms:` metadata.

Namespace inspection is primarily implemented for RDF/XML; Turtle and JSON-LD namespace information may not appear in this panel.

### 3. Select properties

Choose **Select Properties** to control which predicates appear in the visualization.

The application groups properties using the observed triples:

| Category | Classification |
| --- | --- |
| Object properties | Predicates used with URI-reference objects |
| Annotation properties | Predicates with non-URI objects whose URI contains `label` or `comment` |
| Data properties | Remaining predicates with non-URI objects |

These categories are practical interface groupings, not a complete interpretation of OWL property declarations. A predicate used in different ways can appear in more than one category.

Select individual properties or use the category selection buttons, then click **Generate Graph**.

For larger datasets, begin with a small set of relevant properties.

### 4. Explore the graph

The visualization displays directed relationships between resources, with labels and colors distinguishing predicates.

Available controls include:

| Control | Action |
| --- | --- |
| **Search** | Find and highlight matching nodes |
| **Reset** | Reload the visualization |
| **Freeze** | Toggle automatic layout physics |
| **Delete node** | Remove one selected node and its connected edges from the displayed network |

Nodes can be dragged to adjust the layout. With **Freeze (ON)**, physics is disabled while manual positioning remains available.

Deleting a node affects the current visualization only. It does not modify the uploaded RDF file.

---

## Labels and Colors

### Node labels

Resource labels are selected in this order:

1. `otv:shortConceptName`
2. `rdfs:label`
3. The final portion of the resource URI

The recognized OTV namespace is:

```text
http://www.ontologia.fr/OTB/otv#
```

Labels longer than 35 characters are shortened to their first and last 15 characters, separated by an ellipsis.

Resource tooltips include the full URI and `otv:conceptName`, where available.

### Node colors

Colors reflect the selected relationships rather than fixed ontology classes.

| Appearance | Meaning |
| --- | --- |
| Sky blue | URI resources appearing as subjects but not objects |
| Light salmon | URI resources appearing as objects but not subjects |
| Pale blue | Other resource nodes, including intermediate resources |
| Gray boxes | Non-URI object values |

Edges are colored by predicate using a repeating palette. Their labels show a shortened predicate name, while tooltips show the full URI.

---

## Search

Search checks node labels and tooltip text, including resource URIs and available concept names.

- Matching is case-insensitive.
- `*` is converted into a wildcard matching any sequence of characters.
- Matching nodes are highlighted and selected.
- The view adjusts to include the matches.

For example:

```text
krater
```

Finds nodes containing `krater` in their label or tooltip.

```text
Greek*pottery
```

Finds text containing `Greek` followed by `pottery`, with any intervening characters.

The current implementation interprets other regular-expression characters as well; search is not strictly literal.

---

## SPARQL Queries

Select **SPARQL Endpoint** to open the query interface in a new tab.

Queries run through RDFLib against the uploaded graph. The interface includes example queries and displays variable bindings in a table.

For example, inspect up to 100 triples:

```sparql
SELECT ?subject ?predicate ?object
WHERE {
  ?subject ?predicate ?object .
}
LIMIT 100
```

Count the triples:

```sparql
SELECT (COUNT(*) AS ?tripleCount)
WHERE {
  ?subject ?predicate ?object .
}
```

The results interface is designed around tabular `SELECT` queries. It should not be treated as a complete SPARQL protocol service or a replacement for a production triplestore.

---

## Architecture

The supplied application is contained in `Talos_RDF_Viewer.py`, including its Flask routes, HTML templates, styles, and browser-side controls.

| Component | Role |
| --- | --- |
| **Flask** | Local web server, upload handling, and page rendering |
| **RDFLib** | RDF parsing, graph inspection, and SPARQL execution |
| **PyVis** | Interactive network generation |
| **JavaScript** | Search, layout controls, and visual node removal |
| **Temporary storage** | Uploaded files and generated visualization output |

The main application routes are:

| Route | Purpose |
| --- | --- |
| `/` | File selection page |
| `/upload` | File upload and initial analysis |
| `/select` | Property selection |
| `/view` | Graph visualization |
| `/sparql` | Query interface |

---

## Data Handling and Deployment

Uploaded files are sent to the running Flask process and stored in a temporary directory. When running locally, this processing takes place on your computer.

The application registers cleanup of uploaded temporary files at normal shutdown. Cleanup is not guaranteed after an abrupt termination, and generated visualization output may remain in the system temporary directory.

Some visualization assets or RDF operations may require network access. Do not assume fully offline operation.

The supplied launch configuration is intended for local use. Public or multi-user hosting requires additional deployment and security work, including access controls, upload limits, query restrictions, and isolation of generated output.

Because the application requires a Python backend, GitHub Pages cannot run the viewer itself.

---

## Troubleshooting

### Missing Python module

Install the dependencies using the same Python interpreter used to launch the application:

```bash
python -m pip install flask rdflib pyvis
```

### Browser does not open

Visit `http://127.0.0.1:5000` manually and check the terminal for errors.

### Port 5000 is already in use

Change the port in both:

- The URL inside `open_browser()`.
- The `app.run(port=5000, debug=False)` call.

Restart the application and open the updated address.

### Graph generation is slow

Select fewer properties or use a smaller dataset. Rendering all triples may produce a dense graph and require substantial processing.

### Metadata is missing

Confirm that the graph contains an `owl:Ontology` declaration and the supported `dc:` properties. Namespace extraction is primarily designed for RDF/XML.

### File upload shows zero statistics

Inspect the terminal output and verify the file's syntax and extension. In the current implementation, parsing errors during initial analysis can still lead to the upload-success page with zero statistics.

---

## Documentation

See the [Installation and Usage Guide](TALOS_RDF_Viewer_Documentation.pdf) for illustrated workflows and examples.

The supplied guide is dated **17 August 2025**; the Python source header is dated **23 August 2025**. Where their descriptions differ, this README follows the supplied source code.

---

## Help

To ask a question, report a problem, or suggest an improvement, open an issue in this repository or contact the [TALOS AI4SSH Lab](https://www.talos-lab.eu/).

For bug reports, include:

- Your operating system and Python version.
- The command used to launch the application.
- Steps to reproduce the problem.
- Relevant terminal or browser-console errors.
- A minimal, non-sensitive example file, where possible.

---

## Contribution

Contributions are welcome. Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in this project shall be licensed under the Apache License, Version 2.0, without any additional terms or conditions.

---

## License

This project is licensed under the [Apache License, Version 2.0](LICENSE).

---

## Developer

Developed by **[Christophe Roche](https://github.com/Christophe-Roche)** for the [TALOS AI4SSH Lab](https://www.talos-lab.eu/).
