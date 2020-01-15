<template>
  <div class="container">
    <form class="mb-5">
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          placeholder="Buscar..."
          v-model="searchString"
          @keydown.13.prevent="parseSearchString"
        />
        <div class="input-group-addpend">
          <button type="submit" class="btn btn-outline-secondary" @click="parseSearchString">
            <i class="fas fa-search"></i>
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "SearchForm",
  data() {
    return {
      searchString: ""
    };
  },
  methods: {
    parseSearchString() {
      const trimmedSearchString = this.searchString.trim();
      
      if (!trimmedSearchString !== '') {
        const searchParams = trimmedSearchString.split(/\s+/);
        this.$emit('search', searchParams);
        this.searchString = '';
      }


    }
  }
};
</script>

<style scoped>
input,
button {
  box-shadow: none !important;
}

.form-control {
  border-color: #6c757d;
}
</style>