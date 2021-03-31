<template>

  <section class="input-part">
    <input 
      type="text" 
      class="category-input" 
      v-model="newCategoryName"
      @keypress.enter="addCategoryName">
  </section>
  
</template>

<script>
  export default {
    name: "CategoryNameInput",


    data(){
      return{
        newCategoryName: ""
      }
    },

    methods: {

      addCategoryName(){
        this.$emit("add-category-name", this.newCategoryName);
        this.newCategoryName = "";
      }

    }
    

  }

</script>
