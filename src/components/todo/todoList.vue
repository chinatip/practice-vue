<template>
  <div class="card">
    <div v-for="todo in sortedTodo" :key="todo.time" class="list-group list-group-flush">
      <div style="display: flex; margin: 5px;">
        <input type="text"
          class="list-group-item"
          :class="todo.completed? {done: true}: {wait: true}"
          v-model="todo.text"
          @change="update(todo.time, 'text')"
          style="width: 100%; margin-right: 10px;"
        >
        <div style="flex: 1; display: flex; justify-content: flex-end; margin-right: 20px;">
          <button class="btn btn-warning" @click="update(todo.time, 'status')">Change</button>
          <button class="btn btn-danger"
            @click="update(todo.time, 'remove')"
            style="margin-left: 10px;"
          >
            X
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import lodash from 'lodash';

export default {
  name: 'todoList',
  props: ['todos'],
  computed: {
    sortedTodo() {
      return lodash.sortBy(this.todos, t => t.text);
    },
  },
  methods: {
    update(time, type) {
      this.$emit('update', time, type);
    },
  },
};
</script>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
