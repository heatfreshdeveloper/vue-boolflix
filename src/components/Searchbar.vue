<template>
  <div class="container">
      <input type="text" class="form-control" v-model="searched" @keydown.enter="startResearch"
      placeholder="Cerca un film o una serie TV..." aria-label="Username">
      <button class="btn btn-primary" @click="startResearch">Cerca</button>
  </div>
</template>

<script>
export default {
    name: "Searchbar",
    data() {
        return {
            searched: "",
        }
    }, 
    methods: {
        startResearch() {
            this.$emit("searchMovies", this.searched);
        }
    }
}
</script>

<style>

</style>