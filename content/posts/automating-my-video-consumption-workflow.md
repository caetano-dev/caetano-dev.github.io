+++
title = "Automating my video consumption workflow with code"
date = "2025-02-06T12:30:10-03:00"
author = "Pedro Caetano"
tags = ["Entertainment", "Media", "Scripting", "Automation"]
keywords = ["Videos", "Series", "MPV", "Golang, Automation", "Scripting"]
description = "How I use code to manage the series and YouTube videos I watch across my computer, phone and TV"
showFullContent = false
readingTime = true
hideComments = false
+++

## Managing shows

Every vacation, I decide to pick a few shows to watch. I like to have all of them downloaded on my computer so that I can manage their files better. This is good for content ownership since Netflix and other streaming services can remove shows at any time. However, managing all these files can be a pain, especially when you have to deal with different devices like your phone and TV. To me, the only point of paying for a streaming service is the convenience of being able to watch content wherever you are and not having to keep track of what episodes you have already watched.

I wanted to have a workflow where I could download all the episodes of a show, watch them on any device, and have my progress synced at least on my computer, so I decided to write some code to help me with that. Here's how I did it:

I created a Go application I decided to call **Lazywatch**. It is a CLI tool that automatically keeps track of the next episode on the list and opens it in MPV. It also identifies and selects the folder containing the next season of the show I am watching.

Here is how it works for my use case:

1. I put all my shows inside a folder called "Torrents" on my computer, and each show has its own folder inside it. For example, "Torrents/Shrinking", "Torrents/Pluribus", etc.
2. When I want to watch a show, I run the command `watch` in my terminal. The application will look for the configuration file. If it doesn't find one, it will ask me to select the parent directory of the show I want to watch and create the configuration file with the path to that show.
3. The application will ask for the next episode to watch. It will then open that episode in MPV and mark it as watched in the configuration file. Calling `watch` again will open the next episode in the list, and so on. When I finish a season, it will automatically select the next season folder.
4. When I am done and want to switch to another show, I can call `watch configure` and run the configuration process again.

You can find the code for this application in my GitHub repository:

[https://github.com/caetano-dev/Lazywatch](https://github.com/caetano-dev/Lazywatch)

Now, how do I watch the shows on my phone and TV? I have a smart LG TV that supports DLNA. I use a DLNA server called MiniDLNA to share the "Torrents" folder on my network. This way, I can access the shows from my TV and phone using any DLNA client, like the default media player from my TV or VLC on my phone.

### Setting up the MiniDLNA server

Since I am running Linux, setting up the server was straightforward. Here is the process I followed:

First, I installed the package (on Debian/Ubuntu systems):

```bash
sudo apt update
sudo apt install minidlna

```

Next, I edited the configuration file located at `/etc/minidlna.conf`. The most important lines to change are the media directories (where the files are stored) and the friendly name (how the server appears on the TV).

```bash
sudo vim /etc/minidlna.conf

```

Inside the file, I added my "Torrents" directory:

```ini
# V for Video. You can also use A for Audio or P for Pictures.
media_dir=V,/home/username/Downloads/Torrents

# Name of the server as seen by the TV/Phone
friendly_name=My Media Server

# Ensure the database updates automatically when I add new files
inotify=yes

```

After saving the changes, I restarted the service to apply them:

```bash
sudo systemctl restart minidlna

```

Now, the "Torrents" folder appears automatically on my local network devices. The only downside is that I have to manually keep track of which episode I am watching on those devices, but at least I can watch the shows without having to transfer files or use a streaming service.

## Managing YouTube videos

I also use a similar workflow to manage the YouTube videos I want to watch. I like to keep all the videos I want to watch downloaded in my Videos folder. I have created a bash yt-dlp wrapper that downloads the video, strips emojis from the titles, saves it to my Videos and Torrents folder (in case I want to watch it on the TV), and downloads a 480p version for me to watch on my phone. I do this because my media consumption phone is a really cheap one. It cannot handle 1080p videos.

Here is the full script:

```bash
#!/bin/bash

YTDLP_BINARY="./Vidéos/yt-dlp"
# Defined target directory (Assumed ~/ based on standard Linux paths)
TORRENT_DIR="$HOME/Téléchargements/Torrents"

if [ -z "$1" ]; then
  echo "Error: No search query or URL provided."
  echo "Usage: $0 <video_title_or_url>"
  exit 1
fi

if [ ! -x "$YTDLP_BINARY" ]; then
    echo "Error: yt-dlp binary not found or not executable at '$YTDLP_BINARY'."
    exit 1
fi

# Ensure the Torrents directory exists
mkdir -p "$TORRENT_DIR"

# If the input doesn't look like a URL, prepend ytsearch1:
if [[ ! "$1" =~ ^http ]]; then
    SEARCH_QUERY="ytsearch1:$1"
    echo "Searching YouTube for: $1"
else
    SEARCH_QUERY="$1"
fi

# Metadata replacement to remove emojis (non-ASCII)
EMOJI_REMOVAL="--replace-in-metadata title '[^\x00-\x7f]' ''"

# Command to copy the downloaded file to the Torrents folder
COPY_CMD="--exec \"cp {} '$TORRENT_DIR'\""

echo "Attempting to download in 1080p"

# Use eval to handle the dynamic search query and metadata flags
# Added COPY_CMD to ensure the file is copied after download
eval "\"$YTDLP_BINARY\" $EMOJI_REMOVAL -P \"Vidéos\" -f \"bestvideo[height=1080]+bestaudio/best[height=1080]\" --merge-output-format mp4 $COPY_CMD \"$SEARCH_QUERY\""

if [ $? -ne 0 ]; then
  echo
  echo "1080p format not available or search failed. Falling back to best available."
  echo
  # Added COPY_CMD here as well so the fallback is also copied
  eval "\"$YTDLP_BINARY\" $EMOJI_REMOVAL -P \"Vidéos\" --merge-output-format mp4 $COPY_CMD \"$SEARCH_QUERY\""
fi

echo
echo "Downloading 480p version to Torrents folder..."

# 480p Download: Directed to TORRENT_DIR with specific naming prefix
# Added a fallback to 'best[height=480]' in case separate video/audio streams aren't available at that res
eval "\"$YTDLP_BINARY\" $EMOJI_REMOVAL -P \"$TORRENT_DIR\" -o \"480p%(title)s.%(ext)s\" -f \"bestvideo[height=480]+bestaudio/best[height=480]/best[height=480]\" --merge-output-format mp4 \"$SEARCH_QUERY\""

echo "Download process finished."

```

If you are going to copy it, just make sure to change the paths to the yt-dlp binary and the target directory where you want to save the videos. You also need to have yt-dlp installed and make it executable.
