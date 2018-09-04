<template>
    <header class="header">
        <h1>{{head}}</h1>
    </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      head: "todos"
    };
  }
};
</script>

<style scoped>
header {
  flex: 0 1 auto;
  box-sizing: border-box;
  padding: 20px 0;
  text-align: center;
}
h1 {
  color: rgba(175, 47, 47, 0.15);
  font-size: 100px;
}
</style>
