# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a CANopen documentation project for Q-Drives that uses MkDocs to generate static documentation from Markdown files. The project documents the CANopen Object Dictionary.

## Project Structure

```
canopen/
├── mkdocs.yml          # MkDocs configuration file
├── docs/               # Documentation source files
│   ├── index.md        # Homepage (contains generic MkDocs template)
│   ├── about.md        # About page (minimal content)
│   └── object-dictionary/
│       └── object-dictionary.md  # Main CANopen Object Dictionary documentation
└── raw/
    └── C7_ObjectDictionary.txt   # Raw source data for object dictionary
```

## Development Commands

### Build and Serve Documentation
- `mkdocs serve` - Start live-reloading development server
- `mkdocs build` - Build static documentation site
- `mkdocs new [dir-name]` - Create new MkDocs project
- `mkdocs -h` - Show help

### Working Directory
All MkDocs commands should be run from the `canopen/` directory.

## Content Architecture

### Object Dictionary Documentation
The main content is in `docs/object-dictionary/object-dictionary.md`, which documents CANopen objects with:
- Object indices (e.g., 0x1000, 0x1001)
- Data types (UNSIGNED8, UNSIGNED32, etc.)
- Access types (ro, const, etc.)
- PDO mapping information
- Parameter descriptions

### Raw Data Source
`raw/C7_ObjectDictionary.txt` contains the structured source data that should be used as reference when updating the Markdown documentation. This file has detailed descriptions, error codes, and technical specifications.

## Key Features
- Uses readthedocs theme
- Focuses on CANopen protocol documentation
- Contains comprehensive Object Dictionary reference
- Includes standard CANopen objects (1000-60xx ranges) and manufacturer-specific objects (2000-5000 ranges)