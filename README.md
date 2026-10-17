# <img src="RhinoUserTextDatabase/icon.ico" width="48" align="top" /> UserText DB

![Version](https://img.shields.io/badge/version-1.1.48_Beta-blue.svg)
![Platform](https://img.shields.io/badge/platform-Rhino_8_(Windows_%7C_Mac)-black.svg)
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
<video src="Resources/MP4/SHOW%20SELECTED.mp4" width="100%" autoplay loop muted playsinline></video>
* **Bi-Directional Sync:** The data and the 3D model are one. Select a row in your database, and the geometry highlights in Rhino. Select objects in your viewport, and the grid instantly filters to show exactly what you've selected.
* **Error-Free Data:** Consistency is the hardest part of metadata. Our plugin automatically extracts unique values from your model and turns them into dropdown menus. Stop worrying about typos ruining your material schedules.
<video src="Resources/MP4/SELECT%20BY%20KEY.mp4" width="100%" autoplay loop muted playsinline></video>
* **Massive Time Savings:** Need to assign "Approved" to 400 objects? The built-in Batch Editor does it in one click.

---

## 🛠️ HOW: Key Features

### ⚡ 1. The Live Data Grid
<video src="Resources/MP4/GRID%20NEW%20COLUMN.mp4" width="100%" autoplay loop muted playsinline></video>

* **Excel-Style Editing:** A seamless tabular interface for all User Text Keys.
* **Keyboard Navigation:** Fully optimized for keyboard users—arrow keys to move, `Enter` to open an edit, `Enter` to close.
* **Custom Layouts:**
<video src="Resources/MP4/GROUP%20BY.mp4" width="100%" autoplay loop muted playsinline></video>
 Reorder, hide, and add columns exactly how you want to see them.
* **Natural Sorting:** Sort By and grouping treat numbers as numbers (`9` before `10`, `Level 2` before `Level 10`); decimal commas like `12,5` are understood, and empty values go last.
* **Formula Values:** Values written as Rhino text fields (e.g. `%<Area("…")>%`) show their result. The formula is kept unless you type a new value, and CSV export keeps the formula text.
* **Fits Any Panel Size:** The settings tabs scroll on their own and the grid always keeps room for itself, so the panel stays usable when docked narrow or floating small.
* **Smart Visibility Filtering:** Quick toggles to hide empty rows, or filter out hidden/locked geometry. By default, the grid only shows visible, unlocked objects (respecting layer states) to keep your workspace relevant.

### 🧠 2. Smart Automation & Batching
<video src="Resources/MP4/BATCH%20DATA.mp4" width="100%" autoplay loop muted playsinline></video>

* **Auto-Populating Dropdowns:** Turn any column into a dropdown. The plugin automatically scans your entire Rhino file, finds every unique value used in that column, and builds your dropdown options for you.
* **Batch Editing:** Apply uniform data across massive selections instantly.
* **One Undo per Action:** Every cell edit, batch edit, column rename, column delete and CSV import is a single `Ctrl+Z` in Rhino.
* **Safe Column Rename & Delete:** Renaming a key (Grid Settings → Key Name) only moves values from objects that have the old key, and never overwrites a value that already exists under the new name — any conflicts are reported and left untouched. Deleting a column removes that key from every object, after confirmation.

### 📐 2b. Calculated Columns & Group Totals
* **Calculated columns** — `@Layer`, `@Block`, `@Area`, `@Volume`, `@Length` and `@Base Z` — are read straight from the geometry. They are hidden by default: tick **Visible** in *Grid Settings* to show them. Values are in model units and include the contents of blocks (nested too); closed flat curves (plots, footprints) and hatches report the area they enclose. They work like any other column for sorting, grouping, Select By, 3D Audit and CSV export, but are read-only.
* **Group totals:** in *Grid Settings*, set a column's **Group Total** to Sum, Average, Min, Max or Count. When the grid is grouped, each group row shows that summary — e.g. group by `Use` with `@Area` set to Sum to get the floor area per use. `@Area`, `@Volume` and `@Length` sum by default.

### 🎨 3. 3D Audit Mode
<video src="Resources/MP4/3D%20AUDIT.mp4" width="100%" autoplay loop muted playsinline></video>

* **Live Color-Coding:** Select any metadata column (or Object Name/Type) to instantly color-code your entire Rhino viewport based on the data values.
* **Consistent Colours & Legend:** Each value keeps the same colour across sessions and files (20-colour palette). Numeric columns with many values use a blue-to-red gradient. A legend with object counts is drawn in the viewport.
* **Deep Block Support:** The custom display conduit is fully block-aware, recursively diving into nested instance definitions to accurately color inner geometry.

### 🗂 4. View States
<video src="Resources/MP4/GRID%20SETTINGS.mp4" width="100%" autoplay loop muted playsinline></video>

* **What are States?** View States allow you to save the exact configuration of your Grid Settings—which columns are visible, their order, and what data you are focusing on—into a named profile.
* **Why are they useful?** When working on complex BIM models, you often need to switch contexts (e.g., viewing 'Structural' data vs 'Cost Estimation' data vs 'Phasing'). Instead of manually checking and unchecking 20 columns every time you change tasks, simply load a saved state to instantly snap your workspace into the exact column layout you need.

### 🔄 5. Excel & CSV Interoperability
* Export your entire Rhino model's metadata to a CSV with one click.
* Share the CSV with a project manager, edit it in Excel, and import it back. The plugin reads the changes and injects the new data straight into your Rhino geometry.
* **Excel-friendly files:** exported CSVs are UTF-8 (accents like `ñ` survive) and use your computer's list separator, so they open correctly in Excel in any language (`;` in Spanish/European Excel, `,` elsewhere). Imports accept `,`, `;` or tab.
* **How import works:**
  * Rows are matched to objects by the `ObjectId` column, which must be kept.
  * Columns are matched by **header name**, so you can reorder or remove columns in Excel.
  * An **empty cell removes that key** from the object (same as clearing it in the grid). Remove a column entirely if you don't want to touch that key.
  * Changes to the `Name` column rename objects; `Type` is read-only and ignored.
  * New column headers become new keys. A summary shows how many objects changed and how many rows didn't match an object in the file.

### ⚙️ 6. Sleek, Native Integration
* Switchable horizontal/vertical layouts to dock perfectly wherever you like in your Rhino workspace.
* Clean, minimalistic UI built on Eto.Forms.

---

## 🚀 BACKEND: Architecture & Performance (For Developers)
UserText DB is designed from the ground up to handle massive architectural models with tens of thousands of objects without bottlenecking Rhino's main thread.

- **UI Virtualization:** The plugin leverages Eto's `TreeGridView` data virtualization. Rather than instantiating a UI text box for every single cell (which would cause memory exhaustion with 10,000+ objects), the interface only draws the exact cells currently visible on your monitor.
- **In-Memory Index:** Each object's user text is cached once and looked up by object Id, so filtering, sorting and grouping never go back to the Rhino document per cell.
- **Batched Writes:** Edits are written with `ObjectTable.ModifyAttributes` inside a single undo record, and the panel ignores the document events its own writes generate — editing 1,000 objects refreshes the grid once, not thousands of times.
- **Idle-Time Sync:** Changes made anywhere in Rhino (Properties panel, `SetUserText`, undo/redo, paste, import, layer visibility/lock) are queued and applied in one pass when Rhino is idle. While the panel is hidden the queue is kept and applied when you return.
- **Event Throttling & Fast-Bypassing:** Dropdown updates and bulk layout changes use internal circuit breakers. This forces the UI to bypass its standard grid rebuilds when updating internal lists, preventing cascading UI events that would otherwise trigger dozens of heavy LINQ filtering queries per click.
- **Cached 3D Audit:** Audit geometry (including nested blocks) is meshed and cached once, not rebuilt every frame. Objects that can't be meshed are left visible instead of disappearing.
- **Schema Persistence via Rhino Strings:** Your customized grid structures, empty column placeholders, dropdown options, and view states are seamlessly serialized into lightweight JSON and stored persistently in the `RhinoDoc.Strings` dictionary. This ensures your customized database schema inherently travels inside the `.3dm` file without requiring external databases.

---

## 🔍 SEARCH: Query Cheatsheet
<video src="Resources/MP4/FILTER%20SELECTION.mp4" width="100%" autoplay loop muted playsinline></video>


Finding the right data shouldn't be hard. Our custom query engine understands human logic:

### Basic Search
<video src="Resources/MP4/FILTER%20SELECTION%202.mp4" width="100%" autoplay loop muted playsinline></video>

Type any text into the filter box to instantly hide rows that don't contain your search string.
- *Example:* Typing `wood` will show only objects with "wood" in any column.

Search is always case-insensitive.

### Multi-Term Search (AND)
Separate terms with commas: an object must match **every** term.
- *Example:* `timber, phase 6` finds objects that contain both "timber" and "phase 6".

### Either Term (OR)
Use ` OR ` (capital letters, with spaces) or ` | ` between terms: an object must match **at least one**.
- *Example:* `timber OR steel` finds objects that contain "timber" or "steel".
- Combine both: `timber OR steel, phase 6` finds timber or steel objects that are also in phase 6.

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
- `^(Concrete|Steel)$` : Exact match on either value, nothing longer. (Regex mode is already case-insensitive.)

*Want to master Regex? Check out the [RexEgg Quick Start Guide](https://www.rexegg.com/regex-quickstart.php) for a comprehensive cheat sheet, or use [Regex101](https://regex101.com/) if you want an interactive tool to test your patterns.*

---
*Created by [Enzyme APD](https://www.weareenzyme.com/)*

---

## 🚀 Installation

**Requirements:** Rhino 8 for Windows or Mac. Works with Rhino's default .NET runtime and, on Windows, with the .NET Framework runtime (`SetDotNetRuntime`).

### From the Rhino Package Manager (recommended)
1. In Rhino 8, run the `PackageManager` command.
2. Search for **UserTextDatabase** (tick *Include pre-releases* while the plugin is in beta).
3. Click **Install** and restart Rhino.
4. Open the panel with the `UserTextDB` command.

### Manual install (beta testers)
1. Download the latest `.yak` file from the [release folder](release/). *(Click the `.yak` file, then click the "Download raw file" button).*
2. Open Rhino 8.
3. Open a file explorer and simply **Drag and Drop** the downloaded `.yak` file directly into the open Rhino 8 window.
4. Restart Rhino to complete the installation.

---

## 📝 Changelog

### 1.1.48-beta
**New**
- Calculated columns: `@Layer`, `@Block`, `@Area`, `@Volume`, `@Length`, `@Base Z` (enable them in Grid Settings).
- Group totals per column: Sum, Average, Min, Max or Count in group rows.
- Natural sorting and group order (`Level 2` before `Level 10`).
- Text field formulas show their evaluated value.
- 3D Audit: stable colours per value, gradient for numeric columns, and a legend in the viewport.

**Fixes**
- The grid stays readable in narrow or short panels: settings tabs scroll and the grid always keeps its space ([#1](https://github.com/ENZYME-APD/UserTextDB-Public/issues/1)).
- The *Read Documentation* link in the Info tab opens this page.

### 1.1.47-beta
**Fixes**
- Renaming a key no longer erases values on objects that already had the new key.
- CSV export no longer breaks when an object name contains a comma; accents and Spanish/European Excel are handled.
- CSV import matches columns by header name, supports multi-line cells and reports skipped rows.
- The grid now stays in sync with edits made outside the panel (Properties panel, `SetUserText`, undo/redo), when opening or importing files, when switching documents on Mac, after *Select None*, and when layers are hidden or locked.
- Every edit is one undo step.
- New files no longer get example columns (Status/Material/Phase) added automatically, and opening a file no longer marks it as modified.
- 3D Audit no longer hides objects that have no render mesh, and works in non-English Rhino.
- After committing an edit with `Enter`, the cell stays selected for arrow-key navigation.

**Performance**
- Editing, batch editing, filtering and selection sync are much faster on large models (no more full grid rebuilds per object).
- 3D Audit no longer rebuilds geometry on every frame.

**Compatibility**
- One package for Rhino 8 on Windows and Mac, including the .NET Framework runtime on Windows.
