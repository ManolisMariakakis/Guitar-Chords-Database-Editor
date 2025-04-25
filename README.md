# 🎸 Guitar Chords Database Editor

This is a lightweight web application for viewing, editing, and exporting a **guitar chord diagram database** stored in a CSV file — including editable **fingering numbers** for each chord.

For each chord entry:
- The **chord name**, **shape**, and **image** have been taken from [jguitar.com](https://www.jguitar.com), ensuring a reliable reference.
- A **visual chord diagram** is rendered
- Editable **finger positions** are provided (fingering numbers are mostly assigned dynamically based on heuristic rules)
- An **image preview** is shown — taken from [jguitar.com](https://www.jguitar.com), specifically the **first (and typically simplest) variation** of the chord.
  ⚠️ The images are over **12,000 files**, stored in a ZIP archive (`jguitar.zip`).
  ➡️ Before running the program, you **must extract the archive** into a folder named `jguitar` placed in the same directory as the HTML file.
- The program allows visual comparison so users can **verify accuracy or correct fingerings** directly via the editor
- Save/export the updated database to a new CSV file

---

## 🚀 Features

- ✅ Load chord diagrams from a `guitar_db.csv` file
- ✅ Display each chord with:
  - Finger positions (dot chart)
  - Editable finger number inputs
  - **Image preview from jguitar.com (first/simplest chord variation)**
- ✅ Filter chords by:
  - Root note
  - Chord suffix (with categorized optgroups, e.g., "Major", "7th", "Suspended")
  - Bass note
- ✅ Render chords within a key range (From Key - To Key)
- ✅ Re-render on filter or range change
- ✅ Update fingerings directly in the UI
- ✅ Download the updated database as a CSV (`guitar_db.csv`)
- ✅ Cache-busting for always fresh CSV load

---

## 📁 CSV Format

The database file `guitar_db.csv` is a semicolon (`;`) separated file. Each line (after the header) represents one chord entry and includes the following fields:

| Field           | Description |
|----------------|-------------|
| **key**        | A unique numeric ID for sorting or referencing each chord. |
| **shape**      | A JSON array of 6 values (one per string, from low E to high e) representing frets to press. Use `"x"` for muted and `"0"` for open strings. |
| **fingers**    | A JSON array of 6 values indicating which finger (1–4) is used on each string. `"0"` means no finger (i.e., open string). |
| **image**      | The path to the chord image (typically from `jguitar.com`) used for visual comparison. |
| **chord**      | The chord name (e.g., `A`, `Am`, `G7`). |
| **chord_long** | A longer or more descriptive name (e.g., `A minor seventh`). |
| **root**       | The root note of the chord (e.g., `A`, `C#`). |
| **suffix**     | The short suffix (e.g., `m`, `7`, `maj7`). |
| **suffix_long**| The full suffix name used for grouping (e.g., `Minor`, `Major 7th`). |
| **bass**       | The bass note (used for slash chords, e.g., `E` in `C/E`). Can be empty if not applicable. |

### 🔢 Order of `shape` and `fingers` Arrays

Both the `shape` and `fingers` fields are **JSON arrays of 6 elements**, representing the six strings of a guitar in the following order:

```
["e", "B", "G", "D", "A", "E"]
```

This matches the visual layout of the chord diagrams: from **left to right**, top string ("e") to bottom string ("E").

- **Example `shape`**:  
  `["x", "0", "2", "2", "1", "0"]`

- **Example `fingers`**:  
  `["0", "0", "2", "3", "1", "0"]`

Ensure the array always contains **6 items**, even if some are `"x"` or `"0"`.

---

## 🛠 How to Use

1. Open the HTML file in a browser.
2. Ensure `guitar_db.csv` is in the same directory.
3. Use the controls to:
   - Filter by root, suffix, or bass.
   - Choose a range of chord keys to view.
   - Edit fingerings.
4. Click **"Download guitar_db.csv"** to save changes.

---

## 🧠 Developer Notes

- Uses plain HTML, CSS, and JavaScript — no external libraries.
- All data is stored in `window.chordCalls`.
- Currently displayed chord indexes are tracked in `window.visibleChordIndexes`.
- Uses cache-busting via `?nocache=Date.now()` to ensure the CSV always loads fresh.

---
