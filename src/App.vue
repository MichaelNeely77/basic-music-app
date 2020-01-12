<template>
  <div id="app">
    <header>
      <h1>
        My Music Application
      </h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" class="(song.src == current.src) ? 'song playing' : 'song'">
            {{ song.title }} - {{ song.artist }}
          </button>
        </h3>
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'app',
  data () {
    return {
      current: {
        
      },
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Extreme Action',
          artist: 'Bensound',
          src: require('./assets/bensound-extremeaction.mp3')

        },
        {
          title: 'Happy Rock',
          artist: 'Happy Rocker',
          src: require('./assets/bensound-happyrock.mp3')
        },
        {
          title: 'High Octane',
          artist: 'Heavy Stuff',
          src: require('./assets/bensound-highoctane.mp3')
        },
        {
          title: 'Punky Stuff',
          artist: 'Your Problem Band',
          src: require('./assets/bensound-punky.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    prev () {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length -1;
        }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
        next () {
      this.index++;
      if (this.index > this.songs.length -1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;

  }
}
</script>

<style>

 * {
   margin: 0;
  padding: 0;
  box-sizing: border-box;
  }
  body {
    font-family: 'Montserrat', sans-serif;
  }

  header {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 15px;
    background-color: #212121;
    color: #fff;
  }
</style>
