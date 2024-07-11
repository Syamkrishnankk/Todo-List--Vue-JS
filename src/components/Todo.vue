<script setup>
import { ref } from 'vue'
const list = ref([])
const task = ref('')

const addItem = () => {
    const date = new Date();
    // const date = d.getDate();
    if(task.value.length > 0){
        list.value.push(
            {
                date:date,
                value:task.value,
                completed:false,
            }
        );
        task.value = '';
    }
    console.log(list.value.length);
}
const editTodo = (index) => {
    const editText = prompt('Edit the Todo : ');
    console.log(editText);
    if (editText.length > 0){
        console.log(editText.trim());
        const updatedItem = { ...list.value[index], value: editText};
        console.log(updatedItem);
        list.value.splice(index, 1, updatedItem);
    }
};
const toggleCompleted = (index) => {
  list.value[index].completed = !list.value[index].completed;
};
const deleteItem = (index) => {
    list.value.splice(index,1);
}
const styleObject = ref({
    'text-decoration-line' : 'line-through',
  
})

</script>

<template>
    <h3 class="text-center text-h3 mb-8">Todo List</h3>
    <v-container>
        <v-row align="center" justify="center">
            <v-col >
                <v-text-field  v-model="task" @keyup.enter="addItem" placeholder="Enter the task !!" class="w-100" min-width="300" ></v-text-field>
            </v-col>
            <v-col  justify="left">
                <v-btn variant="tonal" @click="addItem" size="large" height="40" class="mt-n6 p-5"><p class="font-weight-medium">Add Task</p></v-btn>
            </v-col>
        
        </v-row>
        
        <ul>
            
            <li v-for="(item,index) in list">
                <v-row align="center" justify="left" class="mt-5">
                <v-col cols="auto">
                    <span :style="item.completed ? styleObject : ''"><p class="font-weight-medium" >{{ item.value }}</p></span>
                </v-col>
                <v-col cols="auto">
                    <v-btn @click="toggleCompleted(index)" >{{ item.completed ? 'Undo' : 'Complete' }}</v-btn>
                </v-col>
                <v-col cols="auto">
                    <v-btn @click="editTodo(index)">Edit</v-btn>
                </v-col>
                <v-col cols="auto">
                    <v-btn @click="deleteItem(index)">Delete</v-btn>
                </v-col>
                </v-row>
                 <p class="mt-2">{{ item.date }}</p>
            </li>
            
        </ul>
   
    </v-container>
</template>

<!-- <style>
.enter-task{
    width: 300px;
}
.row{
    display: flex;
    flex-direction: row;
}

</style> -->
<!-- <template>
    
  </template>
  <script>
    export default {
      data: () => ({
        rules: [
          value => !!value || 'Required.',
          value => (value || '').length <= 20 || 'Max 20 characters',
          value => {
            const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
            return pattern.test(value) || 'Invalid e-mail.'
          },
        ],
      }),
    }
  </script> -->
  