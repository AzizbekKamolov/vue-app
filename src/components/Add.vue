<template>
  <div class="container">
    <div class="form-group">
      <label for="title">Title</label>
      <input type="text" class="form-control" id="title" name="title" v-model="title">
    </div>
    <div class="form-group">
      <label for="keywords">Keywords</label>
      <input type="text" class="form-control" id="keywords" name="keywords" v-model="keywords">
    </div>
    <div class="form-group">
      <label for="slug">Url Slug</label>
      <input type="text" class="form-control" id="slug" name="slug" v-model="slug">
    </div>
    <div class="form-group">
      <label for="content">Content</label>
      <input type="text" class="form-control" id="content" name="content" v-model="content">
    </div>
    <button type="submit" class="btn btn-primary" @click="addItem" :disabled="disabledButton">Add</button>
    <TipTap @tipTap="tipTap"></TipTap>
  </div>
</template>

<script>

import axios from "axios";
import {uuid} from "vue-uuid";
import router from "@/router";
import TipTap from './TipTap.vue'
// import { Editor, EditorContent } from '@tiptap/vue-2'
// import StarterKit from '@tiptap/starter-kit'

export default {
  name: 'AddView',
  data: () => {
    return {
      disabledButton: false,
      title: '',
      slug: '',
      keywords: '',
      content: '<p>A Vue.js wrapper component for Tiptap to use <code>v-model</code>.</p>'
    }
  },
  components: {TipTap},
  methods: {
    addItem() {
      if (!this.title || !this.keywords || !this.content) {
        alert("not empty")
      } else {
        this.disabledButton = true
        axios.post('http://localhost:3000/items', {
          "id": uuid.v1(),
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
      this.content = ''
      this.disabledButton = false
      router.push('/')
    },
    tipTap(data){
      console.log(data)
    }
  },
  mounted() {
    // this.content = new Editor({
    //   content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
    //   extensions: [StarterKit],
    // })
    // console.log()
  },
  props: {
    // msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
