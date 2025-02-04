<template>
   <div>
        <h1>Task Manager</h1>
        <input type="text" v-model="newTask" @keyup.enter="addTask">
        <button @click="addTask">Add Task</button>

        <div>
            <table>
               <thead>
                    <tr>
                        <th></th>
                        <th>Name</th>
                        <th>Action</th>
                    </tr>
               </thead>
               <tbody>
                <tr v-for="(task, index) in tasks" :key="index" :class="{ 'line-through': task.completed }">
                    <td>
                        <input type="checkbox" @click="toggleTask(index)" v-model="task.completed">
                    </td>
                    <td>
                        {{ task.name }}
                    </td>
                    <td>
                        <button @click="deleteTask(index)">Delete</button>
                    </td>
                </tr>
               </tbody>
            </table>
            <div>
                <p>Total Task: {{ totalTask }}</p>
                <p>Completed Task: {{ completedTask }}</p>
                <p>Message: {{ completeStatus }}</p>
            </div>
        </div>
   </div>
</template>

<script>
export default {
    data() {
        return {
            tasks: [],
            newTask: ''
        };
    },
    computed: {
        totalTask: function () {
            return this.tasks.length;
        },

        completedTask: function () { 
            return this.tasks.filter(task => task.completed).length;
        },

        completeStatus: function () { 
            let status = this.completedTask;

            if (status == 0) {
                return 'No completed Task!';
            } else if (status < this.tasks.length) {
                return 'Some tasks completed';
            } else if (status == this.tasks.length) {
                return 'All task completed.';
            }
        },

    },
    methods: {
        addTask: function() {
            this.tasks.push({name: this.newTask, completed: false});
            this.newTask = '';
        },
        deleteTask: function(index) {
            this.tasks.splice(index, 1);
        },
        toggleTask: function(index) {
            this.tasks[index].completed = !this.tasks[index].completed;
        }
    }
}
</script>