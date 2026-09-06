**Audio Files in Browser with JavaScript:**

You can play and manipulate audio in a web browser using JavaScript through the ==**HTML5 audio
element.**== This element allows you to embed audio files (like MP3, WAV, or Ogg) directly into web pages. JavaScript can interact with the audio through the **Audio API**, giving you control over playback, volume, loops, and more.

### Key Methods & Properties:

- **play()**: Starts playback of the audio.
    
- **pause()**: Pauses the audio.
    
- **currentTime**: Gets or sets the current position (in seconds) of the audio.
    
- **volume**: Sets the volume (0.0 to 1.0).
    
- **loop**: A boolean to make the audio loop automatically.
    

### Example:

```Html
<audio id="myAudio" src="audiofile.mp3" preload="auto"></audio> 
<script>  

	const audio = document.getElementById('myAudio');   
	audio.play(); // Play the audio 

</script>
```

With JavaScript, you can also use the **Web Audio API** for more complex audio processing, like creating custom sound effects or analyzing audio data in real-time.


---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[JavaScript introduction]]