<script setup lang="ts">
import { ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import PhotoMe from './assets/me.jpg'

const subtitle = ref("Hi, I\’m Francis, a passionate front-end developer specializing in JavaScript and Vue.js. With a keen eye for clean design and seamless user experiences, I’ve crafted responsive web applications and dynamic interfaces. I thrive on turning ideas into interactive reality. Whether it’s mastering a new framework or adapting to evolving technologies, I’m always up for the challenge. Let’s build something amazing together!");
</script>

<template>
  <header>
    <div class="wrapper">
      <div class="avatar-holder">
        <img :src="PhotoMe" class="rounded-[50px] w-3/4" alt="me" />
      </div>

      <HelloWorld :msg="subtitle" />

      <nav class="flex justify-center">
        <RouterLink to="/">
          <div class="box-1">
            <div class="btn btn-one">
              <span>Home</span>
            </div>
          </div>
        </RouterLink>
        <RouterLink to="/bio">
          <div class="box-1">
            <div class="btn btn-one">
              <span>Biography</span>
            </div>
          </div>
        </RouterLink>
        <RouterLink to="/exp">
          <div class="box-1">
            <div class="btn btn-one">
              <span>Experiences</span>
            </div>
          </div>
        </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
