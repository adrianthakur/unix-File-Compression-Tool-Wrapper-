 # Unified Compression Tool
Overview
The Unified Compression Tool is a Bash-based command-line utility designed to simplify file compression and decompression tasks. It provides a menu-driven interface for compressing files into .tar.gz format, decompressing .tar.gz archives, and comparing compression ratios between ZIP and TAR.GZ formats.
This tool is useful for students, developers, and system administrators who want a lightweight, interactive way to manage file compression directly from the terminal.


Features
Upon execution, the script displays a feature overview followed by a menu with four options:
- Compress a file into .tar.gz format
- Uses tar with gzip (tar -czf) to compress a specified file.
- The output file is named <filename>.tar.gz.
- Decompress a .tar.gz archive
- Uses tar -xzf to extract the contents of a .tar.gz archive.
- The original files are restored in the current directory.
- Compare ZIP vs TAR.GZ compression
- Compresses the same file using both ZIP and TAR.GZ formats.
- Calculates and displays the original size, compressed sizes, and compression ratios.
- Requires the zip utility and bc for floating-point calculations.
- Temporary compressed files are deleted after comparison.
- Exit
- Terminates the script gracefully.

Usage
To run the tool:
bash compress_tool.sh


Follow the on-screen prompts to select an option and enter filenames as required.

Dependencies
- tar (standard on most Unix-like systems)
- gzip (used via tar -czf)
- zip (required for comparison feature)
- bc (used for calculating compression ratios)
- stat (used to retrieve file sizes)
If the zip command is not installed, the script will notify the user and skip the comparison feature.
To install missing dependencies:
sudo apt update
sudo apt install zip bc



Internal Logic
- The script uses a while true loop to continuously display the menu until the user chooses to exit.
- Input validation is performed for file existence before compression or decompression.
- Compression ratios are calculated using:
zip_ratio = zip_size / original_size
tar_ratio = tar_size / original_size
- Temporary files (.zip and .tar.gz) created during comparison are removed after displaying results.

Notes
- This script is intended for single-file operations. It does not support directory compression.
- File paths must be relative to the current working directory.
- The script is designed for educational and practical use in Unix-like environments.






REQUIRMENTS : 
- Written in Bash and runs in a Unix/Linux terminal
- Uses standard tools: tar, gzip, gunzip
- Provides a menu to compress, decompress, or exit
- Accepts user input interactively
- Validates file existence before processing
- Compresses files into .tar.gz and extracts them bac
- To use the Unified Compression Tool,system meets the following basic requirements:
System Compatibility
- Works on any Unix-like operating system (Linux, macOS, or WSL on Windows)
- Requires Bash shell (version 4.0 or higher recommended)
Required Tools
The script depends on a few standard command-line utilities. Most of them are pre-installed on Linux systems, but if you're missing any, you can install them easily:
- tar – used for creating and extracting .tar.gz archives
- gzip – works with tar to compress files
- zip – needed for comparing ZIP vs TAR.GZ compression
- stat – used to check file sizes
- bc – used to calculate compression ratios with decimal precision
needed to make zip files accesible 
sudo apt update
sudo apt install zip bc

Permissions
Before running the script, make sure it’s executable:
chmod +x compress_tool.sh


Once everything is set up, you can launch the tool with:
./compress_tool.sh




CODE : 

#!/bin/bash

# Unified Compression Tool - Bash CLI Utility

# Feature Overview
echo "=============================================="
echo "         Welcome to Unified Compression Tool"
echo "=============================================="
echo "This tool provides the following features:"
echo "1. Compress a file into .tar.gz format"
echo "   - Uses tar and gzip to reduce file size for storage or transfer."
echo "2. Decompress a .tar.gz archive"
echo "   - Extracts files from a compressed .tar.gz archive."
echo "3. Compare ZIP vs TAR.GZ compression"
echo "   - Shows file sizes and compression ratios for both formats."
echo "4. Exit"
echo "   - Closes the tool."
echo "=============================================="
echo ""

# Main Menu Loop
while true; do
    echo "=============================="
    echo "     Unified Compression Tool"
    echo "=============================="
    echo "1. Compress a file (.tar.gz)"
    echo "2. Decompress a .tar.gz file"
    echo "3. Compare ZIP vs TAR.GZ compression"
    echo "4. Exit"
    echo "=============================="
    read -p "Enter your choice [1-4]: " choice

    case $choice in
        1)
            read -p "Enter the filename to compress (e.g., notes.txt): " filename
            if [ -f "$filename" ]; then
                tar -czf "${filename}.tar.gz" "$filename"
                echo "File compressed to ${filename}.tar.gz"
            else
                echo "File not found: $filename"
            fi
            ;;
        2)
            read -p "Enter the .tar.gz file to decompress (e.g., notes.tar.gz): " compressed
            if [ -f "$compressed" ]; then
                tar -xzf "$compressed"
                echo "File decompressed."
            else
                echo "File not found: $compressed"
            fi
            ;;
        3)
            read -p "Enter the filename to compare (e.g., notes.txt): " file
            if [ ! -f "$file" ]; then
                echo "File not found: $file"
            else
                if ! command -v zip &> /dev/null; then
                    echo "Error: 'zip' command not found. Please install it to use this feature."
                    continue
                fi

                zip -q "${file}.zip" "$file"
                tar -czf "${file}.tar.gz" "$file"

                orig_size=$(stat -c%s "$file")
                zip_size=$(stat -c%s "${file}.zip")
                tar_size=$(stat -c%s "${file}.tar.gz")

                zip_ratio=$(echo "scale=2; $zip_size / $orig_size" | bc)
                tar_ratio=$(echo "scale=2; $tar_size / $orig_size" | bc)

                echo "=============================="
                echo "Original File Size: $orig_size bytes"
                echo "ZIP File Size     : $zip_size bytes"
                echo "TAR.GZ File Size  : $tar_size bytes"
                echo "------------------------------"
                echo "ZIP Compression Ratio    : $zip_ratio"
                echo "TAR.GZ Compression Ratio : $tar_ratio"
                echo "=============================="

                rm -f "${file}.zip" "${file}.tar.gz"
            fi
            ;;
        4)
            echo "Exiting the tool. Goodbye."
            break
            ;;
        *)
            echo "Invalid choice. Please enter 1, 2, 3, or 4."
            ;;
    esac
    echo ""
done













     



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

screenshots : 

<img width="1078" height="746" alt="Screenshot 2025-11-07 133650" src="https://github.com/user-attachments/assets/7c06ed5d-9cda-4408-9ea9-2a4e75b612c0" />



<img width="1009" height="402" alt="Screenshot 2025-11-07 133756" src="https://github.com/user-attachments/assets/7485471d-9887-45ef-8f18-da33a9c50184" />

<img width="1408" height="400" alt="Screenshot 2025-11-07 133816" src="https://github.com/user-attachments/assets/0dba3299-7d01-4a8b-96a1-8cca567c431c" />

<img width="1323" height="630" alt="Screenshot 2025-11-07 133837" src="https://github.com/user-attachments/assets/81f857ed-ab66-426b-b811-020b03ae84ca" />
