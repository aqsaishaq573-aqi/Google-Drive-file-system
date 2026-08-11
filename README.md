# Google Drive File System (Console Simulation in C++)

A console-based simulation of a cloud file storage system (think Google Drive), built entirely in C++ using custom-built data structures — no STL containers for the core logic. Every feature (version history, recycle bin, recent files, sharing, folder trees) is backed by a hand-rolled linked list, stack, queue, graph, or hash table.


## Why this project

Most "file system" class projects stop at create/read/delete. This one models the pieces that make cloud storage actually feel like cloud storage: version history you can roll back through, a recycle bin instead of hard deletes, a recent-files queue, sharing between users represented as a graph, and background-style cloud sync.

## Features

| Category | Capabilities |
|---|---|
| **User Accounts** | Register, login, logout, password reset, role-based access (admin/user) |
| **File Operations** | Create, read, update, delete, search, compress/decompress (RLE) |
| **Version Control** | Every update is versioned; view full history and roll back to any previous version |
| **Recycle Bin** | Deleted files are recoverable until explicitly emptied |
| **Recent Files** | Tracks the last N accessed files in access order |
| **Folder System** | Create, delete, and navigate nested folders; view the tree via DFS or BFS traversal |
| **Sharing** | Share files with other users and revoke access; relationships modeled as a graph |
| **Administration** | Set permissions, create user groups, add members, balance the folder tree, run garbage collection |
| **Cloud Sync** | Simulated background sync of files/folders through a task queue |

## Data Structures & Concepts Used

This is the core of the project — each feature maps to a specific data structure, implemented from scratch:

| Data Structure | Used For |
|---|---|
| **Singly Linked List** | File version history (`FileVersionList`) |
| **Stack** (array-based) | Recycle bin — last deleted, first restored |
| **Circular Queue** | Recent files tracking, and the cloud sync task queue |
| **Graph** (adjacency via linked nodes/edges) | Modeling file-sharing relationships between users and files |
| **Tree traversal (DFS & BFS)** | Walking and printing the folder hierarchy |
| **Hash Table** (custom hash + linear-probing conflict resolution) | Fast file lookup by content hash |
| **Bubble Sort** | Alphabetically sorting folder children and balancing the folder tree |
| **Run-Length Encoding (RLE)** | File compression/decompression, with round-trip verification |

## Tech Stack

- **Language:** C++ (Windows-specific — uses `<windows.h>` for console colors)
- **Build system:** Visual Studio project (`.sln` / `.vcxproj`)
- **No external libraries** — all data structures implemented manually

## Project Structure

```
gdrive-fs/
├── main.cpp          # Full source (all logic in one file)
└── screenshots/
    └── main-menu.png
```

## How to Run

**Visual Studio (recommended, since the project uses Windows console APIs):**
1. Open `main.cpp` in a new C++ Console App project in Visual Studio.
2. Build and run (F5).

**Command line (Windows, with MSVC or MinGW):**
```bash
g++ main.cpp -o gdrive_fs.exe
./gdrive_fs.exe
```

> Note: this project uses `<windows.h>` for colored console output, so it's Windows-only as written. Porting to Linux/macOS would mean swapping `SetConsoleTextAttribute` calls for ANSI escape codes.

## Sample Usage Flow

1. Register a user (`admin` or `user` access level) and log in.
2. Create folders and navigate between them.
3. Create a file, then update it a few times — each update is saved as a new version.
4. View version history and roll back to an earlier version.
5. Delete the file — it goes to the recycle bin, not gone for good.
6. Share a file with another registered user.
7. As an admin, run garbage collection to prune old versions, empty folders, and the recycle bin.

## Known Limitations

- Fixed-size arrays (`MAX_USERS`, `MAX_FILES` = 100) — not dynamically scalable.
- Passwords are stored in plain text (this is a DSA/console demo, not a production auth system).
- Windows-only console output.
- Cloud sync is simulated locally — no actual network calls.

## Course Context

Built as a semester project for a Data Structures course to demonstrate practical application of linked lists, stacks, queues, graphs, trees, and hashing in a single cohesive system rather than isolated exercises.
