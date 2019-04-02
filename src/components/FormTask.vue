<template>
  <div class='ui left card'>
    <div class='content'>
      <div class='header'>
        <p>Crie uma nova Tarefa</p>
      </div>
      <div class="content">
        <div class='ui form'>
          <div class='field'>
            <label>Titulo</label>
            <input type='text' v-model="newTask.title">
          </div>
          <div class='field'>
            <label>Descrição</label>
            <input type='text' v-model="newTask.project">
          </div>
          <div class='ui attached buttons'>
            <button class='ui bottom attached green basic button' v-on:click="createTask">
              Criar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: {
        title: '',
        project: '',
        done: false,
      },
    };
  },
  methods: {
    createTask() {
      if (this.newTask.title.length > 0 && this.newTask.project.length > 0) {
        this.$emit('add', { ...this.newTask });
      } else {
        alert('Campos Vazios');
      }
      this.newTask.title = '';
      this.newTask.project = '';
    },
  },
};
</script>
