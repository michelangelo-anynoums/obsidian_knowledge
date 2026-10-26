## 📺 Introduction to **pytube** (Python)

**pytube** is a lightweight Python library for downloading YouTube videos. It lets you:

- Access video metadata (title, views, length, etc.)
    
- List available video/audio streams
    
- Download videos in different resolutions or audio-only formats
    

> ⚠️ Note: Because YouTube frequently changes its internals, `pytube` may occasionally break. If that happens, upgrading the library usually fixes it.

---

## 📦 Installation

Install `pytube` using pip:

```Python
pip install pytube
```

(Optional but recommended)

```Python
pip install --upgrade pytube
```

---

## 🚀 Basic Usage

### Creating a YouTube object

```Python
from pytube import YouTube  

url = "https://www.youtube.com/watch?v=VIDEO_ID" 
yt = YouTube(url)  

print(yt.title) 
print(yt.author) 
print(yt.length) # duration in seconds
print(yt.views)
```

---

### Listing Available Streams

Each YouTube video has multiple **streams** (different resolutions, formats, audio-only, etc.).

```Python
for stream in yt.streams:     
	print(stream)
```

Common filters:

```Python
yt.streams.filter(progressive=True) # video + audio 
yt.streams.filter(only_audio=True) # audio only
yt.streams.filter(file_extension="mp4") # extension
```

---

## ⬇️ Downloading YouTube Videos

### 1️⃣ Download the Highest Resolution (Video + Audio)

```Python
stream = yt.streams.get_highest_resolution() 
stream.download()
```

By default, the video is saved in the **current directory**.

---

### 2️⃣ Download to a Specific Folder

```Python
stream.download(output_path="downloads/")
```

---

### 3️⃣ Download a Specific Resolution (e.g., 720p)

```Python
stream = yt.streams.filter(progressive=True,file_extension="mp4",res="720p").first()  
stream.download()
```

---

### 4️⃣ Download Audio Only (MP3-like)

```Python
audio_stream = yt.streams.filter(only_audio=True).first() 
audio_stream.download(output_path="audio/")
```

> 💡 This downloads audio as `.mp4` or `.webm`. You can later convert it to MP3 using tools like `ffmpeg`.

---

### 5️⃣ Rename the Downloaded File

```Python
stream.download(filename="my_video.mp4")
```

---

## 🛠 Helpful Extras

### Handle Errors Gracefully

```Python
from pytube import YouTube 
from pytube.exceptions import PytubeError  

try:     
	yt = YouTube(url)     
	yt.streams.get_highest_resolution().download() 
except PytubeError as e:     
	print("Download failed:", e)
```

----


Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]