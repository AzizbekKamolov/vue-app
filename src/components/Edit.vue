<template>
  <div class="container">
    <div class="form-group">
      <label for="title">Title</label>
      <input type="text" class="form-control" id="title" name="title" v-model="title">
    </div>
    <div class="form-group">
      <label for="slug">Url Slug</label>
      <input type="text" class="form-control" id="slug" name="slug" v-model="slug">
    </div>
    <div class="form-group">
      <label for="keywords">Keywords</label>
      <input type="text" class="form-control" id="keywords" name="keywords" v-model="keywords">
    </div>
    <div class="form-group">
      <label for="content">Content</label>
      <input type="text" class="form-control" id="content" name="content" v-model="content">
    </div>

    <button type="submit" class="btn btn-primary" @click="editItem" :disabled="disabledButton">Save</button>
  </div>
</template>

<script>

import axios from "axios";
import router from "@/router";

export default {
  name: 'AddView',
  data: () => {
    return {
      disabledButton: false,
      title: '',
      slug: '',
      keywords: '',
      content: '',
      id: ''
    }
  },
  components: {},
  methods: {
    editItem() {
      if (!this.title || !this.keywords || !this.content) {
        alert("not empty")
      } else {
        this.disabledButton = true
        axios.put('http://localhost:3000/items/' + this.id, {
          "id": this.id,
          "title": this.title,
          "slug": this.slug,
          "keywords": this.keywords,
          "content": this.content,
        }).then(() => this.clearInputData())
      }

    },
    clearInputData() {
      this.title = ''
      this.keywords = ''
      this.slug = ''
      this.content = ''
      this.disabledButton = false
      router.push('/')
    },
    assignData(data){
      this.title = data.title
      this.slug = data.slug
      this.keywords = data.keywords
      this.content = data.content
    }
  },
  props: {},
  created() {
    this.id = this.$route.params.id
    const res = axios.get('http://localhost:3000/items/' + this.id )
    res.then((result) => this.assignData(result.data)).catch(() => router.push('/'))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
