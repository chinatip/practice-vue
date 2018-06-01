<template>
  <div>
    <div class="card">
      <div class="card-body">
        <form @submit.prevent="save()">
          <input type="text" v-model="newTodo" class="form-control" aria-label="Small">
          <button class="btn btn-primary" style="margin-top: 10px;">Save</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'inputBox',
  methods: {
    save() {
      this.$emit('save', this.newTodo);
    },
  },
  data() {
    return {
      newTodo: '',
    };
  },
};

</script>

<style>

</style>
