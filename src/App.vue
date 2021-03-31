<template>
  
  <section id="app" class="tasklist-app">
    <header class="header">
			<h1>TaskLIst</h1>
		</header>
    <main class="main" role="main">
      
      <category-name-input
        @add-category-name="addCategoryName"
      ></category-name-input>

      <trello-contents
        class="trello-contents"
        :displayCategories="displayCategories"
        @dragstart="dragstart"
        @dragover="dragover"
      ></trello-contents>

		</main>
  </section>

</template>

<script>

import CategoryNameInput from './components/categoryNameInput.vue';
import TrelloContents from './components/trelloContents.vue';

export default {
  name: 'App',

  components: {
    CategoryNameInput,
    TrelloContents
  },

  data(){
    return{
      newCategoryName:"",
      moveTask: "",

      categories: [
      {
        id: 1,
        name: 'テストA',
        collapsed: false,
      }, 
      {
        id: 2,
        name: 'テストB',
        collapsed: false,
      },
        {
        id: 3,
        name: 'テストC',
        collapsed: false,
      }, 

      ],

      tasks:[
        {
        id: 1,
        category_id: 1,
        name: 'テスト1',
        start_date: '2020-12-18',
        end_date: '2020-12-20',
        incharge_user: '鈴木',
        percentage: 100,
      },
      {
        id: 2,
        category_id: 1,
        name: 'テスト2',
        start_date: '2020-12-19',
        end_date: '2020-12-23',
        incharge_user: '佐藤',
        percentage: 90,
      },
      {
        id: 3,
        category_id: 3,
        name: 'テスト3',
        start_date: '2020-12-19',
        end_date: '2020-12-21',
        incharge_user: '鈴木',
        percentage: 40,
      },
      {
        id: 4,
        category_id: 2,
        name: 'テスト4',
        start_date: '2020-12-21',
        end_date: '2020-12-30',
        incharge_user: '山下',
        percentage: 60,
      },
      {
        id: 5,
        category_id: 2,
        name: 'テスト5',
        start_date: '2020-12-20',
        end_date: '2020-12-22',
        incharge_user: '佐藤',
        percentage: 5,
      },
      {
        id: 6,
        category_id: 1,
        name: 'テスト6',
        start_date: '2020-12-28',
        end_date: '2020-12-08',
        incharge_user: '佐藤',
        percentage: 0,
      },
      ],
    }
  },

  computed: {
    //categoryのdataと、tasksのデータを紐付けてnest化する。
    displayCategories(){
       
      let categories = [];
      let tasks = "";

      this.categories.map(category => {
        tasks = this.tasks.filter(task => task.category_id === category.id);
        categories.push({
            id: category.id,
            name: category.name,
            tasks
          });
      });
      return categories;
    }
  },


  methods: {
    addCategoryName(categoryTitle){
      const newCategoryName = categoryTitle && categoryTitle.trim();

      if (!newCategoryName) {
				return;
			}

			this.categories[0].name = newCategoryName;
      
    },

    dragstart(task){
      this.moveTask = task;
      console.log(task);
    },


    dragover(overtask){
      consoloe.log(overtask);
    }
  },



}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


.trello-contents {
  display: flex;
  width: 100%;
}

</style>
