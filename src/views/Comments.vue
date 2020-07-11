<template>
  <div id="app">
      <Header />
    <Comments v-bind:comments="comments" />
    <h3>Add New Comment</h3>
    <form @submit="addComment">
        <input class="inputComment" type="text" v-model="description"  name="description" placeholder="Your comment" v-bind:class="{ error: descriptionError }" /><br>
        <input type="submit" value="Add Comment"><br /><br /><br />
    </form>
  </div>
</template>

<script>

import Comments from '../components/Comments'
import Header from '../components/Header'
import axios from 'axios'
export default {
  name: 'HomeComments',
  components: {
    Comments, Header
  }, 
  data(){
    return {
      comments:[ ],
      description: '', descriptionError: false
    }
  },
  methods:{
      validateForm(){
          let globalError=false;
          if (this.description.trim().length==0){
            this.descriptionError=true;
            globalError=true;
          } else{
            this.descriptionError=false;
          }
          return globalError;
      },
      addComment(e){
          e.preventDefault();
          if (!this.validateForm()){
            var taskId = this.$route.params.taskId;
            let params = new URLSearchParams();
            params.append('description',this.description);
            params.append('task.taskId', taskId);
            axios.post("http://localhost:8083/comment",params )
              .then( res=> {
                this.comments = [...this.comments, res.data];
                this.description = '';
              } 
              )
              .catch( err => console.log(err) )
          }
      }
   
  },
  created(){
    var taskId = this.$route.params.taskId;
    axios.get('http://localhost:8083/task/' + taskId + '/comments')
    .then(res => this.comments = res.data)
    .catch(err => console.log(err))
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


.inputComment {
  /* To make sure that all text fields have the same font settings
     By default, textareas have a monospace font */
  font: 1em sans-serif;

  /* Uniform text field size */
  width:80%;
  box-sizing: border-box;

  /* Match form field borders */
  border: 1px solid #999;
}

.error  {
  background-color: #fce4e4;
  border: 1px solid #cc0033;
  outline: none;
}
</style>
