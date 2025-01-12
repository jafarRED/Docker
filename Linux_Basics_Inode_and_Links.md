# Hard Link

A hard link is a direct reference (or alias) to the same inode (physical location on the disk) as the original file.

## Key Features of Hard Links:

### Same File Content:
- Both the original file and the hard link point to the same inode, meaning they share the same data.
- If one is modified, the changes reflect in the other.

### Independent Names:
- Deleting the original file does not affect the hard link since it points to the same inode.

### Inode Count:
- The number of hard links is reflected in the link number in the `ls -l` output.

### Restrictions:
- Cannot create hard links for directories (to avoid file system loops).
- Hard links must exist on the same filesystem as the original file.

### Example of Hard Link:
```bash
# Create a hard link
ln original.txt hardlink.txt

# Verify the link count
ls -li
```
**Output:**
```
123456 -rw-r--r-- 2 user user 1024 Jan 12 12:00 hardlink.txt
123456 -rw-r--r-- 2 user user 1024 Jan 12 12:00 original.txt
```
- Both files have the same inode number (123456).
- The link count (second column) is 2.

#### Deleting the Original File:
```bash
rm original.txt
```
The data is still accessible using `hardlink.txt` because the inode is intact.

---

# Soft Link (Symbolic Link)

A soft link (or symbolic link) is like a shortcut or pointer to another file. It stores the path to the target file, not the actual data.

## Key Features of Soft Links:

### Separate Inode:
- A soft link has its own inode and does not share data with the original file.

### Path-Dependent:
- If the target file is deleted, the soft link becomes broken (it points to a nonexistent file).

### Flexible:
- Can link across different filesystems or even directories.
- Can create soft links for directories.

### Shortcut-Like:
- Works similarly to shortcuts in Windows.

### Example of Soft Link:
```bash
# Create a soft link
ln -s original.txt softlink.txt

# Verify the link
ls -li
```
**Output:**
```
234567 lrwxrwxrwx 1 user user 13 Jan 12 12:00 softlink.txt -> original.txt
123456 -rw-r--r-- 1 user user 1024 Jan 12 12:00 original.txt
```
- `softlink.txt` has its own inode (234567) and points to `original.txt`.

#### Deleting the Original File:
```bash
rm original.txt
```
The soft link `softlink.txt` will no longer work and is considered broken.

---

# Key Differences Between Hard Link and Soft Link

| Feature         | Hard Link                                   | Soft Link                               |
|-----------------|--------------------------------------------|-----------------------------------------|
| Type            | Points to the same inode as the file.      | Points to the file’s path (shortcut).   |
| Inode           | Shares the same inode as the original.     | Has a different inode from the original.|
| File Systems    | Must be on the same filesystem.            | Can link across different filesystems.  |
| Directories     | Cannot link directories.                   | Can link directories.                   |
| Original File   | Still accessible if the original is deleted.| Becomes broken if the original is deleted.|
| Command to Create| `ln original hardlink`                     | `ln -s original softlink`               |

---

# Practical Use Cases

## Hard Link:
- Useful for creating backups where both names point to the same data, minimizing disk space usage.

## Soft Link:
- Ideal for shortcuts or when you want to link files across different filesystems or directories.

---

# What Is the Link Number in `ls -l`?

## For Files:
- The link number shows how many hard links point to the same inode (storage location).

**Example:**
- If a file has a link number of 1, it means no other hard links exist (only the file itself points to the inode).
- If you create a hard link to a file, the link number increases for both the original and the hard link.

## For Directories:
- The link number indicates how many entries inside the directory point to it. This includes:
  - The directory itself (via `.`).
  - The reference in the parent directory (via `..`).
  - Any subdirectories inside it (each subdirectory adds a hard link back to its parent).

---

# Key Rule About Hard Links for Directories
- While you cannot manually create hard links for directories (because it could cause filesystem loops), directories automatically have hard links created by the system to maintain the filesystem structure.

### Example Breakdown
**Output:**
```bash
drwxrwxr-x  3 jafar jafar 4096 Jan  5 14:24 SSD
-rwxr-xr-x  1 root  root  51454104 Jan  7 18:06 kubectl
```

#### SSD Directory
- **Type:** Directory (`d`).
- **Link Number:** 3. Why?
  - `SSD/.` → The directory itself.
  - `../SSD` → Reference from its parent directory.
  - `SSD/aws-root` → A subdirectory inside `SSD`, which adds a link back to `SSD`.

#### `kubectl` File
- **Type:** File (`-`).
- **Link Number:** 1.
  - Only the file itself points to its inode.

---

# File System Structure Overview

1. **Directories and Inodes:**
   - Directories are special files that map file names to inode numbers.
   - Inodes contain metadata about files, such as permissions, file size, ownership, timestamps, and the data block addresses where the actual content is stored.
   - Inodes do not contain the file name. The name of the file is stored in the directory entry.

2. **Directory Entry:**
   - A directory entry maps a file name to an inode number.
   - Each entry contains:
     - **File Name:** The actual name of the file (e.g., `example.txt`).
     - **Inode Number:** The unique number identifying the file's inode.

3. **Accessing Files:**
   - When accessing a file (e.g., `cat example.txt`), the system:
     1. Searches the directory entry for `example.txt`.
     2. Finds the inode number associated with the file.
     3. Uses the inode to retrieve metadata and locate data blocks containing the file's content.

4. **Multiple Names (Hard Links):**
   - Creating a hard link adds another directory entry pointing to the same inode.

### Example:
```bash
$ ln example.txt example_link.txt
```
Directory:
| File Name         | Inode Number |
|-------------------|--------------|
| example.txt       | 123456       |
| example_link.txt  | 123456       |

Both names point to the same inode, so changes to one file affect the other.

---

# Summary
- **Inode:** Contains file metadata (size, permissions, data blocks).
- **File Name:** Stored in the directory entry, which maps the name to an inode number.
- **Directory Entry:** Maps a file name to an inode number.
- **Hard Links:** Multiple directory entries can refer to the same inode, meaning the same file can have multiple names.
- **Soft Links:** Shortcut-like references to files, which can span filesystems or directories.
