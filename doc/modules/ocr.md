# Ballon Translator: OCR Modules

[**Table of Contents**](#table-of-contents-ocr)
- [Ballon Translator: OCR Modules](#ballon-translator-ocr-modules)
  - [General Information about OCR](#general-information-about-ocr)
  - [Local OCR Modules](#local-ocr-modules)
    - [mit\* models (mit32px, mit48px, mit48px\_ctc)](#mit-models-mit32px-mit48px-mit48px_ctc)
      - [mit32px](#mit32px)
      - [mit48px](#mit48px)
      - [mit48px\_ctc](#mit48px_ctc)
    - [manga\_ocr](#manga_ocr)
    - [PaddleOCR (Optional)](#paddleocr-optional)
  - [Online/API-based OCR Modules](#onlineapi-based-ocr-modules)
    - [Starriver Cloud (Tuanzi Manga OCR)](#starriver-cloud-tuanzi-manga-ocr)
    - [Google Lens OCR](#google-lens-ocr)
    - [Bing Lens OCR](#bing-lens-ocr)
    - [Google Vision API OCR](#google-vision-api-ocr)
    - [LLM API OCR](#llm-api-ocr)
  - [Other OCR Modules](#other-ocr-modules)
    - [MacOS OCR](#macos-ocr)
    - [Windows OCR](#windows-ocr)
  - [Additional Notes on OCR Modules](#additional-notes-on-ocr-modules)

---

## General Information about OCR

*   All `mit*` models are from [manga-image-translator](https://github.com/zyddnys/manga-image-translator), supporting English, Japanese, and Korean recognition and text color extraction.
*   [manga_ocr](https://github.com/kha-white/manga-ocr) is from [kha-white](https://github.com/kha-white), specializing in text recognition for Japanese, primarily for manga.
*   [Starriver Cloud (Tuanzi Manga OCR)](https://cloud.stariver.org.cn/) requires a username and password. Automatic login is performed at program launch.
    *   Using Starriver OCR per text block is slower and doesn't significantly improve accuracy, therefore it is not recommended. Use Tuanzi Detector instead if possible.
    *   When using Tuanzi Detector, set OCR to `none_ocr` to directly read detected text, saving time and requests.
    *   See **Tuanzi OCR Instructions** for more details: ([Chinese](../团子OCR说明.md) & [Brazilian Portuguese](../Manual_TuanziOCR_pt-BR.md) only).
*   PaddleOCR is an "optional" module. If not installed, a message will appear in Debug mode. Install it by following the instructions mentioned in the debug message or uncomment the lines for `paddlepaddle(gpu)` and `paddleocr` in requirements.txt (at your own risk of potential installation errors).
*   Windows OCR and macOS OCR modules are operating system specific and will only function on their respective operating systems.

---

## Local OCR Modules

### mit* models (mit32px, mit48px, mit48px_ctc)

*   **Source:** [manga-image-translator](https://github.com/zyddnys/manga-image-translator) project.
*   **Supported Languages:** English, Japanese, Korean.
*   **Features:** Text color extraction, offline operation.

**Settings Fields (Common for mit* models):**

*   **chunk_size:**  Controls the size of image chunks processed at once. Adjusting this value might impact performance and memory usage. Typical values are 16 or 32.
*   **device:** Choose between `CPU` (processor) or `CUDA` (NVIDIA GPU, if available and configured) for processing. `CUDA` offers faster performance if a compatible NVIDIA GPU is available.

#### mit32px

*   Optimized for smaller text sizes, around 32 pixels in height.

#### mit48px

*   Optimized for larger text sizes, around 48 pixels in height.

#### mit48px_ctc

*   A variation of `mit48px` using a different Connectionist Temporal Classification (CTC) decoding method, which might offer different performance characteristics.

---

### manga_ocr

*   **Source:** [kha-white/manga-ocr](https://github.com/kha-white/manga-ocr)
*   **Supported Language:** Japanese.
*   **Focus:** Specifically trained and optimized for Japanese manga text recognition, offline operation.

**Settings Fields:**

*   **device:** Choose between `CPU` or `CUDA` for processing.

---

### PaddleOCR (Optional)

*   **Description:** Local OCR engine developed by PaddlePaddle. Requires manual installation of `paddlepaddle-gpu` and `paddleocr` libraries.
*   **Installation:** Follow the instructions after selecting `paddle_ocr` in the settings, or refer to [PaddlePaddle installation guide](https://www.paddlepaddle.org.cn/en/install/quick?docurl) and [PaddleOCR GitHub repository](https://github.com/PaddlePaddle/PaddleOCR).
*   **Supported Languages:** Extensive language support, including Chinese, English, French, German, Japanese, Korean, and many more (see full list in settings).

**Settings Fields:**

*   **language:** Select the language for OCR from the dropdown list. PaddleOCR supports a wide range of languages.
*   **device:** Choose between `CPU` or `CUDA` for processing. `CUDA` is recommended for faster performance if PaddlePaddle GPU version is installed.
*   **use_angle_cls:** Enable angle classification to improve recognition of rotated text.
*   **ocr_version:** Select the PaddleOCR model version (`PP-OCRv4`, `PP-OCRv3`, `PP-OCRv2`, `PP-OCR`). `PP-OCRv4` is the latest and generally most accurate.
*   **enable_mkldnn:** Enable Intel Math Kernel Library for Deep Neural Networks (MKLDNN) for CPU acceleration (for Intel CPUs).
*   **det_limit_side_len:** Maximum side length for text detection.
*   **rec_batch_num:** Batch size for text recognition.
*   **drop_score:** Confidence threshold for text recognition. Text boxes with confidence scores below this threshold will be discarded.
*   **text_case:** Control the text case of the output: `Uppercase`, `Capitalize Sentences`, or `Lowercase`.
*   **output_format:** Control the output format: `Single Line` (all recognized text in one line) or `As Recognized` (preserving line breaks if detected).

---

## Online/API-based OCR Modules

### Starriver Cloud (Tuanzi Manga OCR)

*   **Provider:** [Starriver Cloud (Tuanzi Manga OCR)](https://cloud.stariver.org.cn/). A Chinese OCR service.
*   **Requires Account:** Yes, requires a Starriver Cloud account, username, and password.

**Settings Fields:**

*   **User:** Your Starriver Cloud account username.
*   **Password:** Your Starriver Cloud account password.
    *   **Security Note:** Passwords are stored in plain text. Be cautious when using on shared or public computers.
*   **refine:** Enable text refinement processing for potentially improved accuracy.
*   **filtrate:** Enable text filtration processing to remove unwanted characters or noise.
*   **disable skip area:** Disables the use of predefined skip areas during OCR.
*   **detect scale:** Scaling factor for text detection. Increase for better detection of small text.
*   **merge threshold:** Threshold for merging detected text boxes into text blocks.
*   **force expand:** Forcefully expand detected text regions, potentially capturing more text.
*   **low accuracy mode:** Enable a faster, less accurate OCR mode for quicker processing.
*   **更新 Token (Update Token):** Button to manually update the API authentication token.

---

### Google Lens OCR

*   **Engine:** Google Lens API (unofficial).
*   **Based on:** [chrome-lens-ocr](https://github.com/dimdenGD/chrome-lens-ocr) project.
*   **Requires Network:** Yes.

**Settings Fields:**

*   **delay:** Delay in seconds between OCR requests to avoid rate limiting. Default is 1.0 second.
*   **newline_handling:** Method for handling newline characters in the OCR output. Options include: `remove` (remove newlines) or `keep` (preserve newlines). Default is `remove`.
*   **no_uppercase:** Convert recognized text to lowercase. (Checkbox: enable/disable).
*   **response_method:** Method for retrieving the OCR response from Google Lens. Options include: `Full Text` (get the entire text as a single string) or `Location coordinates` (retrieve text with location coordinates - may be used for different output formats in other parts of the application). Default is `Full Text`.
*   **proxy:** Optional proxy server URL for network requests. Supports various proxy formats (HTTP, SOCKS, etc.).

---

### Bing Lens OCR

*   **Engine:** Bing Lens API (unofficial).
*   **Requires Network:** Yes.
*   **Similar to:** Google Lens OCR in functionality and settings.

**Settings Fields:**

*   **delay:** Delay in seconds between OCR requests. Default is 1.0 second.
*   **newline_handling:** Method for handling newline characters (like Google Lens OCR). Default is `remove`.
*   **no_uppercase:** Convert text to lowercase (Checkbox).
*   **response_method:** Method for retrieving OCR response. Options: `Full Text` or `Location coordinates`. Default is `Location coordinates`.
*   **proxy:** Optional proxy server URL.

---

### Google Vision API OCR

*   **Engine:** Google Cloud Vision API (Official Google Cloud API).
*   **Requires Account:** Yes, requires a Google Cloud account with Vision API enabled and API key.
*   **Paid Service:** Google Cloud Vision API is a paid service.

**Settings Fields:**

*   **api_key:** Your Google Cloud Vision API key. Obtain this from the Google Cloud Console.
*   **language_hints:** Language codes to hint the API about the language of the text (e.g., `ja` for Japanese, `en` for English). Improves accuracy.
*   **proxy:** Optional proxy server URL for network requests to the Google Cloud API.
*   **delay:** Delay in seconds between API requests. Default is 0.0 (no delay, adjust if encountering API limits).
*   **newline_handling:** Method for handling newline characters in the OCR output. Options: `remove` or `keep`. Default is `remove`.
*   **no_uppercase:** Convert recognized text to lowercase (Checkbox).

---

### LLM API OCR

*   **Engine:** Large Language Models (LLMs) Vision capabilities via API.
*   **Similar to:** LLM-based Translators, utilizing APIs like OpenAI's or compatible services with image input support.
*   **Requires Network & API Key:** Yes, requires network access and an API key for the LLM provider.

**Settings Fields:**

*   **provider:** Select the LLM API provider. Example: `Google`, `OpenAI`.
*   **api_key:** API key for the selected LLM provider.
*   **endpoint:** Custom API endpoint URL, if needed for specific providers or third-party services.
*   **model:** Select the specific LLM model to use for OCR. Options depend on the chosen provider (e.g., `GPT-4 Vision Preview`, `Gemini Pro Vision`).
*   **override_model:** Option to manually specify a model name, overriding the dropdown selection.
*   **language:** Specify the language of the text in the image to guide the LLM.
*   **prompt:** Custom prompt to instruct the LLM for OCR. Example: "One line. Even if it's vertical Japanese text!".
*   **system_prompt:** System-level prompt to set the overall behavior of the LLM. Example: "You recognize the text perfectly and don't add unnecessary stuff.".
*   **proxy:** Optional proxy server URL.
*   **delay:** Delay in seconds between API requests. Default is 1.0.
*   **requests_per_minute:** Limit the number of requests per minute to stay within API rate limits (0 for no limit).

---

## Other OCR Modules

### MacOS OCR

*   **Operating System:** macOS only.
*   **Engine:** Uses built-in OCR functionality provided by macOS.
*   **Offline Operation:** Yes, leverages local OS capabilities.

**Settings Fields:**

*   **language:** Select the language for OCR from the dropdown list. Uses macOS supported languages.

---

### Windows OCR

*   **Operating System:** Windows only.
*   **Engine:** Uses built-in OCR functionality provided by Windows.
*   **Offline Operation:** Yes, leverages local OS capabilities.

**Settings Fields:**

*   **language:** Select the language for OCR from the dropdown list. Uses Windows supported languages.

---

## Additional Notes on OCR Modules

*   Choose OCR module based on target language, desired accuracy, performance needs, and availability of resources (local vs. online, CPU vs. GPU), and operating system compatibility (for OS-specific modules).
*   Experiment with different settings (like `chunk_size`, `delay`, `detect scale`, `merge threshold`, prompts) to optimize OCR performance for specific image types and text styles.
*   For Japanese manga, `manga_ocr` and `mit*` models are excellent offline choices. Consider PaddleOCR for broader language support locally.
*   For potentially higher accuracy and broader language coverage, explore online API-based options like Google Vision API or LLM API OCR, keeping in mind API costs, network dependency, and setup complexity. Google and Bing Lens OCR offer simpler, free (but potentially less reliable/rate-limited) online alternatives.
*   For macOS and Windows users, consider the respective OS-specific OCR modules for convenient, system-integrated offline OCR.

---
