<template>
  <div>
    <h2>semua fitur masih dalam pengembangan</h2>
    <h2>Semau Codingan saya berantakanan & Error saya akan menggukanan fitur branch di git agar saya bisa <br>
    membuat tugas secara terpisah dan kemudian hasil nya saya akan upload tugasnya  secepat mungkin</h2>
    <h1>Filter Posts by User</h1>
    <select v-model="selectedUserName">
      <option value="">-- Select User Name --</option>
      <option v-for="user in availableUsers" :key="user.id" :value="user.name">{{ user.name }}</option>
    </select>
    <button @click="filterPosts">Filter</button>

    <h1>Post ID</h1>
    <p v-if="selectedPostId">Post ID: {{ selectedPostId }}</p>
    <p v-else>No post ID selected.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      availableUsers: [
        { id: 1, name: "Leanne Graham" },
        { id: 2, name: "Ervin Howell" },
        { id: 3, name: "Clementine Bauch" },
        // tambahkan nama pengguna lainnya di sini
      ],
      posts: [],
      selectedUserName: '',
      selectedPostId: null
    };
  },
  computed: {
    filteredUser() {
      return this.availableUsers.find(user => user.name.toLowerCase() === this.selectedUserName.toLowerCase());
    }
  },
  methods: {
    async fetchPosts() {
      const response = await fetch("https://jsonplaceholder.typicode.com/posts");
      this.posts = await response.json();
    },
    filterPosts() {
      if (this.filteredUser) {
        this.selectedPostId = this.filteredUser.id;
      } else {
        this.selectedPostId = null;
      }
    }
  },
  created() {
    this.fetchPosts();
  }
};
</script>
