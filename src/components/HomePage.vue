<template>
  <div>
    <h1>Tugas To do list - UTS</h1>
    <div id="app">
      <div class="todo-container">
        <h1>Todo List</h1>
        <div class="input-container">
          <input v-model="task" @keyup.enter="addTask" placeholder="Add a new task" />
          <button @click="addTask" style="background-color: salmon;">Add</button>
        </div>
        <ul class="todo-list">
          <li v-for="(todo, index) in todos" :key="index" :class="{ completed: todo.completed }">
            <div class="checkbox-container">
              <input type="checkbox" :checked="todo.completed" @change="toggleStatus(index)">
            </div>
            <span>{{ todo.task }}</span>
            <button @click="removeTask(index)" style="background-color: #ff5c5c;">Remove</button>
            <button @click="editTask(index)" style="background-color: skyblue;">Edit</button>
          </li>
        </ul>
        <p>Total unfinished tasks: {{ unfinishedTodosCount }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue';

export default {
  name: 'FirstPage',
  setup() {
    const task = ref('');
    const todos = ref([]);

    const addTask = () => {
      if (task.value.trim()) {
        todos.value.push({ task: task.value.trim(), completed: false });
        task.value = '';
        saveTodos();
      }
    };

    const removeTask = (index) => {
      todos.value.splice(index, 1);
      saveTodos();
    };

    const toggleStatus = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
      const completedTask = todos.value.splice(index, 1)[0];
      const targetIndex = completedTask.completed ? todos.value.length : todos.value.findIndex(todo => !todo.completed);
      todos.value.splice(targetIndex, 0, completedTask);
      saveTodos();
    };

    const editTask = (index) => {
      const newTask = prompt('Edit task:', todos.value[index].task);
      if (newTask !== null) {
        todos.value[index].task = newTask.trim();
        saveTodos();
      }
    };

    const unfinishedTodosCount = computed(() => {
      return todos.value.filter(todo => !todo.completed).length;
    });

    const saveTodos = () => {
      localStorage.setItem('todos', JSON.stringify(todos.value));
    };

    const loadTodos = () => {
      const savedTodos = localStorage.getItem('todos');
      if (savedTodos) {
        todos.value = JSON.parse(savedTodos);
      }
    };

    onMounted(() => {
      loadTodos();
    });

    return {
      task,
      todos,
      addTask,
      removeTask,
      toggleStatus,
      editTask,
      unfinishedTodosCount,
    };
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

h1 {
  font-weight: 300;
}

#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
  background-color: #ffffff;
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.todo-container {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.todo-container h1 {
  font-size: 24px;
  margin-bottom: 20px;
}

.todo-container p {
  font-size: 18px;
  color: #888;
}

.input-container {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-list li {
  display: flex;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
  transition: all 0.3s ease;
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: #888;
}

.todo-list li span {
  flex-grow: 1;
  margin-left: 10px;
}

.checkbox-container {
  flex: 0 0 30px;
  display: flex;
  justify-content: center;
}

input[type="checkbox"] {
  cursor: pointer;
}

input[type="checkbox"]:checked {
  accent-color: orange;
}

.todo-list button {
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  background-color: #ff5c5c;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

.todo-list button:hover {
  background-color: #ff1a1a;
}

h1{
  font-size: 30px bold;
  text-align: center;
  color: salmon;
}
</style>
