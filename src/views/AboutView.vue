<template>

  <div class="Check">

  <v-text-field
   v-model="newTaskNaslov"
   @click:append="dodajTask"
   @keyup.enter="dodajTask"
   class="pa-3"
     solo
     label="Dodaj task"
     append-icon="mdi-plus"
     hide-details
     clearible
     ></v-text-field>
  
  
    <v-list
      class="pb-0"
      two-line
      flat
    >
    <div
    v-list-item
        v-for="task in tasks"
        :key="task.id">
       <!-- Vfor za prolazak kroz taskove -->
        <v-list-item
        @click="doneTask(task.id)"
        :class="{'blue lighten-5':task.done}">
          <template v-slot:>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{'text-decoration-line-through' : task.done}">
                {{task.naslov}}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
          <v-btn 
          @click.stop="deleteTask(task.id)"
          icon>
            <v-icon color="grey lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
          
        </v-list-item>
        <!-- razmaci -->
        <v-divider></v-divider>
    </div>
     
        </v-list>
    </div>
  
</template>

<script>
export default{
  name:'CheckView',
  // Vracanje objekta//
  data(){
    return{
      newTaskNaslov:'',
      tasks:[
        {
          id:1,
          naslov:"Ustani",
          done:false
        },
        {
          id:2,
          naslov:"Treniraj",
          done:false
        },
        {
          id:3,
          naslov:"Gledaj Naruta",
          done:false
        }
        
      ]

    }
  },
  // filtrira kroz svaki task
  //dodaj task
  methods:{
    dodajTask(){
    let newTask={
      id:Date.now(),
      naslov: this.newTaskNaslov,
      done:false
    }
    this.tasks.push(newTask)
    this.newTaskNaslov=''
    },
    doneTask(id){
      let task=this.tasks.filter(task => task.id == id)[0]
      task.done = !task.done
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !==id)
    }
  }


}

</script>
<style scoped>

</style>