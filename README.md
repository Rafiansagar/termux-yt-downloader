# Install Termux from Playstore 
# Video

1. Full Storage Access
```bash
termux-setup-storage
```
2.
```
pkg update -y
pkg upgrade -y
pkg install python git ffmpeg -y
```
3.
```
pip install --upgrade pip
pip install yt-dlp
```
4.
```
mkdir -p ~/storage/shared/Termux\ Download
mkdir -p ~/storage/shared/Termux\ Download/Video
mkdir -p ~/storage/shared/Termux\ Download/Audio
mkdir -p ~/bin
```
5.
```
# add to ~/.bashrc so it's permanent
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
# apply now
source ~/.bashrc
```
6.
```
nano ~/bin/yt
```
7.
```Sh
#!/data/data/com.termux/files/usr/bin/bash
# yt - interactive video downloader (480p -> 8K)
# Saves to: ~/storage/shared/Termux Download

set -e

echo "Enter YouTube URL:"
read -r URL

if [ -z "$URL" ]; then
  echo "No URL provided. Exiting."
  exit 1
fi

DOWNLOAD_DIR="$HOME/storage/shared/Termux\ Download/Video"

mkdir -p "$DOWNLOAD_DIR"

echo ""
echo "Select video resolution to download:"
echo " 1) 480p"
echo " 2) 720p"
echo " 3) 1080p"
echo " 4) 1440p"
echo " 5) 2160p (4K)"
echo " 6) 4320p (8K)"
echo " 0) Best available (auto)"
echo ""
read -r RES_CHOICE

case "$RES_CHOICE" in
  1) HEIGHT=480 ;;
  2) HEIGHT=720 ;;
  3) HEIGHT=1080 ;;
  4) HEIGHT=1440 ;;
  5) HEIGHT=2160 ;;
  6) HEIGHT=4320 ;;
  0) HEIGHT=0 ;;
  *) echo "Invalid choice. Using best available."; HEIGHT=0 ;;
esac

echo ""
echo "Starting download... this may take a while for high resolutions."
echo "Saving to: $DOWNLOAD_DIR"
echo ""

if [ "$HEIGHT" -eq 0 ]; then
  yt-dlp -f "bestvideo+bestaudio/best" -o "$DOWNLOAD_DIR/%(title)s.%(ext)s" "$URL"
else
  yt-dlp -f "bestvideo[height<=$HEIGHT]+bestaudio/best" -o "$DOWNLOAD_DIR/%(title)s.%(ext)s" "$URL"
fi

echo ""
echo "Download finished! File saved to: $DOWNLOAD_DIR"
```
8.
```
chmod +x ~/bin/
```
9. Run
```
yt
```
# Audio
1.
```
nano ~/bin/yta
```
2.
```Sh
#!/data/data/com.termux/files/usr/bin/bash

echo "Enter YouTube URL:"
read URL

DOWNLOAD_DIR=~/Termux\ Download/Audio

yt-dlp -x --audio-format mp3 -o "$DOWNLOAD_DIR/%(title)s.%(ext)s" "$URL"

echo "Audio download finished! Saved to $DOWNLOAD_DIR"
```
3.
```
chmod +x ~/bin/yta
```
4. Run
```
yta
```

