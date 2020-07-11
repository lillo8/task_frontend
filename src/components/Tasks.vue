<template>
    <div class="dataContainer"> 
        <span v-if="tasks.length>0" >
            <table v-bind:key="task.taskId"  v-for="task in tasks">
                <TaskItem v-bind:task="task" v-on:del-task="$emit('del-task', task.taskId)" />
            </table>
        </span>
        <span v-else>No tasks available. Use the Add Task link to create the first one</span>

    </div>
</template>

<script>
import TaskItem from "./TaskItem"
export default {
    name: "Tasks",
    components: {
        TaskItem
    },
    props: ["tasks"]
    
}
</script>

<style scoped>
table{
    border-collapse: separate;
    width: 85%;
    align-self: center;

    
}
.dataContainer {
    margin: 50px;
}
</style>