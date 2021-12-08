<template>
  <div>
    <div class="clearAllContainer shadow">
      <span class="clearAllBtn" v-on:click="clearAll">Clear All</span>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    clearAll: function () {
      this.$emit('clearAll');
    }
  }
}
</script>
<style scoped>
.clearAllContainer {
  width: 10rem;
  height: 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 0 auto;
}

.clearAllBtn {
  color: #e20303;
  display: block;
}
</style>