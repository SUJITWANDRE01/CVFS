# Customized Virtual File System (CVFS)

## Overview
The Customized Virtual File System (CVFS) is an implementation of a file system in memory that simulates the behavior of a traditional file system. This project provides a command-line interface for users to interact with the virtual file system, performing operations such as creating, reading, writing, and deleting files.

## Features
- **File Operations**: Create, open, close, read, write, append, and delete files
- **Directory Operations**: List all files with their information
- **File Attributes**: Track file size, permissions, reference count, and more
- **Seek Functionality**: Move file pointer to specific locations
- **Command Line Interface**: User-friendly shell-like interface for file operations

## System Architecture

### Key Components
1. **Superblock**: Maintains metadata about the file system
   - Total number of inodes
   - Free inodes count

2. **Inode**: Stores information about individual files
   - File name
   - Inode number
   - File size (allocated and actual)
   - File type (regular or special)
   - File data buffer
   - Link count and reference count
   - Access permissions

3. **File Table**: Maintains information about opened files
   - Read and write offsets
   - Mode of file access
   - Reference to associated inode

4. **User File Descriptor Table (UFDT)**: Array of file table pointers

5. **Disk Inode List Block (DILB)**: Linked list of all inodes

## Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `create` | Create a new file | `create <filename> <permission>` |
| `open` | Open an existing file | `open <filename> <mode>` |
| `close` | Close a specific file | `close <filename>` |
| `closeall` | Close all opened files | `closeall` |
| `read` | Read from a file | `read <filename> <number-of-bytes>` |
| `write` | Write into a file | `write <filename>` followed by the content |
| `truncate` | Delete all data from a file | `truncate <filename>` |
| `rm` | Delete a file | `rm <filename>` |
| `ls` | List all files | `ls` |
| `stat` | Display file information | `stat <filename>` |
| `fstat` | Display file information using descriptor | `fstat <file-descriptor>` |
| `lseek` | Change file offset | `lseek <filename> <offset> <position>` |
| `help` | Display all available commands | `help` |
| `man` | Display manual for a command | `man <command-name>` |
| `exit` | Terminate the file system | `exit` |
| `clear` | Clear the console | `clear` |

## File Permissions
- **1**: Read only
- **2**: Write only
- **3**: Read and Write

## File Access Modes
- **1**: Read only mode
- **2**: Write only mode
- **3**: Read and Write mode

## Technical Details
- Maximum number of files: 50
- Maximum file size: 2048 bytes
- Regular file type: 1
- Special file type: 2

## How to Compile and Run
```bash
# Compile the code
g++ CVFS.cpp -o CVFS

# Run the executable
./CVFS
```

## Example Usage
```
Marvellous VFS : > create Demo.txt 3
File is successfully created with file descriptor : 3

Marvellous VFS : > write Demo.txt
Enter the data : 
Hello, this is CVFS demo.

Marvellous VFS : > read Demo.txt 50
Hello, this is CVFS demo.

Marvellous VFS : > ls
File Name       Inode number     File size       Link count
----------------------------------------------------------
Demo.txt        3                23              1
----------------------------------------------------------

Marvellous VFS : > stat Demo.txt
---------Statistical Information about file---------
File name : Demo.txt
Inode Number 3
File size : 2048
Actual File size : 23
Link count : 1
Reference count : 1
File Permission : Read & Write
----------------------------------------------------------

Marvellous VFS : > close Demo.txt

Marvellous VFS : > exit
Terminating the Marvellous Virtual File System
```

## Project Structure
The CVFS project is implemented as a single C++ program that includes:
- Data structure definitions for the file system components
- Function implementations for all file operations
- A main loop that handles user commands

## Limitations
- No support for directories/folders
- No persistence (data is lost when the program terminates)
- Fixed maximum file size
- Limited number of files

## Future Enhancements
- Implementation of a directory structure
- Persistence through file serialization
- Dynamic file size allocation
- Support for file sharing and locking mechanisms
- Improved error handling and recovery
