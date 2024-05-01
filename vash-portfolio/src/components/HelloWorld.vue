<script lang="ts">
import { toRefs, reactive, toRef, ref, onMounted } from 'vue'

export default {
  props: {
    msg: String,
  },
  setup(props) {
    const textColorSet = reactive(['hsla(160, 100%, 37%, 1)', 'tomato', 'hsla(160, 100%, 37%, 1)']);
    const texts = reactive(["Aye, Ahoi Mate!", 'I\'m Francis', 'Welcome aboard!']);
    const { msg } = toRefs(props)
    const data = reactive({
      firstName: 'Francis',
      lastName: "Asentista"
    })
    const dataToRef = toRef(data);
    const dataToRefs = toRefs(data);

    onMounted(() => {
      consoleText(texts, textColorSet)
    })

    const onShow = (event: Event, text: string) => {
      console.log(dataToRef.value);
      console.log(dataToRefs);
    }

    const consoleText = (words: string[], colors: string[] = ['#fff']) => {
      let visible: boolean = true;
      let waiting: boolean = false;
      let letterCount: number = 1;
      let x: number = 1;

      const con: HTMLDivElement = document.getElementById('console') as HTMLDivElement;
      const target: HTMLSpanElement = document.getElementById('text-display') as HTMLSpanElement;

      target.setAttribute('style', `color: ${colors[0]}`);

      window.setInterval(() => {
        if (letterCount === 0 && !waiting) {
          waiting = true;
          target.innerHTML = words[0].substring(0, letterCount);
          window.setTimeout(() => {
            const usedColor: any = colors.shift();
            colors.push(usedColor);
            const usedWord: any = words.shift();
            words.push(usedWord);
            x = 1;
            target.setAttribute('style', `color: ${colors[0]}`);
            letterCount += x;
            waiting = false;
          }, 1000);
        } else if (letterCount === words[0].length + 1 && !waiting) {
          waiting = true;
          window.setTimeout(() => {
            x = -1;
            letterCount += x;
            waiting = false;
          }, 1000);
        } else if (!waiting) {
          target.innerHTML = words[0].substring(0, letterCount);
          letterCount += x;
        }
      }, 120);

      window.setInterval(() => {
        if (visible) {
          con.className = 'console-underscore hidden';
          visible = false;
        } else {
          con.className = 'console-underscore';
          visible = true;
        }
      }, 400);
    }

    return {
      message: msg,
      data,
      dataToRefs
    }
  },

}
</script>

<template>
  <div class="greetings">
    <div class='console-container'>
      <span id='text-display'></span>
      <div class='console-underscore' id='console'>&#95;</div>
    </div>
    <h2 class="text-center mb-10">{{ message }}</h2>
    <!-- <h3>
      Fullname: {{ data.firstName }} {{ data.lastName }}<br />
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>. What's next?
    </h3> -->
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
}

h3 {
  font-size: 1.2rem;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
