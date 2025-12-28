# Subtitles Repository

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 

This repository is dedicated to preparing subtitles as part of working with foreign languages and testing Kardenwort tools.

## Table of Contents

*   [Directory Overview](#directory-overview)
*   [Subtitle Creation Process](#subtitle-creation-process)
    *   [1. Acquisition](#1-acquisition)
    *   [2. Slicing (Optional)](#2-slicing-optional)
    *   [3. Recognition](#3-recognition)
    *   [4. Version Control](#4-version-control)
    *   [5. Correction](#5-correction)
    *   [6. Sentence Merging](#6-sentence-merging)
    *   [7. Translation](#7-translation)
    *   [8. Verification](#8-verification)
*   [Kardenwort Ecosystem](#kardenwort-ecosystem)
*   [License](#license)

## Directory Overview

*   `20251223140658-lab`: Test records.
*   `20251228104519-p-aia-ov`: Podcast content [https://podcast.onvibe.io/](https://podcast.onvibe.io/)

[Return to Top](#table-of-contents)

## Subtitle Creation Process

The following optimal process has been established for creating subtitles, leveraging Subtitle Edit and a modified Whisper utility (supporting word-by-word mode).

### 1. Acquisition
Receive video or audio recordings (mp3/mp4) using tools like **Open-Video-Downloader** or **NewPipe**. Low resolution is sufficient for this purpose.

### 2. Slicing (Optional)
For very long recordings, use **LosslessCut** to split the file along Chapter boundaries into smaller portions for parallel or piece-wise processing.

### 3. Recognition
Generate text from the audio track.
*   **Tools**: Subtitle Edit or `20250228230803-whisper` (Faster-Whisper).
*   **Settings**: `--threads 8 --one_word 2`
*   **Output**: An SRT file with word-by-word subtitles, offering maximum flexibility.

### 4. Version Control
*   Create a separate directory in the Git repository.
*   Save the subtitles and track changes.
*   **Note**: Ensure only text subtitle files are tracked; exclude binary files.

### 5. Correction
*   Open the subtitles in **Subtitle Edit**.
*   Play the media and edit using `Ctrl+H` and "Merge line".
*   Commit changes to Git after each session (include ZID).
*   **Result**: Validated **word-by-word** subtitles (**v1**).

### 6. Sentence Merging
*   In **Subtitle Edit**, use **Auto-translate / Merge sentences...**.
*   Merge words into sentences based on audio track boundaries.
*   **Result**: **Merged phrase/sentence** subtitles (**v2**). This version prepares the file for translation.

### 7. Translation
*   Use **Subtitle Edit**'s **Auto-translate / Auto-translate via Copy-Paste...**.
*   **Service**: `aistudio.google.com` (Gemini 2.5 Pro).
*   **Prompt**: [`docs/prompts/20251108170321-translation-into-english.md`](docs/prompts/20251108170321-translation-into-english.md).
*   **Settings**: Max block size 5000-10000, empty model context.
*   **Format**: Line separator `@@@`.
*   **Output**: Save with `.en` postfix (e.g., `filename.v2.en.srt`).

### 8. Verification
*   **Integrity**: Create a hash sum of the audio file (using 7z) to ensure subtitle synchronization.
*   **Review**: View double subtitles in a suitable player (e.g., Chrome with [asbplayer](https://github.com/killergerbah/asbplayer) plugin).

For more details, see [RFC 20251228193409](docs/rfcs/20251228193409-doc-subtitle-process.md).

[Return to Top](#table-of-contents)

## Kardenwort Ecosystem

This project is part of the [Kardenwort](https://github.com/kardenwort) environment, designed to create a focused and efficient learning ecosystem.

[Return to Top](#table-of-contents)

## License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for details.

[Return to Top](#table-of-contents)

