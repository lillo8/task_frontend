<template>
    <span>
        <tr>
            <td class="tdTName"><strong>{{task.title}}</strong></td>
            <td class="tdTPriority"><strong>{{task.priority.priorityDesc}}</strong></td>
            <td class="tdTDate">{{task.toDoDate}} </td>
            <td class="tdTButtons"> 

                <router-link  :to="{ name: 'Comments', params: {taskId: task.taskId } }" class="showComments" title="Show Comments">
                    <img  src="../img/comm.png" width="20" />
                </router-link>
                <router-link class="editTask" :to="{ name: 'Add', params: {id: task.taskId } }" title="Modify Task">
                     <img src="../img/edit.png" width="20" />
                </router-link> 
                <button @click="$emit('del-task', task.taskId)" class="deleteTask" title="Delete Task">
                    <img style=" background-color:red" src="../img/delete.png" width="20" />
                </button>
            </td>
        </tr>
        <tr>
            <td colspan="4" class="tdTDescrition"><i> {{task.description}}</i>
            </td>
        </tr> 
    </span>  
</template>

<script>
export default {
    name: 'TaskItem',
    props: ["task"]
}
</script>

<style scoped>
.deleteTask{
    background: lightgray;
    border: none;
    cursor: pointer;
}
.showComments{
    border: none;
    cursor: pointer;
    text-decoration: none;
    padding-right: 2px;
}
.editTask{
    border: none;
    cursor: pointer;
    text-decoration: none;
    padding-right: 2px;    
}
.tododate{
    background: lightgray;
    color:black;
    border: none;
    padding: 5px 9px;
    text-decoration: none;
}


tr {
  padding-bottom: 10px; 
  padding-top: 20px;
}
td{
    vertical-align: bottom;
}
.tdTName{
    width: 30% ; 
    white-space: pre-wrap;
    text-align: left;
}
.tdTPriority{
    width: 20% ;
}
.tdTDate{
    width: 20% ;
}
.tdTButtons{
    width:25% ;
    text-align: right;
}
.tdTDescrition{
 border-bottom: 1px solid red;
 text-align: left;
}

img{
    background-color:blue; 
    padding:2px
}

</style>