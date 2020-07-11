<template>
  <div class="about">
    <h1 v-if="$route.params.id==0" >Add New Task</h1>
    <h1 v-else>Modify Task</h1>
    <form @submit="addTask">
      <ul>
        <li>
          <label for="title">Title:</label>
          <input id="title" type="text" v-model="title" name="title" placeholder="Taks Title..."  v-bind:class="{ error: titleError }"/><br />
        </li>

        <li>
          <label for="description">Description:</label>
          <input id="description"  type="text" v-model="description"  name="description" placeholder="Taks Description..." v-bind:class="{ error: descriptionError }" /><br />
        </li>

        <li>
          <label for="priority">Priority:</label>
          <select  id="priority" v-model="priority" name="priority" v-bind:class="{ error: priorityError }">
            <option v-if="this.priority.value == 2"  selected="selected" value="2">LOW</option>
            <option v-else value="2">LOW</option>
            <option v-if="this.priority.value == 1"  selected="selected" value="1" >MEDIUM</option>
            <option v-else value="1">MEDIUM</option>
            <option v-if="this.priority.value == 0"  selected="selected" value="0">HIGH</option>
            <option v-else value="0">HIGH</option>
          </select><br />
        </li>

        <li>
          <label for="toDoDate">To Do Date:</label>
          <input  id="toDoDate" type="date"  name="toDoDate" v-model="toDoDate"  v-bind:class="{ error: toDoDateError }" />
        </li>

        <li class="button">
          <input v-if="$route.params.id==0" type="submit" value="Add Task">
          <input v-else type="submit" value="Modify Task">
        </li>
      </ul>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
//import VueRouter from 'vue-router'
export default {
    name: "Add",
    data(){
        return{
            title: '', titleError:false,
            priority: '', priorityError:false,
            description: '',descriptionError:false,
            toDoDate:'', toDoDateError:false
        }
    },
    methods:{
        validateForm(){
          let globalError=false;
          if (this.title.trim().length==0){
            this.titleError=true;
            globalError=true;
          } else{
            this.titleError=false;
          }
          if (this.description.trim().length==0){
            this.descriptionError=true;
            globalError=true;
          }else{
            this.descriptionError=false;
          }
          if (this.priority.length==0){
            this.priorityError=true;
            globalError=true;
          }else{
            this.priorityError=false;
          }
          if (this.toDoDate.trim().length==0){
            this.toDoDateError=true;
            globalError=true;
          }else{
            this.toDoDateError=false;
          }
          return globalError;
        },
        addTask(e){
            e.preventDefault();
            console.log("adding a new task" +  this.title );
            if (!this.validateForm()){
              let params = new URLSearchParams();
              params.append('title',this.title);
              params.append('description',this.description);
              params.append('priority.priorityId',this.priority);

              params.append('toDoDate',this.toDoDate);

              if (this.$route.params.id>0){
                  params.append('taskId', this.$route.params.id);
              }
              axios.post("http://localhost:8083/task",params, {  headers: {    'Content-Type': 'application/x-www-form-urlencoded'  }})
              .then( () => this.$router.push({ path: '/' }));
            }
        }

    },
    async created(){
      if (this.$route.params.id>0){
        const response = await axios.get('http://localhost:8083/task/' + this.$route.params.id );
        this.title =  response.data.title;
        this.description = response.data.description;
        this.toDoDate = response.data.toDoDate;
        this.priority = response.data.priority.priorityId;
      }
    }
}
</script>


<style scoped>

form {
  /* Center the form on the page */
  margin: 0 auto;
  width: 400px;
  /* Form outline */
  padding: 1em;
  border: 1px solid #CCC;
  border-radius: 1em;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

form li + li {
  margin-top: 1em;
}

label {
  /* Uniform size & alignment */
  display: inline-block;
  width: 90px;
  text-align: right;
}

input, select,
textarea {
  /* To make sure that all text fields have the same font settings
     By default, textareas have a monospace font */
  font: 1em sans-serif;

  /* Uniform text field size */
  width: 300px;
  box-sizing: border-box;

  /* Match form field borders */
  border: 1px solid #999;
}

input:focus, 
textarea:focus,
select:focus {
  /* Additional highlight for focused elements */
  border-color: #000;
}

textarea {
  /* Align multiline text fields with their labels */
  vertical-align: top;

  /* Provide space to type some text */
  height: 5em;
}

.button {
  /* Align buttons with the text fields */
  padding-left: 90px; /* same size as the label elements */
}

button {
  /* This extra margin represent roughly the same space as the space
     between the labels and their text fields */
  margin-left: .5em;
}
.error  {
  background-color: #fce4e4;
  border: 1px solid #cc0033;
  outline: none;
}

</style>