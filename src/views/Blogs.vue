<template>
  <div>
    <h1>Blogs</h1>
    <v-row>
      <v-col cols="4">
        <AddBlog />
        <!-- 追加 -->
      </v-col>
      <v-col cols="8">
        <table>
          <tr>
            <th>Title</th>
            <th>Description</th>
          </tr>
          <tr v-for="blog in blogs" :key="blog.id">
            <td>{{ blog.title }}</td>
            <td>{{ blog.body }}</td>
            <td>
              <router-link :to="{ name: 'show-blog', params: { id: blog.id } }"
                >show</router-link
              >
            </td>
            <td>
              <router-link :to="{ name: 'edit-blog', params: { id: blog.id } }"
                >edit</router-link
              >
            </td>
            <td>
              <span class="button_link" @click="deleteBlog(blog)"
                >[ delete ]</span
              >
            </td>
          </tr>
        </table>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import { mapState } from "vuex";
import AddBlog from "./AddBlog"; //追加

export default {
  components: {
    AddBlog //追加
  },
  computed: {
    ...mapState(["blogs"])
  },
  data() {
    return {
      blog: {}
    };
  },
  methods: {
    deleteBlog(blog) {
      console.log(blog);
      this.$store.dispatch("deleteBlog", blog);
    }
  }
};
</script>
