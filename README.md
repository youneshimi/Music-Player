## Music Player
Le projet Music Player est une application Web développée sur la plate-forme javascript .Il s'agit d'un petit projet de niveau simple et basique à des fins d'apprentissage.
## script.js

```ts
const cover = document.getElementById('cover');
const disc = document.getElementById('disc');
const title = document.getElementById('title');
const artist = document.getElementById('artist');
const progressContainer = document.getElementById('progress-container');
const progress = document.getElementById('progress');
const timer = document.getElementById('timer');
const duration = document.getElementById('duration');
const prev = document.getElementById('prev');
const play = document.getElementById('play');
const next = document.getElementById('next');
let songIndex = 0;
const songs = [
  {
    title: 'Sacrifice',
    artist: 'the Weeknd',
    coverPath: 'assets/images/cover1.jpg',
    discPath: 'assets/music/music1.mp3',
    duration: '1:33',
  },
  {
    title: 'Heat Waves',
    artist: 'Glass Animals',
    coverPath: 'assets/images/cover2.jpg',
    discPath: 'assets/music/music2.mp3',
    duration: '2:22',
  },
  {
    title: 'Ed Sheeran',
    artist: 'Bad Habits',
    coverPath: 'assets/images/cover3.jpg',
    discPath: 'assets/music/music3.mp3',
    duration: '1:54',
  },
];

loadSong(songs[songIndex]);

function loadSong(song) {
  cover.src = song.coverPath;
  disc.src = song.discPath;
  title.textContent = song.title;
  artist.textContent = song.artist;
  duration.textContent = song.duration;
}

function playPauseMedia() {
  if (disc.paused) {
    disc.play();
  } else {
    disc.pause();
  }
}

function updatePlayPauseIcon() {
  if (disc.paused) {
    play.classList.remove('fa-pause');
    play.classList.add('fa-play');
  } else {
    play.classList.remove('fa-play');
    play.classList.add('fa-pause');
  }
}

function updateProgress() {
  progress.style.width = (disc.currentTime / disc.duration) * 100 + '%';

  let minutes = Math.floor(disc.currentTime / 60);
  let seconds = Math.floor(disc.currentTime % 60);
  if (seconds < 10) {
    seconds = '0' + seconds;
  }
  timer.textContent = `${minutes}:${seconds}`;
}

function resetProgress() {
  progress.style.width = 0 + '%';
  timer.textContent = '0:00';
}

// Go to previous song
function gotoPreviousSong() {
  if (songIndex === 0) {
    songIndex = songs.length - 1;
  } else {
    songIndex = songIndex - 1;
  }

  const isDiscPlayingNow = !disc.paused;
  loadSong(songs[songIndex]);
  resetProgress();
  if (isDiscPlayingNow) {
    playPauseMedia();
  }
}
function gotoNextSong(playImmediately) {
  if (songIndex === songs.length - 1) {
    songIndex = 0;
  } else {
    songIndex = songIndex + 1;
  }

  const isDiscPlayingNow = !disc.paused;
  loadSong(songs[songIndex]);
  resetProgress();
  if (isDiscPlayingNow || playImmediately) {
    playPauseMedia();
  }
}
function setProgress(ev) {
  const totalWidth = this.clientWidth;
  const clickWidth = ev.offsetX;
  const clickWidthRatio = clickWidth / totalWidth;
  disc.currentTime = clickWidthRatio * disc.duration;
}

play.addEventListener('click', playPauseMedia);
disc.addEventListener('play', updatePlayPauseIcon);
disc.addEventListener('pause', updatePlayPauseIcon);
disc.addEventListener('timeupdate', updateProgress);
disc.addEventListener('ended', gotoNextSong.bind(null, true));
prev.addEventListener('click', gotoPreviousSong);
next.addEventListener('click', gotoNextSong.bind(null, false));
progressContainer.addEventListener('click', setProgress);

```

> Informations sur les chansons

```ts
const songs = [
  {
    title: 'Sacrifice',
    artist: 'the Weeknd',
    coverPath: 'assets/images/cover1.jpg',
    discPath: 'assets/music/music1.mp3',
    duration: '1:33',
  },
  {
    title: 'Heat Waves',
    artist: 'Glass Animals',
    coverPath: 'assets/images/cover2.jpg',
    discPath: 'assets/music/music2.mp3',
    duration: '2:22',
  },
  {
    title: 'Ed Sheeran',
    artist: 'Bad Habits',
    coverPath: 'assets/images/cover3.jpg',
    discPath: 'assets/music/music3.mp3',
    duration: '1:54',
  },
];
```
> Charger la chanson initialement
```ts

loadSong(songs[songIndex]);
```

> Charge la chanson donnée

```ts

function loadSong(song) {
  cover.src = song.coverPath;
  disc.src = song.discPath;
  title.textContent = song.title;
  artist.textContent = song.artist;
  duration.textContent = song.duration;
}
```

> Basculer la lecture et la pause
```ts

function playPauseMedia() {
  if (disc.paused) {
    disc.play();
  } else {
    disc.pause();
  }
}
```


> Mettre à jour l'icône

```ts

function updatePlayPauseIcon() {
  if (disc.paused) {
    play.classList.remove('fa-pause');
    play.classList.add('fa-play');
  } else {
    play.classList.remove('fa-play');
    play.classList.add('fa-pause');
  }
}
```


> Mettre à jour la barre de progression

```ts

function updateProgress() {
  progress.style.width = (disc.currentTime / disc.duration) * 100 + '%';

  let minutes = Math.floor(disc.currentTime / 60);
  let seconds = Math.floor(disc.currentTime % 60);
  if (seconds < 10) {
    seconds = '0' + seconds;
  }
  timer.textContent = `${minutes}:${seconds}`;
}
```

> Play/Pause when play button clicked

play.addEventListener('click', playPauseMedia);
```
> Various events on disc
disc.addEventListener('play', updatePlayPauseIcon);
disc.addEventListener('pause', updatePlayPauseIcon);
disc.addEventListener('timeupdate', updateProgress);
disc.addEventListener('ended', gotoNextSong.bind(null, true));

```
> Aller à la chanson suivante lorsque le bouton suivant est cliqué
```ts

prev.addEventListener('click', gotoPreviousSong);
```
> Aller à la chanson précédente lorsque le bouton précédent a été cliqué
```ts

next.addEventListener('click', gotoNextSong.bind(null, false));
```
> Déplacer à un endroit différent dans la chanson

```ts

progressContainer.addEventListener('click', setProgress);

```


## index.html

```ts
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      rel="stylesheet"
      href="https://use.fontawesome.com/releases/v5.15.1/css/all.css"
      integrity="sha384-vp86vTRFVJgpjF9jiIGPEEqYqlDwgyBgEF109VFjmqGmIY/Y4HV4d3Gp2irVfcrp"
      crossorigin="anonymous"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Montserrat&family=Poppins:wght@300;400;500;600;700;800;900&display=swap"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="assets/styles/style.css" />
    <title>Music Player</title>
  </head>
  <body>
    <div class="container">
      <h1 class="heading">Music Player</h1>
      <div class="music-container">
        <div id="cover-box">
          <img src="assets/images/cover1.jpg" alt="cover-image" id="cover" />
        </div>
        <div id="music-box">
          <audio id="disc"></audio>
          <div id="music-info">
            <h2 id="title"></h2>
            <h3 id="artist"></h3>
            <div id="progress-container">
              <div id="progress"></div>
            </div>
            <div id="timer-bar">
              <span id="timer">0:00</span>
              <span id="duration"></span>
            </div>
          </div>
          <div id="control-box">
            <i id="prev" class="btn fas fa-backward"></i>
            <i id="play" class="special-btn fas fa-play"></i>
            <i id="next" class="btn fas fa-forward"></i>
          </div>
        </div>
      </div>
    </div>
    <script src="assets/scripts/script.js"></script>
  </body>
</html>

```
![Capture d’écran 2022-02-06 033643](https://user-images.githubusercontent.com/96379214/152665755-fb7c5393-48f5-4365-84c8-2a7eb2e0311f.png)


![player](https://user-images.githubusercontent.com/96379214/152665769-2a84d27b-c995-4810-bf2f-52855adfc272.gif)
