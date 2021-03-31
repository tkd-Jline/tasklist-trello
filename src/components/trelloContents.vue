<template>

  <section class="trello-contents">

    <div 
      class="trello-part"
      v-for="(category,index) in displayCategories"
      :key="index"
      draggable="true"
    >

    <div class="category-name">
      {{category.name}}
    </div>

    <trello-item
      :category="category"
      @dragstart="dragstart"
      @dragover="dragover"
    ></trello-item>

    </div>

  </section>

</template>

<script>

  import TrelloItem from './trelloItem.vue';

  export default {

    name: "TrelloContents",

    components: {
      TrelloItem,
    },

    props: {
      displayCategories:{
        type: Array,
      }
    },

    methods: {

      dragstart(task){
        this.$emit("dragstart",task);
      },

      dragover(overtask){
        this.$emit("dragover",task);
      }


    }


  }

</script>

<style scoped> 

  .trello-part {
    min-width: 30%;
    background: gray;
    margin: 10px 10px;
    padding: 5px 15px;
  }

  .category-name {
    font-weight: bold;
  }


</style>