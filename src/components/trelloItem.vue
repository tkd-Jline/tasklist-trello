<template>

  <div class="category-tasks"
    v-for="(task, index) in category.tasks"
    :key="index"
    draggable= "true"
    @dragstart="dragTask(task)"
    @dragover="dragOverTask(task)"
  >
    {{task.name}}
  </div>

</template>

<script>

  export default {

    name: "TrelloItem",

    data(){
      return {
        task: "",
      }
    },

    props: {
      category: {
        type: Object
      }

    },

    methods: {

      dragTask(task){
        this.$emit("dragstart",task);
      },

      dragOverTask(overtask){
        this.$emit("dragover",overtask);
      }

    }

  }

</script>

<style scoped>

  .category-tasks {
    background: #fff;
    margin: 5px;
    padding: 5px 10px;
  }

</style>
