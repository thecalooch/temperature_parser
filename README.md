# Temperature Processor
A Python library for converting Optris temperature readings into undistorted/flattened images. 

## Dependencies
* numpy
* opencv
* Pillow

# Getting Started
## Setup input data  
Open config.json    
Set your target data folder.   
Save & Close    

## Run Everything    
Run bin/run_all.bat    

# Workflow for TIR Image Processing

## Utility Steps
### Mask Creation
python ./util/mask_creator.py
    * Create mask for removing outlier temperatures along edges of input photograph. 
    * This allows the final image to exclude values.
    * See images/mask.png for example output.

## Processing Steps
1. Convert temperature CSVs to tiffs  
   * Find min and max temperatures across all temp arrays.  
   * Convert temperatures to RGB colors using color range (based on the above min and max temps).
   * Apply image mask to remove edges.  
   * Create .tif file for each CSV.  
   
2. Fisheye lens calibration using OpenCV
   * Create calibration matrix from provided images in ./images/calibration.
   * Carry out distortion correction on tifs.  
   * Save final tifs to a folder.  
   
3. GPS data parser  
   * Read all Optris files in a directory.  
   * From each file get filename and add '.tif' to filename.  
   * Get latitude and longitude. (e.g. -43.3935689, 172.2936697).  
   * Add altitude of 304.8 to each latitude and longitude.  
   * Create one output CSV with GPS coordinates for all tifs.   

## Expected Distorted Output
![alt text](https://github.com/thecalooch/temperature_parser/blob/master/images/heatmap_example.png)

## Temperature Color Range
![alt text](https://github.com/thecalooch/temperature_parser/blob/master/images/temperature_range.png)



