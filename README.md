# unix-File-Compression-Tool-Wrapper-
Provide a menu-driven script to compress and decompress files using available tools. Example: Choosing option 1 compresses notes.txt into notes.tar.gz.

1. Menu-Driven Interface
- Displays a clear, interactive menu with numbered options.
- Allows users to choose between compression, decompression, and exit.
2. File Compression
- Compresses a file using tar -czf.
- Automatically names the output as filename.tar.gz.
- Uses gzip compression for efficient archiving.
3. File Decompression
- Decompresses .tar.gz files using tar -xzf.
- Restores original file(s) from the archive.
4. File Existence Validation
- Checks if the input file exists before performing any operation.
- Prevents errors by showing a message if the file is missing.
5. Loop and Exit Control
- Uses an infinite while true loop to keep the tool running.
- Exits cleanly when the user selects option 3 using break.
6. User-Friendly Design
- Provides clear success and error messages.
- Prompts are intuitive and beginner-friendly.



REQUIRMENTS : 
- Written in Bash and runs in a Unix/Linux terminal
- Uses standard tools: tar, gzip, gunzip
- Provides a menu to compress, decompress, or exit
- Accepts user input interactively
- Validates file existence before processing
- Compresses files into .tar.gz and extracts them bac








#!/bin/bash
# File Compression Tool (Wrapper)
# Author: Adrian Thakur
# Description: Compress and decompress files using tar and gzip

while true; do
    echo "=============================="
    echo "   File Compression Tool"
    echo "=============================="
    echo "1. Compress a file"
    echo "2. Decompress a file"
    echo "3. Exit"
    echo "=============================="
    read -p "Enter your choice [1-3]: " choice

    case $choice in
        1)
            read -p "Enter the filename to compress (e.g., notes.txt): " filename
            if [ -f "$filename" ]; then
                tar -czf "${filename}.tar.gz" "$filename"
                echo " File compressed to ${filename}.tar.gz"
            else
                echo " File not found: $filename"
            fi
            ;;
        2)
            read -p "Enter the compressed file to decompress (e.g., notes.tar.gz): " compressed
            if [ -f "$compressed" ]; then
                tar -xzf "$compressed"
                echo " File decompressed from $compressed"
            else
                echo " File not found: $compressed"
            fi
            ;;
        3)
            echo " Exiting the tool. Goodbye!"
            break
            ;;
        *)
            echo " Invalid choice. Please enter 1, 2, or 3."
            ;;
    esac
    echo ""
done

USAGE : 
- Option 1: Enter the name of the file you want to compress (e.g., notes.txt). It will create notes.txt.tar.gz.
- Option 2: Enter the name of a .tar.gz file to decompress (e.g., notes.txt.tar.gz). It will extract the original file.
- Option 3: Exit the tool.




LAB PROJECT DETAILS : 
Adrian Thakur
241033060
COURSE : unix lab  PROJECT : File Compression Tool (Wrapper)



HOW IT WORKS :
- Shows a menu with options to compress, decompress, or exit
- Reads user input to select an action
- Compresses files using tar -czf into .tar.gz format
- Decompresses .tar.gz files using tar -xzf
- Checks if the file exists before processing
- Loops until the user chooses to exit



