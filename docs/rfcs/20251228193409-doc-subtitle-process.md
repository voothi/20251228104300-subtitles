# 20251228193409 - Documentation of Subtitle Creation Process

## Context
I have started a new repository to work on preparing subtitles as part of working with foreign languages and testing Kardenwort tools.
In the first version of the release, I need to describe the optimal process found for creating subtitles using [Subtitle Edit](https://github.com/SubtitleEdit) and its [own utility](https://github.com/voothi/20250228230803-whisper) (modified to work in word-by-word subtitle creation mode).

## Implementation Details
The process currently consists of the following stages:

1.  **Acquisition**: Receive video or audio recording in mp3 or mp4 using [Open-Video-Downloader](https://github.com/jely2002/youtube-dl-gui) or [NewPipe](https://github.com/TeamNewPipe). Low resolution is sufficient.
2.  **Slicing**: If the recording is very long, cut it using [LosslessCut](https://github.com/mifi/lossless-cut) along the boundaries of Chapters into separate recordings for processing in portions or in parallel.
3.  **Recognition**: Recognize the audio track. Use [Subtitle Edit](https://github.com/SubtitleEdit) or [`20250228230803-whisper`](https://github.com/voothi/20250228230803-whisper) with Faster-Whisper with launch keys `--threads 8 --one_word 2` into an SRT file. This provides word-by-word subtitles (initial **v1**), the most flexible form for further processing.
4.  **Version Control**: Create a separate directory in this or another CVS (Git) repository. Save subtitles and start tracking their changes. Ensure binary files are not tracked, only text subtitle files.
5.  **Correction**: Play the resulting subtitles in Subtitle Edit, viewing and editing via `Ctrl+H` and Merge line. After each action, record the work with ZID in CVS. This results in **word-by-word** subtitles (**v1**), recognized and corrected.
6.  **Sentence Merging**: In Subtitle Edit, merge words into sentences along the boundaries of the track using the Auto-translate / `Merge sentences...` function. Save this as a separate file: **merged phrase/sentence** subtitles (**v2**). This version allows moving to the subtitle translation stage.
7.  **Translation**: Translate subtitles in semi-automatic mode using [aistudio.google.com](https://aistudio.google.com) / Gemini 2.5 Pro. Use the prompt `docs/prompts/20251108170321-translation-into-english.md` (used for `20251227091752-drugs-for-ai-325-ru.v2.en.srt`). Carry out the translation in Subtitle Edit via Auto-translate / Auto-translate via Copy-Paste... Select Max block size 5000-10000 on an empty model context. Line separator `@@@`. Save the subtitle file with the `.en` postfix (e.g., `filename.v2.en.srt`).
8.  **Verification**:
    -   Create a hash sum from the audio file using 7z to ensure subtitles exactly match the recording.
    -   View double subtitles in a player like Chrome using the [asbplayer](https://github.com/killergerbah/asbplayer) plugin (can be used as a PWA or locally).
9.  **YouTube Studio Upload**: Upload the finalized subtitles to [YouTube Studio](https://studio.youtube.com). Select the video, go to "Subtitles", add the language, and upload the SRT file "with timing". Optimize and publish.
10. **Learning Integration (Anki)**: Use the **v2** subtitle text to prepare an Anki deck via **Kardenwort**. Process words using the [IntelliFiller AI](https://github.com/voothi/20251206123938-intellifiller-ai-addon-for-anki/tree/main) add-on for automated enrichment of cards.

## Notes
The [aistudio.google.com](https://aistudio.google.com) service is free, but there are limits, and you agree to the use of all data entered into the chat by Google.
