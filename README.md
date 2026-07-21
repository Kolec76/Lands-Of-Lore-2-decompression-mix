LOL2 Toolchain

LOL2 Toolchain is a complete Windows application for extracting, decompressing, analyzing, and rebuilding level resources used in Lands of Lore II: Guardians of Destiny. The project was developed as part of an extensive reverse engineering effort focused on documenting the game's internal file formats and resource management system.

The application provides an automated workflow for handling level archives (MIX files), identifying their contents, decompressing RefPack compressed resources, and rebuilding the original game directory structure.

Features
Automatic loading of supported MIX level archives
Automatic backup of original game files
Extraction of MAP, ODF, and TEX resources
Automatic resource type detection
Built-in RefPack decompression engine
Support for the game's TEX wrapper format
Automatic detection of SPHERE1, SPHERE2, and SPHERE3 directories
Automatic reconstruction of the original game folder structure
MIX reset utility for rebuilding custom resources
Easy-to-use graphical user interface (GUI)
Workflow
Select MIX Archive
        │
        ▼
Create Backup
        │
        ▼
Extract MAP / ODF / TEX
        │
        ▼
Decompress TEX (RefPack)
        │
        ▼
Detect SPHERE Folder
        │
        ▼
Rebuild Game Directory Structure
Supported Archives

The tool currently supports the official Lands of Lore II level archives:

L1_DC.MIX
L3_DH.MIX
L4_HJ.MIX
L5_HC.MIX
L7_DH.MIX
L8_SJ.MIX
L9_DR.MIX
L10_DC.MIX
L12_CM.MIX
L13_RC.MIX
L14_HT.MIX
L16_CA.MIX
L17_HC.MIX
L19_BC.MIX
L20_BB.MIX
Technical Overview

The application includes custom implementations of:

MIX archive parser
MIX index reader
Automatic resource identification
Binary file extractor
RefPack stream decompressor
TEX wrapper parser
Automatic SPHERE directory detection
Resource rebuilding utilities

All operations are performed automatically through a single graphical interface.

Directory Structure
LOL2Tool.exe
│
├── KOPY_MIX
│
├── WORK
│   └── LEVEL
│       ├── LEVEL.MAP
│       ├── LEVEL.ODF
│       └── LEVEL.TEX
│
├── SPHERE1
├── SPHERE2
└── SPHERE3
Technologies
C++
Embarcadero C++ Builder
VCL
WinAPI
RefPack Decompression
Binary File Parsing
Reverse Engineering
Project Goals

This project was created for:

Reverse engineering research
Documentation of Lands of Lore II file formats
Game archive analysis
RefPack format research
Modding tool development
Digital preservation of classic game data formats
How to Use
Place the application inside the game directory.
Select a supported MIX archive.
The program automatically creates a backup.
Run Extract to extract the MAP, ODF, and TEX files.
Run Decompress to unpack the TEX resource.
Use Sphere Build to reconstruct the original game directory structure.
If necessary, use Reset MIX before rebuilding the archive.
Author

Kolec

Developed since 2026.
