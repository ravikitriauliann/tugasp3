<template>
  <div class="app">
    <h1>Membuat Daftar Kegiatan</h1>
    <div class="input-container">
      <input
        type="text"
        v-model="newItem"
        placeholder="Tulis disini"
        @keyup.enter="addItem"
      />
      <button @click="addItem">Add</button>
    </div>
    <div class="filter-container">
      <button @click="filter = 'all'">All</button>
      <button @click="filter = 'completed'">Completed</button>
      <button @click="filter = 'incomplete'">Incomplete</button>
    </div>
    <ul class="todo-list">
      <li
        v-for="(item, index) in filteredItems"
        :key="index"
        :class="{ completed: item.completed }"
      >
        <div
          class="item-container"
          :style="{ opacity: item.completed ? 0.5 : 1 }"
        >
          <span>{{ index + 1 }}. {{ item.text }}</span>
          <div class="button-container">
            <button @click="toggleCompleted(index)">
              {{ item.completed ? "Undo" : " Done" }}
            </button>
            <button @click="editItem(index)">Edit</button>
            <button @click="deleteItem(index)">Delete</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: "",
      items: [],
      filter: "all",
    };
  },
  computed: {
    filteredItems() {
      if (this.filter === "completed") {
        return this.items.filter((item) => item.completed);
      } else if (this.filter === "incomplete") {
        return this.items.filter((item) => !item.completed);
      } else {
        return this.items;
      }
    },
  },
  methods: {
    addItem() {
      if (this.newItem.trim() !== "") {
        this.items.push({ text: this.newItem, completed: false });
        this.newItem = "";
      }
    },
    editItem(index) {
      const newText = prompt("Edit the item:", this.items[index].text);
      if (newText !== null && newText.trim() !== "") {
        this.items[index].text = newText;
      }
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
    toggleCompleted(index) {
      this.items[index].completed = !this.items[index].completed;
    },
  },
};
</script>

<style scoped>
.app {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #cf64f3;
  border-radius: 15px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  color: #02ff6b;
  margin-bottom: 30px;
  font-weight: bold;
}

.input-container {
  margin-bottom: 20px;
}

input[type="text"] {
  width: 70%;
  padding: 12px;
  border: none;
  border-radius: 8px 0 0 8px;
  font-size: 16px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

button {
  padding: 12px 20px;
  border: none;
  background-color: #2ecc71;
  color: white;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #27ae60;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 15px;
  background-color: #fff;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.completed {
  text-decoration: line-through;
  color: black;
}

.item-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.button-container button {
  margin-left: 10px;
  background-color: #fc6ed4;
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.button-container button:hover {
  background-color: #f78ee9;
}

span {
  color: #c73ef5;
  font-weight: bolder;
}

.filter-container {
  margin-bottom: 20px;
}

.filter-container button {
  margin-right: 10px;
}
</style>
