<template>
  <div class="container">
    <table class="table">
      <thead>
      <tr>
        <!--        <th>#</th>-->
        <th>Title</th>
        <th>Url Slug</th>
        <th>Keywords</th>
        <th>Content</th>
        <th>Actions</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in items" :key="item.id">
        <!--        <td>{{ item.id }}</td>-->
        <td>{{ item.title }}</td>
        <td>{{ item.slug }}</td>
        <td>{{ item.keywords }}</td>
        <td>{{ item.content }}</td>
        <td>
          <router-link :to="{name:'edit', params:{id:item.id}}">
            <b-icon-pencil-square class="text-info mr-3 lg-button"></b-icon-pencil-square>
          </router-link>

          <b-icon-trash class="text-danger trash-icon lg-button" @click="deleteItem(item.id)"></b-icon-trash>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import axios from "axios";
// import router from "@/router";

export default {
  data: () => {
    return {
      items: []
    }
  },
  methods: {
    deleteItem(id) {
      const res = axios.delete('http://localhost:3000/items/' + id)
      res.then(() => this.getItems()).catch((e) => console.log(e))
    },
    async getItems() {
      const res = axios.get('http://localhost:3000/items')
      this.items = (await res).data
    },

  },
  name: 'HomeView',
  components: {
    // HelloWorld
  },
  mounted() {
    this.getItems()
  },
}
</script>
<style scoped>
.trash-icon{
  cursor: pointer;
}

.lg-button{
  font-size: 25px;
  }
</style>
