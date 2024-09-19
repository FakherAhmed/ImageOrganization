# ImageOrganization
This script is designed to efficiently organize and compress image files from a source directory. 

# Introduction

This script is designed to efficiently organize and compress image files from a source directory. It provides an automated solution to sort images by year, optimize their size, and ensure a clean folder structure. Various functions and modules are utilized to accomplish a range of tasks.

## Main Features

- **Organize Images by Year**: Sorts images into year-based folders based on EXIF data or filenames.
- **Image Compression**: Compresses large images to save storage space while maintaining quality within defined limits.
- **Duplicate Detection**: Uses hashing to ensure no duplicate images are processed.
- **EXIF Data Utilization**: Extracts information such as the capture date and image orientation from EXIF data.
- **Error Handling**: Identifies and moves corrupted or faulty images to a specific folder.
- **Optimize Folder Structure**: Removes empty and unnecessary subfolders to create a flat and organized structure.

## Workflow

1. **Initialization**: Import necessary modules and define parameters like size limits and allowed file extensions.
2. **Directory Preparation**: Create required folders for corrupted images and images without date information.
3. **Image Processing**:
   - **Validation**: Check if the file is a valid image and exceeds the minimum size.
   - **Duplicate Checking**: Calculate an MD5 hash to identify already processed images.
   - **Extract Year**:
     - **From EXIF Data**: Attempt to extract the capture year from EXIF data.
     - **From Filename**: If EXIF data is unavailable, extract the year from the filename using regex patterns.
     - **Default Assignment**: Assign the image to the "NoDate" folder if no year can be determined.
   - **Image Compression**: Compress images larger than a set limit to reach the target size.
   - **Correct Orientation**: Adjust the image orientation based on EXIF data.
   - **Storage**: Copy the processed image into the appropriate year directory in the destination folder.
4. **Post-Processing**:
   - **Flatten Folder Structure**: Merge folders with only one subfolder to simplify the structure.
   - **Remove Empty Folders**: Delete empty folders that are no longer needed.
5. **Logging**: Record all errors and exceptions in a log file for easy tracking.

## Parameters and Settings

- **Size Limits**:
  - `small_size_limit`: 3 MB – Images above this size will be compressed.
  - `medium_size_limit`: 10 MB – Additional compression level for very large images.
  - `target_size_limit`: 6 MB – Target size for compressed images.
  - `min_image_size`: 0.05 MB – Minimum size for an image to be processed.
- **Directories**:
  - `corrupted_folder`: Folder for corrupted images.
  - `nodate_folder`: Folder for images without a determined date.
- **File Extensions**: Allowed extensions are `.jpg`, `.jpeg`, `.png`, `.tiff`, `.bmp`, `.gif`.

## Prerequisites

- **Python Modules**:
  - Standard libraries: `os`, `shutil`, `hashlib`, `re`, `time`, `logging`
  - External libraries: `PIL` (Pillow), `tqdm`
- **EXIF Support**: Images should contain EXIF metadata for certain features to work.

## Usage

1. **Set Directories**:
   - Define the `source_directory` as the path containing the images to be processed.
   - Define the `destination_directory` where the organized images will be stored.
2. **Run the Script**:
   - Ensure all prerequisites are installed.
   - Execute the script in a Python environment.
3. **Monitor Output**:
   - Processed images will be organized in the destination directory.
   - Logs will be recorded in `error_log.log`.
   - A summary of processing statistics will be displayed upon completion.

## Notes

- **Error Handling**: The script logs errors to `error_log.log`. Check this file if issues arise.
- **Performance**: The script uses `tqdm` for progress indication, which may slightly affect performance.
- **Backup**: Always backup your images before processing to prevent data loss.
