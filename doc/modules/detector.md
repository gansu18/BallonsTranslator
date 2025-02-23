# Ballon Translator: Detector Modules

- [Ballon Translator: Detector Modules](#ballon-translator-detector-modules)
  - [General Information about Detectors](#general-information-about-detectors)
  - [Available Detector Modules](#available-detector-modules)
    - [CTD (Comic Text Detector)](#ctd-comic-text-detector)
    - [Starriver Detector (Tuanzi Manga Detector)](#starriver-detector-tuanzi-manga-detector)

---

## General Information about Detectors

*   Detector modules are responsible for identifying and locating text regions within an image. These detected regions are then typically passed to an OCR module for text recognition.
*   **CTD (Comic Text Detector)** is based on the [comic-text-detector](https://github.com/dmMaze/comic-text-detector) project. It is designed for detecting text in comics and manga.
*   **Starriver Detector (Tuanzi Manga Detector)** is the text detection component of [Starriver Cloud (Tuanzi Manga OCR)](https://cloud.stariver.org.cn/). It is an online service requiring account credentials.

---

## Available Detector Modules

### CTD (Comic Text Detector)

*   **Source:** [comic-text-detector](https://github.com/dmMaze/comic-text-detector)
*   **Purpose:** Designed for detecting text specifically in comics and manga images.
*   **Operation:** Local, offline processing.

**Settings Fields:**

*   **detect_size:** Specifies the size of the input image for the detection model. Available options: `896`, `1024`, `1152`, `1280`. Larger sizes may improve detection of small text but increase processing time and resource usage.
*   **det_rearrange_max_batches:** Controls the maximum number of batches for rearranging detected text boxes. Options: `1`, `2`, `4`, `6`, `8`, `12`, `16`, `24`, `32`. Adjusting this parameter can affect memory usage and processing efficiency, especially for images with a large amount of text.
*   **device:** Choose between `CPU` or `CUDA` for processing. `CUDA` is recommended for faster detection if a compatible NVIDIA GPU is available.

---

### Starriver Detector (Tuanzi Manga Detector)

*   **Provider:** [Starriver Cloud (Tuanzi Manga OCR)](https://cloud.stariver.org.cn/). This is the detection component of the Tuanzi OCR service.
*   **Requires Account:** Yes, requires a Starriver Cloud account, username, and password for API access.
*   **Operation:** Online, API-based text detection.

**Settings Fields:**

*   **User:** Your Starriver Cloud account username.
*   **Password:** Your Starriver Cloud account password.
    *   **Security Note:** Passwords are stored in plain text. Be cautious when using on shared or public computers.
*   **expand_ratio:** Controls the expansion ratio for detected text boxes. A value like `0.01` expands the boxes slightly, potentially capturing more of the text and surrounding area.
*   **refine:** Enable text refinement processing. May improve the quality of detected text regions.
*   **filtrate:** Enable text filtration processing. May help to filter out noise or unwanted elements from detected regions.
*   **disable_skip_area:** Disables the use of predefined skip areas during text detection.
*   **detect_scale:** Scaling factor for text detection. Increase for better detection of small text.
*   **merge_threshold:** Threshold for merging detected text boxes into text blocks. Adjust to control how close text boxes need to be to be grouped together.
*   **low_accuracy_mode:** Enable a faster, less accurate detection mode for quicker processing.
*   **force_expand:** Forcefully expand detected text regions, potentially capturing more text.
*   **font_size_offset:** Offset value for font size detection.  *(Further details on how this affects detection are needed)*.
*   **font_size_min (set to -1 to disable):** Minimum font size for text detection. Set to `-1` to disable minimum size filtering.
*   **font_size_max (set to -1 to disable):** Maximum font size for text detection. Set to `-1` to disable maximum size filtering.
*   **font_size_multiplier:** Multiplier for font size detection.  *(Further details on how this affects detection are needed)*.
*   **更新 Token (Update Token):** Button to manually update the API authentication token for Starriver Cloud.

---
