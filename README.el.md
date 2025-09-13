# TALOS Εφαρμογή Οπτικοποίησης RDF Γραφημάτων

[![Python](https://img.shields.io/badge/Python-3.8%2B-informational.svg)](#-εκτέλεση)
[![Flask](https://img.shields.io/badge/Flask-3.x-lightgrey.svg)](#-εκτέλεση)
[![RDFlib](https://img.shields.io/badge/RDFlib-6.x-lightgrey.svg)](#-εκτέλεση)
[![PyVis](https://img.shields.io/badge/PyVis-0.3.x-lightgrey.svg)](#-εκτέλεση)

Διαθέσιμες γλώσσες: [English](README.md) | [Ελληνικά](README.el.md)

---

Αυτό το αποθετήριο παρέχει μια ελαφριά, βασισμένη σε φυλλομετρητή εφαρμογή για την οπτικοποίηση και εξερεύνηση RDF γραφημάτων.

---

## 📂 Περιεχόμενα

Το αποθετήριο περιλαμβάνει:

- `Talos_RDF_Viewer.py` — ο πλήρης πηγαίος κώδικας (όλα-σε-ένα εφαρμογή)  
- `TALOS_RDF_Viewer_Documentation.pdf` — τεκμηρίωση και οδηγίες χρήσης  

---

## Επισκόπηση

Η **TALOS Εφαρμογή Οπτικοποίησης RDF Γραφημάτων** είναι μια διαλειτουργική web εφαρμογή σε Python για τη **διαδραστική εξερεύνηση RDF γραφημάτων**. Σας επιτρέπει να:

- ανεβάζετε RDF αρχεία (`.rdf`, `.xml`, `.ttl`, `.jsonld`),
- ελέγχετε **στατιστικά γραφήματος**, **Dublin Core** μεταδεδομένα (από `owl:Ontology`) και **δηλωμένα namespaces**,
- επιλέγετε ποιες **ιδιότητες** θα οπτικοποιηθούν (object / data / annotation),
- δημιουργείτε ένα **διαδραστικό γράφημα** (μετακίνηση κόμβων, πάγωμα, αναζήτηση, διαγραφή κόμβων),
- υποβάλλετε ερωτήματα μέσω ενσωματωμένου **SPARQL endpoint**.

Έχει σχεδιαστεί για **ερευνητές, εκπαιδευτικούς και προγραμματιστές**, και είναι ιδιαίτερα χρήσιμο για **ορολογίες** που έχουν δημιουργηθεί με το περιβάλλον [TEDI](https://ontoterminology.com/tedi).

---

## Χαρακτηριστικά

- **Υποστήριξη πολλαπλών μορφών:** RDF/XML, Turtle, JSON-LD  
- **Αυτόματη εξαγωγή:** αριθμός τριπλετών, τύποι ιδιοτήτων, Dublin Core (από `owl:Ontology`), δηλωμένα namespaces  
- **Επιλογέας ιδιοτήτων:** object, data, annotation (με ομαδική επιλογή/αποεπιλογή)  
- **Προβολή γραφήματος** (PyVis):  
  - προτεραιότητα ετικετών κόμβων: `otv:shortConceptName` → `rdfs:label` → τμήμα URI  
  - tooltips με `otv:conceptName` + πλήρες URI  
  - χρωματική διάκριση κόμβων: root / terminal / ενδιάμεσοι / literals  
  - αναζήτηση με `*` wildcard, χωρίς διάκριση πεζών/κεφαλαίων, με αυτόματο ζουμ + επισήμανση  
  - εναλλαγή (Freeze ON/OFF), reset, διαγραφή επιλεγμένου κόμβου  
- **SPARQL endpoint:** εκτέλεση ερωτημάτων, έτοιμα παραδείγματα  
- **Responsive περιβάλλον:** σύγχρονος, καθαρός και προσβάσιμος σχεδιασμός  

---

## Εκτέλεση

```bash
# 1) Βεβαιωθείτε ότι έχετε Python 3.8+
python --version

# 2) Εγκατάσταση εξαρτήσεων
pip install flask rdflib pyvis

# 3) Εκκίνηση εφαρμογής
python Talos_RDF_Viewer.py

# 4) Άνοιγμα στον φυλλομετρητή (ανοίγει αυτόματα)
# http://127.0.0.1:5000
```

---
## Συγγραφέας

Καθ. Christophe Roche — TALOS ERA Chair Holder — Πανεπιστήμιο Κρήτης

📧 roche.university@gmail.com

🌐 https://talos-ai4ssh.uoc.gr/

---

## Αναφορά

Για γενική αναφορά στο έργο:

> Roche, C. (2025). TALOS RDF Graph Viewer (Έκδοση 1.0).
> TALOS AI4SSH Project, Πανεπιστήμιο Κρήτης.
> https://talos-ai4ssh.uoc.gr/

---

## Άδεια

Όλος ο κώδικας διανέμεται με άδεια Creative Commons Attribution–NonCommercial (CC BY-NC 4.0).
Μπορείτε να κοινοποιήσετε και να αναδιανείμετε το υλικό υπό τις ακόλουθες προϋποθέσεις:

> BY: Πρέπει να αποδίδεται αναφορά στον δημιουργό.

> NC: Επιτρέπεται μόνο μη-εμπορική χρήση.

Περισσότερες πληροφορίες: https://creativecommons.org/licenses/by-nc/4.0/

---

## Περισσότερες Πληροφορίες

Ιστότοπος TALOS RDF Graph Viewer: [talos-ai4ssh.eu/RDF_Viewer](http://talos-ai4ssh.eu/RDF_Viewer/)

Ιστότοπος Έργου TALOS: [talos-ai4ssh.uoc.gr](https://talos-ai4ssh.uoc.gr)

---
