<template>
  <div class="mt-3">
    <input @input="onInput" placeholder="Search Start Here" />
    <button @click="SearchYouTube" class="btn-success">Search</button>
    <!--
            Same effect
        <input @input="onInput"/>
         <input v-on:input="onInput"/>

        -->
  </div>
</template>
<script>
/*
    if I want to communicate between Parent => Child I should use props
    if I want to communicate between child => Parent I should use emitting events included in vue.
*/
export default {
  name: "SearchBar",
  methods: {
    onInput: function (event) {
      //to send data from searchbar to App component (Parent).
      this.$emit("termChange", event.target.value);
    },
    SearchYouTube: function () {
      console.log("Button Clicked..");
    },
  },
};
</script>
<style scoped>
input {
  width: 75%;
}
div {
  text-align: center;
}
</style>