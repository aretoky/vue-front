<template>
  <div>
    <v-form ref="checkForm">
      <v-text-field
        v-model="blog.title"
        label="Title"
        :rules="[required('Title')]"
      ></v-text-field>
      <v-textarea
        v-model="blog.body"
        label="Body"
        :rules="[required('Body')]"
      ></v-textarea>

      <v-btn class="mr-4" @click="onSubmit">Create</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: {},
      required(propertyType) {
        return v => (v && v.length > 0) || `You must input a ${propertyType}`;
      }
    };
  },
  methods: {
    async onSubmit() {
      if (this.$refs.checkForm.validate()) {
        const blog = await this.$store.dispatch("addBlog", this.blog);
        this.$store.commit("setMessage", {
          status: true,
          message: "Blog was successfully created."
        });
        setTimeout(() => {
          this.$store.commit("setMessage", {});
        }, 3000);
        this.$router.push({ name: "show-blog", params: { id: blog.id } });
      }
    }
  }
};
</script>
