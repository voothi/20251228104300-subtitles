# Subtitles Repository

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 
[![Version](https://img.shields.io/badge/version-1.0.12-blue.svg)](release-notes.md)

This repository is dedicated to preparing subtitles as part of working with foreign languages and testing Kardenwort tools.
Check the [Release Notes](release-notes.md) for the latest updates.

## Table of Contents

- [Directory Overview](#directory-overview)
- [Subtitle Creation Process](#subtitle-creation-process)
    - [1. Acquisition](#1-acquisition)
    - [2. Slicing (Optional)](#2-slicing-optional)
    - [3. Recognition](#3-recognition)
    - [4. Version Control](#4-version-control)
    - [5. Correction](#5-correction)
    - [6. Sentence Merging](#6-sentence-merging)
    - [7. Translation](#7-translation)
    - [8. Verification](#8-verification)
    - [9. YouTube Studio Upload](#9-youtube-studio-upload)
    - [10. Learning Integration (Anki)](#10-learning-integration-anki)
- [Notes](#notes)
- [Kardenwort Ecosystem](#kardenwort-ecosystem)
- [License](#license)

## Directory Overview

- `20251223140658-lab`: Test records.
- `20251228104519-p-aia-ov`: Podcast content [https://podcast.onvibe.io/](https://podcast.onvibe.io/)

[Return to Top](#table-of-contents)

## Subtitle Creation Process

The following optimal process has been established for creating subtitles, leveraging [Subtitle Edit](https://github.com/SubtitleEdit) and a modified Whisper utility (supporting word-by-word mode).

### 1. Acquisition
Receive video or audio recordings (mp3/mp4) using tools like [Open-Video-Downloader](https://github.com/jely2002/youtube-dl-gui) or [NewPipe](https://github.com/TeamNewPipe). Low resolution is sufficient for this purpose.

### 2. Slicing (Optional)
For very long recordings, use [LosslessCut](https://github.com/mifi/lossless-cut) to split the file along Chapter boundaries into smaller portions for parallel or piece-wise processing.

### 3. Recognition
Generate text from the audio track.
- **Tools**: [Subtitle Edit](https://github.com/SubtitleEdit) or [Whisper Audio Recorder & Transcriber](https://github.com/voothi/20250228230803-whisper) (Faster-Whisper, recommended model: `large-v3-turbo`).
- **Settings**: `--threads 8 --one_word 2`
- **Output**: An SRT file with word-by-word subtitles (initial **v1**), offering maximum flexibility.

### 4. Version Control
- Create a separate directory in the Git repository.
- Save the subtitles and track changes.
- **Note**: Ensure only text subtitle files are tracked; exclude binary files.

### 5. Correction
- Open the subtitles in **Subtitle Edit**.
- Play the media and edit using `Ctrl+H` and "Merge line".
- Commit changes to Git after each session (include ZID).
- **Result**: Validated **word-by-word** subtitles (**v1**).

### 6. Sentence Merging
- In **Subtitle Edit**, use **Auto-translate / Merge sentences...**.
- Merge words into sentences based on audio track boundaries.
- **Result**: **Merged phrase/sentence** subtitles (**v2**). This version prepares the file for translation.

### 7. Translation
- Use **Subtitle Edit**'s **Auto-translate / Auto-translate via Copy-Paste...**.
- **Service**: [aistudio.google.com](https://aistudio.google.com) (Gemini 2.5 Pro).
- **Prompts**:
    - English: [`docs/prompts/20251108170321-translation-into-english.md`](docs/prompts/20251108170321-translation-into-english.md)
    - Belarusian: [`docs/prompts/20251108170321-translation-into-belarusian.md`](docs/prompts/20251108170321-translation-into-belarusian.md)
- **Settings**: Max block size 5000-10000, empty model context.
- **Format**: Line separator `@@@`.
- **Output**: Save with `.en` postfix (e.g., `filename.v2.en.srt`).

### 8. Verification
- **Integrity**: Create a hash sum of the audio file (using 7z) to ensure subtitle synchronization.
- **Review**: View double subtitles in a suitable player (e.g., Chrome with [asbplayer](https://github.com/killergerbah/asbplayer) plugin, or [PotPlayer](https://github.com/Pot-Player) on Windows).

### 9. YouTube Studio Upload
Finalize the process by making the subtitles available on YouTube.
- **Access**: Go to [YouTube Studio](https://studio.youtube.com).
- **Subtitles Section**: Select the video and navigate to the "Subtitles" tab.
- **Add Language**: Add the target language (e.g., English or Russian).
- **Upload File**: Choose "Upload file" and select the **v2** (or translated `.en`) SRT file.
- **Sync**: Choose "With timing" to ensure the internal SRT timestamps are used.
- **Publish**: Review and publish to make them live.

### 10. Learning Integration (Anki)
The finalized **v2** subtitles can be used for language learning.
- **Deck Preparation**: Use the subtitle text to break down and prepare an Anki deck using **Kardenwort**.
- **Word Processing**: Process each word using the [IntelliFiller AI](https://github.com/voothi/20251206123938-intellifiller-ai-addon-for-anki/tree/main) Anki add-on to automatically fill in card details and context.

[Return to Top](#table-of-contents)

## Notes

The [aistudio.google.com](https://aistudio.google.com) service is free to use, but please be aware of the following:
- There are usage limits (rate limits) for the free tier.
- By using the free tier, you agree that Google may use the data entered into the chat for service improvement purposes.

[Return to Top](#table-of-contents)

For more details, see:
- [RFC 20251228230424](docs/rfcs/20251228230424-prepare-release-v1.0.12.md) - Release v1.0.12 (Belarusian Subtitles)
- [RFC 20251228193409](docs/rfcs/20251228193409-doc-subtitle-process.md) - Subtitle Creation Process

## Kardenwort Ecosystem

This project is part of the [Kardenwort](https://github.com/kardenwort) environment, designed to create a focused and efficient learning ecosystem.

[Return to Top](#table-of-contents)

## License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for details.

[Return to Top](#table-of-contents)
