# Vehicle Number Plate Detection using OpenCV and EasyOCR

An Automatic Number Plate Recognition (ANPR) system built in Python that detects a vehicle's number plate from an uploaded image, extracts the plate region, recognizes the text using OCR, and displays an annotated result — designed to run in Google Colab.

**Project report for:** Digital Image Processing
**Professor:** Ankita Jain
**Student:** Immandi Sri Likhitha (SE25MROB009)

---

## Overview

This project implements an end-to-end ANPR pipeline using **Python, OpenCV, and EasyOCR**. Given an uploaded vehicle image, the system:

1. Detects the number plate region
2. Extracts the plate area
3. Recognizes the plate text using OCR
4. Displays and saves the final annotated output image

## Objectives

- Upload a vehicle image
- Detect the number plate region
- Extract the plate area
- Recognize the plate text using OCR
- Display and save the final output image

## Tech Stack

| Software / Library | Purpose |
|---|---|
| Python | Programming language |
| Google Colab | Cloud execution environment |
| OpenCV | Image processing |
| EasyOCR | Text recognition |
| NumPy | Array operations |
| Matplotlib | Image visualization |
| PIL (Pillow) | Image handling |

Additional dependencies installed at runtime: `imutils`, `ultralytics` (YOLO-related utilities).

## How It Works

The pipeline runs as a sequence of Colab notebook cells:

| Step | Description |
|---|---|
| **1. Environment setup** | Mounts Google Drive, configures Kaggle API credentials, installs required libraries |
| **2. Dependency installation** | Installs EasyOCR, OpenCV, imutils, Ultralytics, Pillow, NumPy, Matplotlib |
| **3. Library imports** | Imports OpenCV, EasyOCR, NumPy, Matplotlib, PIL, `io`, `re` |
| **4. Image upload** | Uploads the vehicle image and converts it to OpenCV (BGR) format |
| **5. Preprocessing** | Converts to grayscale → bilateral filtering (noise removal) → Canny edge detection |
| **6. Contour detection** | Finds and sorts contours, approximates polygons, and identifies the 4-cornered rectangular plate region |
| **7. Plate extraction** | Masks and crops the detected plate region from the image |
| **8. OCR recognition** | Upscales the cropped plate, converts to grayscale, applies Otsu thresholding, and runs EasyOCR |
| **9. Text cleaning** | Joins OCR fragments, strips non-alphanumeric characters, corrects common OCR misreads (e.g. `O→0`, `I→1`, `S→5`), and pattern-matches against the Indian number plate format |
| **10. Annotation** | Draws the plate boundary and overlays the recognized text on the original image |
| **11. Save & download** | Saves the final annotated image and downloads it from Colab |

### Workflow Summary

```
Upload image → Grayscale → Filter + edge detection → Find contours
    → Identify plate (4-corner rectangle) → Extract plate region
    → OCR (EasyOCR) → Clean/format text → Annotate image → Save & download
```

## Getting Started

This project is designed to run in **Google Colab**.

1. Open the notebook in Google Colab.
2. Run the setup cell to mount Google Drive and configure your Kaggle API key (`kaggle.json`), if required.
3. Run the dependency installation cell:
   ```bash
   pip install easyocr opencv-python-headless imutils ultralytics Pillow numpy matplotlib
   apt-get install -y libgl1-mesa-glx
   ```
4. Run the remaining cells in order to upload a vehicle image and generate the annotated output.
5. The final result is saved to `/content/plate_result.jpg` and downloaded automatically.

## Number Plate Text Correction

OCR misreads are corrected using a character substitution map before validating against the plate format:

| OCR reads | Corrected to |
|---|---|
| O, Q, D | 0 |
| I, L | 1 |
| S | 5 |
| B | 8 |
| G | 6 |
| Z | 2 |

The cleaned text is matched against the Indian vehicle plate pattern (e.g. `AB 12 CD 1234`).

## Advantages

- Fully automatic vehicle number recognition
- Simple to implement and run
- Works entirely within Google Colab (no local setup required)
- Good OCR accuracy under normal conditions
- Useful for traffic monitoring and parking systems

## Limitations

- Performance may reduce for blurred images
- Low lighting conditions affect OCR accuracy
- Skewed/angled plates may reduce detection accuracy
- Unusual font styles can cause OCR errors

## Applications

- Smart parking systems
- Toll gate automation
- Traffic law enforcement
- Vehicle tracking systems
- Security surveillance

## Future Improvements

- Use YOLO for more robust plate detection
- Add support for multiple languages/plate formats
- Improve OCR accuracy with deep learning-based text recognition
- Implement real-time video processing
- Deploy as a web or mobile application

## Conclusion

This project demonstrates a complete Automatic Number Plate Recognition system using OpenCV and EasyOCR. It detects the number plate, extracts the region, recognizes the text, and produces an annotated output image — a simple, effective foundation for intelligent transportation applications.
