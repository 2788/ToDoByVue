<template>
    <footer class="footer">
        <p>DoubleClick item to edit</p>
        <p>A vue demo</p>
       <p>Written by {{author}}</p>
       <p>For XX</p>
    </footer>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      author: "duli"
    };
  }
};
</script>

<style scoped>
p {
  color: #bfbfbf;
  font-size: 10px;
  line-height: 1;
}
p:first-child{
  color: brown;
}
p:last-child{
  color:darkblue;
}
.footer {
  flex: 0 1 auto;
  box-sizing: border-box;
  width: 100%;
  margin-top: auto;
  margin-bottom: 0;
  padding: 10px 0;
  font-size: 10px;
  text-align: center;
}
</style>
