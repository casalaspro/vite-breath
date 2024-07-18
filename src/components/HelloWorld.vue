<script>
export default {
  name: 'Timer',
  data() {
    return {
      minutes: 0,
      hours: 0,
      decimals: 0,
      minuteVowel: 'i',
      seconds: 0,
      secondsInterval: null,
      sounds: [
        {
          name: 'Ting',
          source: './src/assets/Ting.mp3'
        },
        {
          name: 'Metronome',
          source: './src/assets/Metronome.mp3'
        },
        {
          name: 'Water Drop',
          source: './src/assets/Drop.mp3'
        },
        {
          name: 'Gong',
          source: './src/assets/Gong_Meditation.mp3'
        },
      ],
        activeSound: 0,
    };
  },
  watch: {
    minutes() {
      this.chengeMinuteVowel();
    }
  },
  methods: {
    chengeMinuteVowel(){
      if(this.minutes === 1){
        this.minuteVowel = 'o';
      }else{
        this.minuteVowel = 'i';
      }
    },
    secondsCountdown(){
      console.log('ciao ', this.seconds);
      this.secondsInterval = setInterval(() => {
        this.seconds-=1;
        this.playSound(this.soundPath);
          console.log('ciao ', this.seconds);
        }, 1000);
    },
    secondsAlarm(seconds){
      let milliseconds = seconds * 1000;
      setTimeout(() => {
        alert('Tempo scaduto!');
        clearInterval(this.secondsInterval);
      }, milliseconds);
      
    },
    playSound(sound){
      if(sound){
        let audio = new Audio(sound);
        audio.play();
      }
    },
    toggleSound(index){
      
    }
  }
};
</script>

<template>
  <section class="timer_section">
    <h2>Mediterai {{ minutes }} minut{{ minuteVowel }}</h2>
  </section>
  <section class="set-timer_section">
    <div class="container">
    <label for="setMinutes" class="form-label">Tempo per la Meditazione</label>
    <input v-model="seconds" type="number" id="setMinutes" class="form-control" aria-describedby="set the meditation minutes">
    <div id="setMinutesHelp" class="form-text mb-3">
      Pesciulini! Imposta quanti minuti vorresti meditare.
    </div>
    <hr class="my-3">
    <div class="sounds-selection">
      <button @click="playSound(sound.source) " v-for="(sound, index) in sounds " class="mx-3 btn btn-light">{{ sound.name }}</button>
    </div>
    <!-- <button @click="secondsAlarm(seconds), secondsCountdown()" class="btn btn-primary">Parti!</button> -->
    <button @click="playSound(soundPath)" class="btn btn-primary">Parti!</button>
  </div>
  </section>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
