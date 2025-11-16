# BloodHound Cheatsheet

> A quick and clear guide for installing, using, and understanding the BloodHound Cheatsheet.

<details>
<summary><strong>📘 Table of Contents</strong></summary>

* [Overview](#overview)
* [Features](#features)
* [Requirements](#requirements)
* [Installation](#installation)
* [How to Use](#how-to-use)

  * [1. Running BloodHound](#1-running-bloodhound)
  * [2. Uploading Data](#2-uploading-data)
  * [3. Using the Cheatsheet](#3-using-the-cheatsheet)
* [Tips](#tips)
* [Disclaimer](#disclaimer)

</details>

---

## Overview

The **BloodHound Cheatsheet** is a structured reference that helps users quickly look up common BloodHound queries, key attack paths, and common analysis patterns. It acts as a companion to the BloodHound tool, helping beginners and advanced users speed up their Active Directory enumeration workflow.

---

## Features

* Ready-made queries for common AD attack paths
* Clear explanations to help understand each query
* Organized categories for easier navigation
* Works offline as a static reference

---

## Requirements

Before using the cheatsheet, make sure you have:

* **BloodHound** installed
* **Neo4j** running
* Any **collection method** prepared (e.g., SharpHound, Python ingestors)

---

## Installation

Here is a clear guide for installing **BloodHound** from scratch on a fresh system.

### **1. Install Neo4j (Required Database for BloodHound)**

1. Download Neo4j Community Edition from the official site.
2. Install it on your system.
3. Run Neo4j:

```bash
neo4j console
```

4. Open your browser and go to:

```
http://localhost:7474
```

5. Set a new password when prompted.

### **2. Install BloodHound**

You can install BloodHound by downloading the latest release.

**For Linux:**

```bash
sudo apt update
sudo apt install bloodhound
```

**For Windows / Manual Download:**

1. Go to the BloodHound GitHub release page.
2. Download the latest BloodHound ZIP.
3. Extract it.
4. Run:

```
BloodHound.exe
```

### **3. Install a Data Collector (SharpHound / Python Ingestor)**

#### **Windows (SharpHound.exe)**

1. Download SharpHound from the BloodHound repository.
2. Place it on the target machine.

Run it:

```bash
SharpHound.exe -c All
```

#### **Linux (Python ingestor)**

```bash
pip install bloodhound
python3 bloodhound.py -d domain.local -u user -p pass --zip
```

---

## How to Use

### 1. Running BloodHound

1. Start Neo4j:

```bash
neo4j console
```

2. Open BloodHound:

```bash
bloodhound
```

3. Log in using your Neo4j username and password.

### 2. Uploading Data

Collect data using SharpHound:

```bash
SharpHound.exe -c All
```

Or the Python ingestor:

```bash
python3 bloodhound.py -d domain.local -u user -p pass --zip
```

Then upload the ZIP file into BloodHound.

### 3. Using the Cheatsheet

Inside this repository, open:

```
/cheatsheet/queries.md
```

This file contains:

* Common queries
* Privilege escalation paths
* Lateral movement helpers
* Interpretation notes

You can copy any query and paste it directly into the **BloodHound Query Bar**.

---

## Tips

* Always validate your attack path; BloodHound sometimes suggests paths that need extra checks.
* Update your SharpHound version to avoid inaccurate edges.
* Combine the cheatsheet with real-time AD enumeration for better accuracy.

---

## Disclaimer

This cheatsheet is for **educational and security auditing purposes only**. Use it responsibly and only on systems you have explicit permission to test.

---

Enjoy exploring AD the smart way.
