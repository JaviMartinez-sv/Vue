<template>
  <div id="app">
    <Header></Header>

    <h2>{{ title }}</h2>
    <div>
      <input v-model="newTaskName" @keyup.enter="AddNewTask" type="text" />
      <b-button variant="danger" @click="AddNewTask()">Añadir</b-button>

      <p></p>
    </div>

    <div>
      <Todoitem 
      v-for="task in tasks"
      :key="task.id"
      :item="task"
      @deleted='removeElement'>
      </Todoitem>

      
      <!-- <div @click="markAsDone(task.id)" v-for="task in tasks" :key="task.id">
        <div v-if="!task.completed">{{ task.name }}</div>
        <div class="done" v-if="task.completed">{{ task.name }}</div>
        <button @click="removeElement(task.id)">Eliminar</button>
      </div> -->
    </div>

    <p></p>
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <Footer></Footer>
  </div>
</template>

<script>
import Footer from './components/Footer.vue'
// import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
import Todoitem from './components/Todoitem.vue'

export default {
  name: 'App',
  components: {
  //  HelloWorld,
    Header,
    Footer,
    Todoitem
  },
  methods:{
    AddNewTask(){   
      if(this.newTaskName !== ''){
        this.tasks.push({
          id: this.tasks.length,
          completed:false,
          name: this.newTaskName
        })
        this.newTaskName = ''
      }
    },
    markAsDone(id){
      for (let i=0; i<this.tasks.length; i++){
        if(this.tasks[i].id === id){
        this.tasks[i].completed = !this.tasks[i].completed
        }
      }
    },
    removeElement(id){
      console.log(`eliminar ${id}`)
      for (let i=0; i<this.tasks.length; i++){
        if(this.tasks[i].id === id){
        this.tasks.splice(i,1)
        }
      }   
    },
  },
  data(){
    return {
     newTaskName:'',
     title: 'Mi primera aplicacion en Vue',
     tasks: [
       { id: 0, completed: false, name: 'Crear aplicacion'},
       { id: 1, completed: false, name: 'Publicarla'},
       { id: 2, completed: false, name: 'Hacerme rico!'}
     ]
    }
  }
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
.done {
  text-decoration: line-through;
}
</style>
