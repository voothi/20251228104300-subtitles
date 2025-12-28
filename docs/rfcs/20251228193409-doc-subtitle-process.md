# 20251228193409 - Documentation of Subtitle Creation Process

## Context
I have started a new repository to work on preparing subtitles as part of working with foreign languages and testing Kardenwort tools.
In the first version of the release, I need to describe the optimal process found for creating subtitles using Subtitle Edit and its own utility (modified to work in word-by-word subtitle creation mode).

## Implementation Details
The process currently consists of the following stages:

1.  **Acquisition**: Receive video or audio recording in mp3 or mp4 using Open-Video-Downloader or NewPipe. Low resolution is sufficient.
2.  **Slicing**: If the recording is very long, cut it using LosslessCut along the boundaries of Chapters into separate recordings for processing in portions or in parallel.
3.  **Recognition**: Recognize the audio track. Use Subtitle Edit or `20250228230803-whisper` with Faster-Whisper with launch keys `--threads 8 --one_word 2` into an SRT file. This provides word-by-word subtitles, the most flexible form for further processing.
4.  **Version Control**: Create a separate directory in this or another CVS (Git) repository. Save subtitles and start tracking their changes. Ensure binary files are not tracked, only text subtitle files.
5.  **Correction**: Play the resulting subtitles in Subtitle Edit, viewing and editing via `Ctrl+H` and Merge line. After each action, record the work with ZID in CVS. This results in a word-by-word subtitle file (v1), recognized and corrected.
6.  **Sentence Merging**: In Subtitle Edit, merge words into sentences along the boundaries of the track using the Auto-translate / `Merge sentences...` function. Save this as a separate file v2. This version allows moving to the subtitle translation stage.
7.  **Translation**: Translate subtitles in semi-automatic mode using `aistudio.google.com` / Gemini 2.5 Pro. Use the prompt `docs/prompts/20251108170321-translation-into-english.md` (used for `20251227091752-auto-вещества-для-ии-325-ru.v2.en.srt`). Carry out the translation in Subtitle Edit via Auto-translate / Auto-translate via Copy-Paste... Select Max block size 5000-10000 on an empty model context. Line separator `@@@`. Save the subtitle file with the `.en` postfix (e.g., `filename.v2.en.srt`).
8.  **Verification**:
    *   Create a hash sum from the audio file using 7z to ensure subtitles exactly match the recording.
    *   View double subtitles in a player like Chrome using the [asbplayer](https://github.com/killergerbah/asbplayer) plugin (can be used as a PWA or locally).
