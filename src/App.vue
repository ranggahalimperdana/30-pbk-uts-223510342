<template>
  <div id="app">
    <nav class="navbar">
      <button @click="navigate('HomePage')" :class="{ active: currentComponent === 'HomePage' }">Halaman Utama</button>
      <button @click="navigate('FirstPage')" :class="{ active: currentComponent === 'FirstPage' }">Halaman Pertama</button>
      <button @click="navigate('SecondPage')" :class="{ active: currentComponent === 'SecondPage' }">Halaman Kedua</button>
    </nav>
    <main>
      <component :is="currentComponent" @navigate="navigate"></component>
    </main>
  </div>
</template>

<script>
import HomePage from './components/HomePage.vue';
import FirstPage from './components/FirstPage.vue';
import SecondPage from './components/SecondPage.vue';

export default {
  name: 'App',
  components: {
    HomePage,
    FirstPage,
    SecondPage
  },
  data() {
    return {
      currentComponent: 'HomePage'
    };
  },
  methods: {
    navigate(component) {
      this.currentComponent = component;
    }
  }
};
</script>

<style>
body {
  font-family: 'Poppins', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.navbar {
  display: flex;
  justify-content: center;
  background-color: #333;
  padding: 1rem;
}

.navbar button {
  background: none;
  border: none;
  color: white;
  padding: 1rem;
  margin: 0 0.5rem;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s;
}

.navbar button:hover,
.navbar button.active {
  background-color: #555;
}

main {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}
</style>
