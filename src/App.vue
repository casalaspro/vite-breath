<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  data() {
    return {
     
    };
  },
  watch: {
   
  },
  methods: {
    
  },
  components: {
    HelloWorld
  }
};
</script>

<template>
  
  <HelloWorld />
</template>

<style lang="scss">
@use './scss/general.scss';


.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
