---
title: how to make your own music player
published: 2024-09-22 18:08:00
description: 'a guide on how to make your own music player using javascript'
tags: [music, guide, javascript]
category: Programming
---

so you want to make your own music player? well, you've come to the right place! in this guide, i'll show you how to make a simple music player using javascript. let's get started!

## step 1: create the html

```html
<div>
  <audio id="audio" controls>
    <source src="music.mp3" type="audio/mpeg">
    your browser does not support the audio element.
  </audio>
  <div class="metadata">Not Playing.</div>
  <button id="play">play</button>
  <button id="pause">pause</button>
  
  <script src="./music-player.js">
    [
      {
        "name": "my song",
        "artist": "my artist",
        "url": "music.mp3"
      }
    ]
  </script>
</div>
```

so in this step, we create the html for our music player. we have an `audio` element with an `id` of `audio` that will be used to play the music. we also have a `div` element with a `class` of `metadata` that will display the current playing song. we also have two buttons, one with an `id` of `play` and the other with an `id` of `pause` that will be used to play and pause the music.

## step 2: create the javascript

```javascript
// get the current script element and its parent
const currentScript = document.currentScript;
const parent = currentScript.parentElement;

const audio = parent.querySelector('#audio');
const metadata = parent.querySelector('.metadata');
const playButton = parent.querySelector('#play');
const pauseButton = parent.querySelector('#pause');

// get the songs, aka the content of the script tag
const songs = JSON.parse(currentScript.textContent);

let currentIndex = 0;

// set the metadata to the current song
function setMetadata() {
  metadata.textContent = `${songs[currentIndex].name} - ${songs[currentIndex].artist}`;
}
setMetadata();

// play the current song
function play() {
  audio.src = songs[currentIndex].url;
  audio.play()
    .catch(() => {
      // if the audio cannot play, wait till the user clicks the window
      window.addEventListener('click', () => {
        audio.play();
      }, { once: true });
    });
  setMetadata();
}

// pause the current song
function pause() {
  audio.pause();
}

// play the next song
function next() {
  currentIndex = (currentIndex + 1) % songs.length;
  play();
}

// play the previous song
function previous() {
  currentIndex = (currentIndex - 1 + songs.length) % songs.length;
  play();
}

// add event listeners to the play and pause buttons
playButton.addEventListener('click', play);
pauseButton.addEventListener('click', pause);

// add event listeners to the audio element
audio.addEventListener('ended', next);
```

in this step, we create the javascript for our music player. we get the current script element and its parent, then we get the audio element, metadata element, play button, and pause button. we also get the songs from the content of the script tag and set the metadata to the current song.

we then create functions to play, pause, play the next song, and play the previous song. we add event listeners to the play and pause buttons and the audio element to play the next song when the current song ends.

## challenge!!

you don't need to do all of these, but if u want you can...

- add a progress bar to show the current progress of the audio element.
- add a volume control to adjust the volume of the audio element.
- add a shuffle button to shuffle the songs.
- style the music player to make it look nice.

## conclusion

and that's it! you've successfully created your own music player using javascript. feel free to customize it further to suit your needs. happy coding! 🎵🎶