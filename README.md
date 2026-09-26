# <img src="RhinoUserTextDatabase/icon.ico" width="48" align="top" /> UserText DB

![Version](https://img.shields.io/badge/version-1.1.0_Beta-blue.svg)
![Platform](https://img.shields.io/badge/platform-Rhino_8-black.svg)
![Brand](https://img.shields.io/badge/by-Enzyme-4CAF50.svg)

**UserText DB** is a powerful, lightning-fast spreadsheet interface for managing Rhino User Text attributes. Built by [Enzyme APD](https://www.weareenzyme.com/), it replaces Rhino's native, one-object-at-a-time attribute panel with an interactive, Excel-style grid that makes handling metadata, BIM information, and model data effortless.

---

## 📖 WHY: Our Story & Light-BIM
At Enzyme, we have spent years experimenting with and refining the concept of **"Light-BIM"**. 

Our approach is heavily influenced by a 20-year legacy of working with Archicad. Inspired by our Grasshopper mentor [Ismael Sanz](https://www.linkedin.com/in/ismasanz/) and our resident computational wizard [Hendriko Teguh](https://www.linkedin.com/in/hteguh/), and their shared obsession with data-driven design workflows powered by Elefront, we’ve developed workflows that rely heavily on the key-value pairs of UserText in Rhino. 

Whether it is masterplanning, architectural design, or developing complex geometrical features, we leverage this data to enable computational workflows for geometry automation and data extraction. Our core philosophy is simple: **Minimal input, maximum output.**

Because we routinely integrate our Rhino models with highly developed BIM models—exchanging data bi-directionally—we needed a tool that could handle this massive flow of information efficiently. Rhino's native properties panel simply wasn't built for this scale. 

That is why we decided to design our own Rhino plugin: to multiply the usability of Rhino's native features and enable proper spreadsheet/database workflows with absolute ease.

---

## 🎯 WHAT: The Core Pitch
* **Stop Clicking, Start Typing:** The standard Rhino workflow requires selecting an object, opening properties, finding the UserText tab, and typing. UserText DB puts your entire model in an Excel-style grid. Navigate with arrow keys, hit `Enter` to edit, and breeze through data entry.
* **Bi-Directional Sync:** The data and the 3D model are one. Select a row in your database, and the geometry highlights in Rhino. Select objects in your viewport, and the grid instantly filters to show exactly what you've selected.
* **Error-Free Data:** Consistency is the hardest part of metadata. Our plugin automatically extracts unique values from your model and turns them into dropdown menus. Stop worrying about typos ruining your material schedules.
* **Massive Time Savings:** Need to assign "Approved" to 400 objects? The built-in Batch Editor does it in one click.

---

## 🛠️ HOW: Key Features

### ⚡ 1. The Live Data Grid
* **Excel-Style Editing:** A seamless tabular interface for all User Text Keys.
* **Keyboard Navigation:** Fully optimized for keyboard users—arrow keys to move, `Enter` to open an edit, `Enter` to close.
* **Custom Layouts:** Reorder, hide, and add columns exactly how you want to see them.
* **Smart Visibility Filtering:** Quick toggles to hide empty rows, or filter out hidden/locked geometry. By default, the grid only shows visible, unlocked objects (respecting layer states) to keep your workspace relevant.

### 🧠 2. Smart Automation & Batching
* **Auto-Populating Dropdowns:** Turn any column into a dropdown. The plugin automatically scans your entire Rhino file, finds every unique value used in that column, and builds your dropdown options for you.
* **Batch Editing:** Apply uniform data across massive selections instantly.

### 🎨 3. 3D Audit Mode
* **Live Color-Coding:** Select any metadata column (or Object Name/Type) to instantly color-code your entire Rhino viewport based on the data values.
* **Deep Block Support:** The custom display conduit is fully block-aware, recursively diving into nested instance definitions to accurately color inner geometry.

### 🗂 4. View States
* **What are States?** View States allow you to save the exact configuration of your Grid Settings—which columns are visible, their order, and what data you are focusing on—into a named profile.
* **Why are they useful?** When working on complex BIM models, you often need to switch contexts (e.g., viewing 'Structural' data vs 'Cost Estimation' data vs 'Phasing'). Instead of manually checking and unchecking 20 columns every time you change tasks, simply load a saved state to instantly snap your workspace into the exact column layout you need.

### 🔄 5. Excel & CSV Interoperability
* Export your entire Rhino model's metadata to a CSV with one click.
* Share the CSV with a project manager, edit it in Excel, and import it back. The plugin reads the changes and injects the new data straight into your Rhino geometry.

### ⚙️ 6. Sleek, Native Integration
* Switchable horizontal/vertical layouts to dock perfectly wherever you like in your Rhino workspace.
* Clean, minimalistic UI built on Eto.Forms.

---

## 🚀 BACKEND: Architecture & Performance (For Developers)
UserText DB is designed from the ground up to handle massive architectural models with tens of thousands of objects without bottlenecking Rhino's main thread.

- **UI Virtualization:** The plugin leverages Eto's `TreeGridView` data virtualization. Rather than instantiating a UI text box for every single cell (which would cause memory exhaustion with 10,000+ objects), the interface only draws the exact cells currently visible on your monitor.
- **Smart Sleep Mode:** To ensure Rhino remains completely buttery smooth, the plugin "goes to sleep" when the panel is hidden (e.g., when you click away to the Layers or Properties tab). It safely unsubscribes from heavy document tracking to ignore background modeling operations. When you bring the panel back into focus, it performs a single, fast bulk-refresh.
- **Event Throttling & Fast-Bypassing:** Dropdown updates and bulk layout changes use internal circuit breakers. This forces the UI to bypass its standard grid rebuilds when updating internal lists, preventing cascading UI events that would otherwise trigger dozens of heavy LINQ filtering queries per click.
- **Schema Persistence via Rhino Strings:** Your customized grid structures, empty column placeholders, dropdown options, and view states are seamlessly serialized into lightweight JSON and stored persistently in the `RhinoDoc.Strings` dictionary. This ensures your customized database schema inherently travels inside the `.3dm` file without requiring external databases.

---

## 🔍 SEARCH: Query Cheatsheet

Finding the right data shouldn't be hard. Our custom query engine understands human logic:

### Basic Search
Type any text into the filter box to instantly hide rows that don't contain your search string.
- *Example:* Typing `wood` will show only objects with "wood" in any column.

### Multi-Term Search
Separate words with commas to search for multiple terms at once (OR logic).
- *Example:* `timber, phase 6` instantly finds objects that have both.

### Exclusion (NOT)
Prefix a term with a minus `-` to hide rows containing that term.
- *Example:* `-phase 1` will hide any objects belonging to Phase 1.

### Column-Specific Search
Use `columnName:searchTerm` to restrict your search to a specific column.
- *Example:* `mat:wood` searches for "wood" only in the Material column (the column name check is partial, so `mat:` matches `Material`).

### Regular Expressions (Regex Mode)
Enable the `.*` toggle button next to the search bar to bypass standard text search and use pure Regular Expressions. This unlocks extreme power-user querying, allowing you to match complex string patterns, specific naming conventions, and exact data formats.

**Common BIM Regex Examples:**
- `^Wall` : Finds items that *start exactly* with "Wall" (e.g., matches "Wall_Interior", but skips "CurtainWall").
- `Floor|Roof` : The pipe `|` acts as an OR operator. Finds items containing either "Floor" OR "Roof".
- `\d+` : Finds any cell containing numbers (e.g., "Level 1", "Phase 3").
- `^Level [1-5]$` : Finds exact matches for "Level 1" through "Level 5", ignoring "Level 10".
- `(?i)concrete` : Case-insensitive search. Finds "Concrete", "CONCRETE", or "concrete".

*Want to master Regex? Check out the [RexEgg Quick Start Guide](https://www.rexegg.com/regex-quickstart.php) for a comprehensive cheat sheet, or use [Regex101](https://regex101.com/) if you want an interactive tool to test your patterns.*

---
*Created by [Enzyme APD](https://www.weareenzyme.com/)*

---

## 🚀 Beta Testing Installation

To help us beta test the plugin, you can install the latest release manually:

1. Download the latest `.yak` file from the [release folder](release/). *(Click the `.yak` file, then click the "Download raw file" button).*
2. Open Rhino 8.
3. Open a file explorer and simply **Drag and Drop** the downloaded `.yak` file directly into the open Rhino 8 window.
4. Restart Rhino to complete the installation.
