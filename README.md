# TALOS RDF Graph Viewer

[![Python](https://img.shields.io/badge/Python-3.8%2B-informational.svg)](#-%EF%B8%8F-system-requirements)
[![Flask](https://img.shields.io/badge/Flask-3.x-lightgrey.svg)](#-installation)
[![RDFlib](https://img.shields.io/badge/RDFlib-6.x-lightgrey.svg)](#-installation)
[![PyVis](https://img.shields.io/badge/PyVis-0.3.x-lightgrey.svg)](#-installation)

Available languages: [English](README.md) | [Ελληνικά](README.el.md)

---

This repository provides a lightweight, browser-based application for visualizing and exploring RDF graphs.

---

## 📂 Contents

This repository contains:

- `Talos_RDF_Viewer.py` — the complete source code (all-in-one application)  
- `TALOS_RDF_Viewer_Documentation.pdf` — documentation and usage instructions  

---

## Overview

The **TALOS RDF Graph Viewer** is a cross-platform, Python web app for **interactive RDF exploration**. It lets you:

- Upload RDF datasets (`.rdf`, `.xml`, `.ttl`, `.jsonld`)
- Inspect **graph statistics**, **Dublin Core** metadata (from `owl:Ontology`), and **declared namespaces**
- Select which **properties** to visualize (object / data / annotation)
- Generate an **interactive graph** (drag, freeze physics, search with wildcards, delete nodes)
- Query data via a **built-in SPARQL endpoint**

It is designed for **researchers, educators, and developers** and is particularly convenient for **ontoterminologies** built with the [TEDI environment](https://ontoterminology.com/tedi).

---

## Features

- **Multi-format upload:** RDF/XML, Turtle, JSON-LD  
- **Auto-extraction:** triples count, property types, Dublin Core (from `owl:Ontology`), declared namespaces  
- **Property selector:** object, data, annotation (with bulk select/deselect)  
- **Graph viewer** (PyVis):  
  - Node labeling priority: `otv:shortConceptName` → `rdfs:label` → URI fragment  
  - Tooltips with `otv:conceptName` + full URI  
  - Node coloring by role: root / terminal / intermediate / literal  
  - Search with `*` wildcard, case-insensitive; auto-focus + highlighting  
  - Physics toggle (Freeze ON/OFF), reset, delete selected node  
- **SPARQL endpoint:** execute queries; ready-made examples  
- **Responsive UI:** modern, accessible, clean design  

---

## Run

```bash
# 1) Ensure Python 3.8+ is installed
python --version

# 2) Install dependencies
pip install flask rdflib pyvis

# 3) Run the app
python Talos_RDF_Viewer.py

# 4) Open in your browser (opens automatically)
# http://127.0.0.1:5000
```

---

## Author

Prof. Christophe Roche — TALOS ERA Chair Holder — University of Crete

📧 roche.university@gmail.com

🌐 https://talos-ai4ssh.uoc.gr/

---

## Citation  

For general reference to the project:  
> Roche, C. (2025). *TALOS RDF Graph Viewer* (Version 1.0).  
> TALOS AI4SSH Project, University of Crete.  
> https://talos-ai4ssh.uoc.gr/

---

## License

All the code is distributed under the **Creative Commons Attribution–NonCommercial (CC BY-NC 4.0)** license.  
You are free to **share and redistribute** the material under the following conditions:  
- **BY**: Credit must be given to the creator(s).  
- **NC**: Only non-commercial uses are permitted.

More info: https://creativecommons.org/licenses/by-nc/4.0/
 
---

## More Information

- TALOS RDF Graph Viewer Website: [talos-ai4ssh.eu/RDF_Viewer](http://talos-ai4ssh.eu/RDF_Viewer/)
- TALOS Project Website: [talos-ai4ssh.uoc.gr](https://talos-ai4ssh.uoc.gr)  

---
