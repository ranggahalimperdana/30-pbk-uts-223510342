<template>
  <div id="app">
    <nav class="navbar">
      <h1>Tugas Rangga</h1>
      <button @click="navigate('HomePage')" :class="{ active: currentComponent === 'HomePage' }">Tugas UTS Todo list</button>
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
  align-items: center;
  background-color: #333;
  padding: 1rem;
  position: relative;
  flex-wrap: wrap;
}

.navbar h1 {
  flex: 1 1 auto;
  color: salmon;
  font-size: 12px;
  font-weight: bold;
  margin: 0;
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
  flex: 1 1 auto;
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

@media (max-width: 600px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
  }

  .navbar h1 {
    margin-bottom: 1rem;
  }

  .navbar button {
    width: 100%;
    margin: 0.5rem 0;
  }
}
</style>
