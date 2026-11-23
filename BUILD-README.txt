# Bandcamp Downloader V3 — patched build files

Included:
- `BandcampDownloader.py` — patched source; the existing GUI and settings/queue/history implementation are retained.
- `requirements.txt` — yt-dlp 2026.10.26 and PyInstaller build dependencies.
- `.github/workflows/build-windows.yml` — GitHub Actions cloud build for a single Windows EXE.

## Changes
1. Updates yt-dlp to stable `2026.10.26`.
2. Installs yt-dlp's `default` optional dependencies, including curl-cffi.
3. Uses Firefox impersonation for Bandcamp requests, a currently reported workaround for client-challenge responses.
4. Changes `ignoreerrors` to `False`.
5. Marks missing extraction results and empty album track lists as errors rather than successful downloads.
6. Changes the app version to 3.0.1.

The existing Tkinter interface, queue, settings keys, output naming options, FFmpeg option, and history implementation are otherwise unchanged.

## Build without installing Python on your laptop
1. Open https://github.com/ElanMiles/Bandcamp-Downloader.
2. Sign in to GitHub and click **Fork** to create your own copy. You cannot push changes to the original author's repository.
3. In your fork, choose **Add file → Upload files**. Upload this package's `BandcampDownloader.py` and `requirements.txt`, replacing the existing source file when prompted.
4. Create `.github/workflows/build-windows.yml` in your fork and paste the contents of the workflow file included here.
5. Commit the changes to the `main` branch.
6. Open the **Actions** tab. If asked, enable GitHub Actions.
7. Open **Build portable Windows EXE** and wait for the run to finish successfully.
8. Open that workflow run. Under **Artifacts**, download `bandcamp-downloader-v3-windows`.
9. Extract the downloaded ZIP. It contains `bandcamp.downloader.v3.exe`.

The cloud runner installs Python and builds the EXE. Python is not installed on your computer.

## FFmpeg
FFmpeg is not bundled into this EXE. Your existing installation can continue to be used. In Settings, set FFmpeg Path to:

`C:\Users\Aliyana\Downloads\Ffmpeg\bin\ffmpeg.exe`

Save settings and use **Test FFmpeg**. On another computer, that absolute path may differ; select that computer's existing `ffmpeg.exe`. The application itself remains a single EXE, but audio conversion still requires FFmpeg.

## First test
Test one Bandcamp track or album that you purchased or are otherwise authorized to download before adding a large batch. Confirm that the expected audio file appears in the selected folder. Failed extraction should now appear as `Error`, not `Complete`.

Firefox impersonation is a compatibility workaround, not a guarantee. Bandcamp can change its challenge system, and some releases may have restrictions or no downloadable tracks.

## Notes
- The repository is public, so source can be viewed/downloaded without signing in. Creating a fork and running your own GitHub Actions build requires a GitHub account.
- This workflow does not change the original author's repository.
- Existing configuration remains in the user's home profile under `.bandcamp_downloader`.
- The current source keeps history in memory for the running session; this patch does not add persistent history storage.
- Review the repository's MIT license before redistributing modified builds.
