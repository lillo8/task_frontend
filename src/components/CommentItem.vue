<template>
    <div class="commentContainer">
        <div class="commentImage"><img  src="../img/comm.png" width="20" /></div>
        <div class="commentText">{{comment.description}}</div><br /> 
    </div>
</template>

<script>
export default {
    name: 'CommentItem',
    props: ["comment"]
}
</script>

<style scoped>

.commentContainer{
    padding-left: 5%;
    padding-right: 5%;
    vertical-align: middle;
}
.commentText{
    text-align: left;
    margin-left: 40px;
}

.commentImage{
    background-color:blue; 
    padding:2px;
    float: left;
}


</style>