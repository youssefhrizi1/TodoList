<template>
  <div class="home">

 <v-text-field
    class="pa-3"
            outlined
            label="add Task"
            append-icon="mdi-map-marker"
            @click:append="addTask"
            @keyup.enter ="addTask"
            v-model="taskTitle"
            clearable
            hide-details
          ></v-text-field>

 <v-list flat >
  <div class="pa-3" v-if="!tasks.length" ><p>No Tasks Yet</p></div>
 	<div
 class="task"
 v-for="task in tasks"
 :key="task.id"

 >
     <v-list-item
     	@click="editTask(task.id)"
     	:class="{ 'blue lighten-5': task.done } "

     >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through': task.done}">{{ task.title }}</v-list-item-title>
            </v-list-item-content>
                  <v-list-item-action @click="deleteTask(task.id)">
          <v-btn icon>
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>

        </v-list-item>
          <v-divider></v-divider>
 </div>


  </v-list>
 
    


  </div>
</template>

<script>


export default {
  name: 'Home',
  data(){
  	return {
      taskTitle :'',
  		tasks: [
  /*			{ id:1, title:'PHP', done:false},
  			{ id:2, title:'HTML', done:false},
  			{ id:3, title:'JS', done:true},
  			{ id:4, title:'Vue', done:false},*/
  		]
  	}
  },
  methods:{
    addTask(){
      let newTask = { id:Date.now(), title:this.taskTitle, done:false};
      this.tasks.push(newTask);
      this.taskTitle ='';
    },
  	editTask(id){
  		let task = this.tasks.filter(task => task.id === id)[0];
  		//console.log('task ',task);
  		task.done = !task.done; 
  	},
    deleteTask(id){
      console.log(id);
      this.tasks = this.tasks.filter(task => task.id != id);
    }
  }
}
</script>
