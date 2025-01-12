
# File Permissions and Ownership in Linux

## ls -ltr
```bash
drwxrwxr-x  3 jafar jafar      4096 Jan  5 14:24 SSD
-rwxr-xr-x  1 root  root   51454104 Jan  7 18:06 kubectl
```

### First 10 Characters: File Type and Permissions
The first 10 characters in the output represent the file type and permissions.

#### 1st Character: File Type
- `d` — The file is a directory.
- `-` — The file is a regular file.
- `l` — The file is a symbolic link.
- `b` — The file is a block device (used for storage devices).
- `c` — The file is a character device (used for serial devices, like terminals).
- `p` — The file is a named pipe (FIFO).
- `s` — The file is a socket.

#### Characters 2-10: Permissions
The remaining 9 characters are grouped into three sets of 3 characters each. They represent the permissions for:

- **Owner** (user who owns the file)
- **Group** (group to which the file belongs)
- **Others** (all other users)

##### Format: `rwxrwxrwx`
Each group consists of three characters:
- `r` — Read permission (value: 4)
- `w` — Write permission (value: 2)
- `x` — Execute permission (value: 1)
- `-` — Indicates the absence of permission.

## Detailed Breakdown

### Example 1: `drwxrwxr-x` (Directory)

#### File Type:
- `d`: This is a directory.

#### Permissions:

##### Owner (`rwx`):
- `r`: The owner can read the directory.
- `w`: The owner can write (create, delete, or modify files) inside the directory.
- `x`: The owner can execute (enter) the directory.

##### Group (`rwx`):
- `r`: The group can read the directory.
- `w`: The group can write (create, delete, or modify files) inside the directory.
- `x`: The group can execute (enter) the directory.

##### Others (`r-x`):
- `r`: Others can read the directory.
- `-`: Others cannot write inside the directory.
- `x`: Others can execute (enter) the directory.

### Example 2: `-rwxr-xr-x` (Regular File)

#### File Type:
- `-`: This is a regular file.

#### Permissions:

##### Owner (`rwx`):
- `r`: The owner can read the file.
- `w`: The owner can write to the file.
- `x`: The owner can execute the file.

##### Group (`r-x`):
- `r`: The group can read the file.
- `-`: The group cannot write to the file.
- `x`: The group can execute the file.

##### Others (`r-x`):
- `r`: Others can read the file.
- `-`: Others cannot write to the file.
- `x`: Others can execute the file.

## Other Columns in `ls -ltr` Output
## ls -ltr
```bash
drwxrwxr-x  3 jafar jafar      4096 Jan  5 14:24 SSD
-rwxr-xr-x  1 root  root   51454104 Jan  7 18:06 kubectl
```
| Column | Description |
|--------|-------------|
| Link Count (`3`, `1`) | Number of hard links to the file or directory. |
| Owner Name (`jafar`, `root`) | The user who owns the file or directory. |
| Group Name (`jafar`, `root`) | The group that owns the file or directory. |
| Size (`4096`, `51454104`) | The size of the file or directory (in bytes). Directories usually have a default size of 4096 bytes. |
| Date and Time (`Jan 5 14:24`, `Jan 7 18:06`) | Last modification date and time. |
| File Name (`SSD`, `kubectl`) | The name of the file or directory. |

## Changing File Permissions

### Using `chmod` Command
You can modify file permissions using the `chmod` command.

#### Syntax:
```bash
chmod [permissions] <file>
```

#### Examples:
- Add execute permission for the owner:
    ```bash
    chmod u+x file.txt
    ```
- Remove write permission for the group:
    ```bash
    chmod g-w file.txt
    ```
- Set permissions using numeric mode:
    ```bash
    chmod 755 file.txt
    ```
    - `755` translates to `rwxr-xr-x`.

## Changing File Ownership

### Using `chown` Command
You can modify file ownership using the `chown` command.

#### Syntax:
```bash
chown [owner]:[group] <file>
```

#### Examples:
- Change the owner of a file:
    ```bash
    chown jafar file.txt
    ```
- Change the owner and group of a file:
    ```bash
    chown jafar:jafar file.txt
    ```

## Summary Table of Permissions
| Symbol | Description       | Numeric Value |
|--------|-------------------|---------------|
| `r`    | Read permission   | 4             |
| `w`    | Write permission  | 2             |
| `x`    | Execute permission| 1             |
| `-`    | No permission     | 0             |

### Example Permission Breakdown:
- `rwxr-xr-x` = `755`
  - **Owner**: `rwx` = 7 (4+2+1)
  - **Group**: `r-x` = 5 (4+0+1)
  - **Others**: `r-x` = 5 (4+0+1)
