<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask(newTaskTitle)"
      @keyup.enter="addTask(newTaskTitle)"
      class="px-6 py-4"
      outlined
      label="Add task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>
    <v-list class="pt-0" flat>
      <div 
        v-for="task in tasks"
        :key="task.id"
      >
        <v-list-item 
          class="px-6"
          :class="{ 'blue lighten-5' : task.done }" 
          @click="doneTask(task.id)">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through' : task.done }">
                {{task.title}}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn 
                @click.stop="deleteTask(task.id)"
                icon>
                <v-icon color="primary">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider class="mx-6"></v-divider>
      </div>
    </v-list>
  </div>
  
</template>

<script>
  export default {
    name: 'Todo',
    data() {
      return {
        newTaskTitle: '',
        tasks: [
          // {
          //   id: 1,
          //   title: 'Groceries',
          //   done: false
          // },
          // {
          //   id: 2,
          //   title: 'John Doe\'s Birthday',
          //   done: false
          // },
          // {
          //   id: 3,
          //   title: 'Dentist',
          //   done: false
          // }
        ]
      }
    },
    methods: {
      addTask(title) {
        this.tasks.push({
          id: this.tasks.length !== 0 ? this.tasks[this.tasks.length - 1].id + 1 : 1, 
          title: title, 
          done: false
        })
        this.newTaskTitle = ''
      },
      doneTask(id) {
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    }
  }
</script>
