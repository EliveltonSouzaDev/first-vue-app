<template>
  <div class="container mt-4">
    <h1>Comentários</h1>
    <hr />
    <div class="form-todo form-group">
      <p>
        <input
          type="text"
          name="author"
          id=""
          class="form-control"
          v-model="name"
        />
      </p>
      <p>
        <textarea
          placeholder="Comentário"
          name="message"
          class="form-control"
          v-model="message"
        >
        </textarea>
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">
        Comentar
      </button>
    </div>
    <div class="list-group" mt="1">
      <div
        class="list-group-item mt-4"
        v-bind:key="comment.name"
        v-for="(comment, index) in allComments"
      >
        <span class="comment__author"
          >Author:<strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)"
            >Excluir</a
          >
        </div>
      </div>
      <hr />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comments: [],
      name: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (this.message.trim() === "") {
        return null;
      }

      this.comments.push({
        name: this.name,
        message: this.message,
      });

      this.name = "";
      this.message = "";
    },
    removeComment(index) {
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
};
</script>

<style></style>
