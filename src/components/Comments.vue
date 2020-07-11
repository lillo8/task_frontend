<template>
    <div class="div"> 
        <span v-if="comments.length>0">
            <div  v-bind:key="comment.commentId"  v-for="comment in comments">
                <CommentItem v-bind:comment="comment" />
            </div>
        </span>
        <span v-else>
            The selected task has no comments, you can add the first one with the form below.
        </span>
    </div>
</template>

<script>
import CommentItem from "./CommentItem"
export default {
    name: "Comments",
    components: {
       CommentItem
    },
    props: ["comments"]
    
} 
</script>

<style scoped>

</style>