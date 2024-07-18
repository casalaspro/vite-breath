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
      minutesInterval: null,
      timeout: null,
      interval: 1,
      stopSound: {
        name: 'Stop Gong',
        source: './src/assets/Gong_Stop.mp3',
      },
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
    secondsCountdown(interval){
      // first sound
      this.playSound(this.sounds[this.activeSound].source)
      // calculate milliseconds
      let millisecondsInterval = interval * 1000;
      // set the interval
      this.minutesInterval = setInterval(() => {
        this.playSound(this.sounds[this.activeSound].source);
        }, millisecondsInterval);
    },
    minutesAlarm(minutes){
      // calculate milliseconds
      let milliseconds = minutes * 1000 * 60;
      let modal = document.querySelector('.modal');
      // set timeout
      this.timeout = setTimeout(() => {
        // plays the end sound
        this.playSound(this.stopSound.source);
        // it stops the interval
        clearInterval(this.minutesInterval);
        modal.classList.add('d-block', 'blur');

      }, milliseconds);
      
    },
    closeModal(){
      let modal = document.querySelector('.modal');
      modal.classList.remove('d-block', 'blur');
    },
    stopMeditation(){
      clearInterval(this.minutesInterval);
      clearTimeout(this.timeout);
    },
    playSound(sound){
      if(sound){
        let audio = new Audio(sound);
        audio.play();
      }
    },
    toggleSound(index){
      let buttons = document.querySelectorAll('.btn_sound-selection');
      // console.log(buttons);
      let lastActiveSound = this.activeSound;
      this.activeSound = index;
      if(buttons[lastActiveSound].classList.contains('btn-dark')){
        buttons[lastActiveSound].classList.remove('btn-dark');
        buttons[lastActiveSound].classList.add('btn-outline-dark');
        buttons[this.activeSound].classList.remove('btn-outline-dark');
        buttons[this.activeSound].classList.add('btn-dark');
      }else{
        buttons[lastActiveSound].classList.remove('btn-outline-dark');
        buttons[this.activeSound].classList.add('btn-dark');
      }
    }
  },
  mounted(){
    this.toggleSound(0);
  }
};
</script>

<template>
  <div class="card-border border border-5 rounded-5 p-5">
  <section class="timer_section">
    <h2>Mediterai {{ minutes }} minut{{ minuteVowel }}</h2>
  </section>
  <section class="set-timer_section">
    <div class="container">
    <label for="setMinutes" class="form-label">Tempo per la Meditazione</label>
    <input v-model="minutes" type="number" id="setMinutes" class="form-control" aria-describedby="set the meditation minutes">
    <div id="setMinutesHelp" class="form-text mb-3">
      Pesciulini! Imposta quanti minuti vorresti meditare.
    </div>
    <hr class="my-3">
    <div class="otherSettings mb-3">
      <label for="setInterval" class="form-label">Intervallo Segnale Sonoro</label>
    <input v-model="interval" type="number" id="setInterval" class="form-control" step="0.5" aria-describedby="set the interval seconds">
    </div>
    <div class="sounds-selection my-4">
      <button @click="playSound(sound.source), toggleSound(index) " v-for="(sound, index) in sounds " class="mx-3 btn btn_sound-selection btn-outline-dark">{{ sound.name }}</button>
    </div>
    <div class="buttons_start-stop mt-5">
      <button @click="minutesAlarm(minutes), secondsCountdown(interval)" class="btn mx-3 my_btn-start">START</button>
      <button @click="stopMeditation()" class="btn btn-danger mx-3">STOP</button>
      <!-- <button @click="playSound(soundPath)" class="btn btn-primary">Parti!</button> -->
    </div>
  </div>
  </section>
<div class="my_modal">
  <div class="modal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Meditazione Terminata</h5>
        <button @click="closeModal()" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <p>Bravissima Pescetti!</p>
      </div>
      <div class="modal-footer">
        <button @click="closeModal()" type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</div>

</div>
</template>

<style lang="scss" scoped>
.read-the-docs {
  color: #888;
}
.card-border{
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-color: #d4d4d468;
  position: relative;
}
.my_btn-start{
  background-color: rgb(128, 255, 255);
  
}
.my_btn-start:hover{
  background-color: rgb(24, 181, 181);
  color: white;
}
.modal-dialog{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.blur{
  backdrop-filter: blur(10px);
}


</style>
