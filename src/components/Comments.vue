<template>
  <div class="container">
    <h1>comentario</h1>
    <hr />
    <FormTodo v-on:add-todo="addComments"></FormTodo>
	
    <div class="list-group">
	<p v-if="comments.length <= 0" >Sem comentário....</p>
      <div class="list-group-item" v-for="(comment, index) in allComments" :key="index">
        <span class="comment_author"
          >Autor:<strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComments(index)"
            >Excluir</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FormTodo from './FormTodo.vue'
export default {
    components: {
        FormTodo
    },
  data() {
    return {
      comments: [],
      name: "",
      message: "",
    };
  },
  methods: {
    addComments(comment) {
		this.comments.push(comment);
    },
    removeComments(index) {
      this.comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name,
      }));
    },
  },
  watch: {
    comments(val) {
      console.log("val", val);
    },
  },
};
</script>
