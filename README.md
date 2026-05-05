# Batch Command Tool

A powerful and user-friendly batch processing tool built with Python and Tkinter. Supports multi-language interface, file batch operations, CMD/PowerShell batch commands, and provides comprehensive command reference.

![Version](https://img.shields.io/badge/version-1.1.0-blue)
![Python](https://img.shields.io/badge/python-3.7+-green)
![License](https://img.shields.io/badge/license-MIT-orange)

---

## Features

### 🌐 Multi-Language Support
- **6 UN Official Languages**: Chinese, English, French, Spanish, Russian, Arabic
- **Automatic Language Detection**: Automatically detects system language on first run
- **Dynamic Language Loading**: Add new languages without modifying code
- Simply create a new JSON file in `config/language/` folder

### 📁 File Batch Processing

#### File Selection & Management
- Select folder and load all files
- Multi-select files with Ctrl/Cmd+Click
- Sort files by: Name, Size, Time, Type
- Remove files from list (refresh to restore)

#### Batch Operations
| Operation | Description |
|-----------|-------------|
| **Move** | Move to specified directory |
| **Copy** | Copy to specified directory |
| **Copy Here** | Create copy in current folder |
| **Delete** | Delete files (confirmation required) |
| **Remove from List** | Remove from list (doesn't delete file) |
| **Rename** | Batch rename (8 modes) |
| **Change Extension** | Batch change file extension |
| **Change Time** | Modify file timestamp |

### 🔄 Advanced Batch Rename

#### 8 Rename Modes

1. **Simple Numbering**
   - Prefix + Number + Extension
   - Custom start number
   - Zero-padded numbers (e.g., 001, 002)

2. **Variable Placeholder**
   - Flexible pattern using variables:
     - `{name}` - Original filename (without extension)
     - `{num}` - Zero-padded number
     - `{index}` - Index starting from 0
     - `{index1}` - Index starting from 1
     - `{ext}` - Extension (with dot)
     - `{ext_no_dot}` - Extension (without dot)

3. **Multi-Position Replace**
   - Multiple find/replace rules
   - Apply rules in sequence
   - Real-time preview

4. **Find & Replace**
   - Simple text search and replace
   - Batch replace specific characters

5. **Regular Expression**
   - Powerful regex pattern matching
   - Supports regex groups and backreferences

6. **Change Case**
   - UPPERCASE
   - lowercase
   - Title Case
   - Capitalize

7. **Add Timestamp**
   - Multiple format options
   - Add as prefix or suffix

8. **Insert/Delete**
   - Insert text at specific position
   - Delete characters from specific position

#### Real-time Preview
- See changes before applying
- Original filename → New filename display
- Auto-updates as you modify settings

### 💻 CMD Batch Processing

- **Template-based command generation**
- **Variables**: `{file}`, `{name}`, `{ext}`, `{index}`, `{index1}`, `{newname}`
- **Real-time preview of generated commands**
- **Batch execution with output display**
- **Built-in command reference help**

**Example:**
```
Template: ren "{file}" "{newname}"
New Value: {name}_backup{ext}

Result:
[1] ren "file1.txt" "file1_backup.txt"
[2] ren "file2.txt" "file2_backup.txt"
```

### ⚡ PowerShell Batch Processing

- **Same template-based design**
- **Additional variable**: `{folder}` - Working directory path
- **PowerShell command execution**
- **Built-in PowerShell cmdlet reference**

**Example:**
```
Template: Copy-Item -Path "{file}" -Destination "{folder}\backup\{newname}"
New Value: {name}_copy{ext}

Result:
[1] Copy-Item -Path "file1.txt" -Destination "C:\test\backup\file1_copy.txt"
```

### 📚 Command Reference

- **CMD Help**: Press "Help" button in CMD Batch page
- **PowerShell Help**: Press "Help" button in PowerShell Batch page
- **Comprehensive documentation for both shells**

### ⚙️ Settings

- **Language Selection**: Switch between 6 languages instantly
- **Auto-save**: Settings automatically saved when changed
- **Error Handling Options**:
  - Skip failed operations automatically
  - Show error summary after operation

---

## Installation

### Prerequisites
- Python 3.7 or higher
- Tkinter (usually comes with Python)

### Quick Start

1. Clone or download this repository
2. Navigate to the project folder
3. Run:
```bash
python BatchCommandTool.py
```

For Windows, you can also double-click `BatchCommandTool.py` to run.

To avoid the black command prompt window, rename the file to `BatchCommandTool.pyw` and run it.

---

## Project Structure

```
BatchCommandTool-Python/
├── BatchCommandTool.py       # Main application
├── config/
│   ├── settings.json         # User settings
│   ├── language/             # Language files
│   │   ├── zh_cn.json        # Chinese (Simplified)
│   │   ├── en_us.json        # English
│   │   ├── fr_fr.json        # French
│   │   ├── es_es.json        # Spanish
│   │   ├── ru_ru.json        # Russian
│   │   └── ar_ar.json        # Arabic
│   └── help/                 # Command reference
│       ├── cmd/              # CMD help
│       │   ├── en_us.md
│       │   └── zh_cn.md
│       └── powershell/       # PowerShell help
│           ├── en_us.md
│           └── zh_cn.md
```

---

## Adding New Languages

1. Create a new JSON file in `config/language/` folder
2. Name it using the format: `{language_code}.json`
3. Copy the structure from an existing language file
4. Translate all strings to the new language
5. Add a `language_name` field for display in the dropdown
6. The new language will automatically appear in the settings!

### Language File Structure

```json
{
    "language_name": "Your Language",
    "app_title": "Application Title",
    "sidebar": {
        "file_batch": "File\nBatch",
        "cmd_batch": "CMD\nBatch",
        "powershell_batch": "PowerShell\nBatch",
        "settings": "Settings"
    },
    "file_batch": {
        "select_folder": "Select Folder",
        ...
    },
    "cmd_batch": {
        "title": "CMD Batch",
        "help": "Help",
        ...
    },
    "powershell_batch": {
        "title": "PowerShell Batch",
        "help": "Help",
        ...
    }
}
```

#### Note: In the packaging program, the configuration folder is located at BatchCommandTool_internalconfig

---

## Usage Examples

### Example 1: Rename Photos
Select 100 photos (photo1.jpg, photo2.jpg, ...), use Simple Numbering mode:
- Prefix: `vacation_`
- Start: `1`
- Padding: `3`
- Result: `vacation_001.jpg`, `vacation_002.jpg`, ...

### Example 2: Change File Extensions
Change all `.txt` files to `.md`:
1. Select files
2. Click "Change Extension"
3. Old extension: `.txt`
4. New extension: `.md`

### Example 3: Add Date to Filenames
Add current date as prefix:
1. Select files
2. Use "Add Timestamp" mode
3. Format: `YYYYMMDD`
4. Position: Prefix
5. Result: `20260503_originalname.jpg`

### Example 4: CMD Batch Rename
```
Template: ren "{file}" "{newname}"
New Value: {name}_backup{ext}

Result:
[1] ren "photo1.jpg" "photo1_backup.jpg"
[2] ren "photo2.jpg" "photo2_backup.jpg"
```

### Example 5: PowerShell Batch Copy
```
Template: Copy-Item -Path "{file}" -Destination "{folder}\backup\{newname}"
New Value: {name}_copy{ext}

Result:
[1] Copy-Item -Path "doc1.pdf" -Destination "C:\docs\backup\doc1_copy.pdf"
```

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Ctrl+Click** | Multi-select files |
| **Enter** | Add command (in input field) |

---

## Screenshots

The application features:
- Clean, modern interface with custom title bar
- Left sidebar for navigation
- Main content area with file list
- Right panel for sorting and operations
- Modal dialogs for advanced operations
- Command reference help windows

---

## Known Issues

- None reported

---

## License

This project is open source and available under the MIT License.

---

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

---

## Author

Created with ❤️ using Python and Tkinter

---

## Acknowledgments

- Multi-language support powered by JSON configuration
- Modern GUI design using Tkinter theming
- Command references based on official Microsoft and Windows documentation
