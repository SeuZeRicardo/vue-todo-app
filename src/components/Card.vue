
<template>
  <div class='ui centered card'>
    <div class='content' v-show="!isEditing">
      <div class='header'>
        {{ item.title }}
      </div>
      <div class='meta'>
        {{ item.project }}
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
            <i class='edit icon'></i>
          </span>
          <span class='right floated change-status' v-on:click="completedTask" v-show="item.done">
            <i class='check icon'></i>
          </span>
          <span class='right floated change-status' v-on:click="completedTask" v-show="!item.done">
            <i class='exclamation triangle icon'></i>
          </span>
          <span class='right floated delete' v-on:click="deleteAction(item)">
            <i class='trash alternate icon'></i>
          </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Titulo</label>
          <input type='text' v-model="item.title" >
        </div>
        <div class='field'>
          <label>Descrição</label>
          <input type='text' v-model="item.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Fechar
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing && item.done" disabled>
        Completada
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && !item.done">
        Pendente
    </div>
  </div>
</template>

<script>
export default {
  props: ['item'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    completedTask() {
      this.item.done = !this.item.done;
    },
    deleteAction(item) {
      this.$emit('delete', item);
    },
  },
};
</script>
