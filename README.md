# Subtitles Repository

This repository is dedicated to preparing subtitles as part of working with foreign languages and testing Kardenwort tools.

## Directory Overview

*   `20251223140658-lab`: Test records.
*   `20251228104519-p-aia-ov`: Podcast content [https://podcast.onvibe.io/](https://podcast.onvibe.io/)

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
*   **Result**: Validated word-by-word subtitles (v1).

### 6. Sentence Merging
*   In **Subtitle Edit**, use **Auto-translate / Merge sentences...**.
*   Merge words into sentences based on audio track boundaries.
*   Save as a separate file (v2). This prepares the file for translation.

### 7. Translation
*   Use **Subtitle Edit**'s **Auto-translate / Auto-translate via Copy-Paste...**.
*   **Service**: `aistudio.google.com` (Gemini 2.5 Pro).
*   **Settings**: Max block size 5000-10000, empty model context.
*   **Format**: Line separator `@@@`.
*   **Output**: Save with `.en` postfix (e.g., `filename.v2.en.srt`).

### 8. Verification
*   **Integrity**: Create a hash sum of the audio file (using 7z) to ensure subtitle synchronization.
*   **Review**: View double subtitles in a suitable player (e.g., Chrome with [asbplayer](https://github.com/killergerbah/asbplayer) plugin).

For more details, see [RFC 20251228193409](docs/rfcs/20251228193409-doc-subtitle-process.md).
