# unix-File-Compression-Tool-Wrapper-
Provide a menu-driven script to compress and decompress files using available tools. Example: Choosing option 1 compresses notes.txt into notes.tar.gz.



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
