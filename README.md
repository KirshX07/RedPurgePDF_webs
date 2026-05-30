# 🩸 RedPurge PDF - Digital Forensics & Sanitization Engine

```
   ____          _ ____                     ____  ____  _____ 
  / __ \___  ___| |  _ \ _   _ _ __ __ _  |  _ \|  _ \|  ___|
 / /_/ / _ \/ _ \ | |_) | | | | '__/ _` | | |_) | | | | |_   
/ _, _/  __/  __/ |  __/| |_| | | | (_| | |  __/| |_| |  _|  
/_/ |_|\___|\___|_|_|    \__,_|_|  \__, | |_|   |____/|_|    
                                   |___/                    
  [ v1.0.0 ] [ MEMORY-BOUND FORENSICS ] [ ZERO-RETENTION LABS ]
```

**RedPurge PDF** is a high-performance, professional-grade digital forensics utility and metadata sanitization engine architected specifically to purge tracking indicators, software footprints, and hidden tracking matrices from PDF documents. 

Designed for sensitive environments, it operates completely in-memory utilizing serverless stream structures to ensure zero disk-write caching, fulfilling strict **Zero-Retention security standards**.

**Main Point** A powerful, low-memory footprint anti-forensics web application built with Python and Streamlit to detect, analyze, and sanitize hidden metadata leaks (XMP and Info Dictionary) from PDF files permanently.

## 🚀 Live Demo
Access the deployed application here: **[https://redpurge-pdf.streamlit.app](https://redpurge-pdf.streamlit.app)**
---

## 🎓 Academic Credentials

This application has been engineered as a core demonstration utility for undergraduate thesis evaluation:

* **Operator Name:** Kirana Shofa Dzakiyyah
* **NIM:** 25051204358
* **Program:** S1 Teknik Informatika
* **Institution:** Universitas Negeri Surabaya (UNESA)

---

## 🛡️ Core Security & Forensic Capabilities

### 1. Cryptographic Chain of Custody
Upon ingestion, the engine immediately computes a unique **SHA-256 checksum** of the document, establishing an immutable cryptographic anchor. Post-purging, a second SHA-256 is generated and compared to mathematically demonstrate structural modification.

### 2. Complete Prevention of Incremental Write Rollbacks
> [!WARNING]
> Standard PDF editors often save changes via *incremental writing*, simply appending new object references while leaving old deleted data streams intact in the binary layout.

RedPurge PDF **prevents malicious rollbacks** by reconstructing the entire PDF from scratch. The visual content streams of each page are cleanly cloned into a brand-new `pypdf.PdfWriter` compiler instance, leaving all revision histories and historical deleted blocks completely behind.

### 3. Deep Page-Level Cleansing
Beyond standard document-level dictionaries (`/Author`, `/Creator`, `/Producer`, `/CreationDate`, `/ModDate`), RedPurge scans and pop-scrubs private data objects within individual pages and annotation streams, targeting:
* `/PieceInfo` (vendor-specific private application footprints)
* Page-level `/Metadata` XML streams
* Structural `/StructParents` tracking arrays

### 4. Zero-Retention Memory Architecture
* **In-Memory Buffers**: Uses standard `io.BytesIO` arrays to read, decrypt, parse, sanitize, and write PDFs purely inside RAM.
* **100% In-Memory ZIP Compilation**: Multi-file batches are packed into a ZIP archive directly within memory using Python's `zipfile` module, serving raw bytes directly to download triggers without ever cacheing temporary files on disk.
* **Proactive RAM Telemetry**: Incorporates process memory mapping (`psutil`) to display live RSS diagnostics in the control dashboard, proving that resources are successfully garbage-collected (`gc.collect()`) upon workspace reset.

### 5. Boundary Value Analysis (BVA) & Defensive Input
* Gracefully restricts single uploads to **100MB** using native Streamlit configuration triggers.
* Implements robust, insulated error handling (`pypdf.errors.PdfReadError`, encryption locks, or truncated arrays), catching failures gracefully and outputting human-readable warnings inside the terminal instead of crashing.

---

## ⚙️ Project File Map

```
d:\RedPurgePDF_web/
├── .streamlit/
│   └── config.toml           # Streamlit server limits & custom theme variables
├── app.py                     # Presentation Layer, Live Telemetry & Pandas Styler
├── engine.py                  # Forensics Engine, Cryptography & Sanitization Backend
└── requirements.txt           # Dependency Manifest
```

---

## 🚀 Installation & Local Execution

Ensure you have **Python 3.10+** installed on your system.

### 1. Clone or Extract the Workspace
Navigate to the project root:
```bash
cd d:\RedPurgePDF_web
```

### 2. Install Forensic Dependencies
RedPurge utilizes modern, highly optimized libraries to process PDF binaries:
```bash
pip install -r requirements.txt
```

### 3. Launch the Control Panel
Fire up the local host web server using Streamlit:
```bash
streamlit run app.py
```
The browser will automatically open the dashboard at `http://localhost:8501`.

---

## 🔬 Forensic Verification Test Suite
A local test harness is provided to run structural sanitization checks:
```bash
python C:\Users\kiran\.gemini\antigravity\brain\334a09c2-98b7-40d5-9cfa-e0b7f5579647\scratch\test_engine.py
```
This script compiles a mock metadata-heavy PDF stream, decrypts it, strips all PieceInfo keys, performs a complete rebuild, and audits the result back to verify the eradication status.

---

## 🩸 Theme Palette Reference
Designed to wow reviewers with a modern, high-tech cybersecurity tool vibe:
* **Background:** Deep Pure Black (`#0D0D0D`)
* **Accents & Glowing Borders:** Neon Crimson Red (`#D90429`)
* **Containers & Cards:** Charcoal Gray (`#1A1A24`)
* **Typography Headers:** Crisp White (`#EDF2F4`)
* **Descriptions / Telemetry:** Cyber Gray (`#8D99AE`)
