<template>
  <ul  class="data-box">
    <li  v-for="item in items" :key="item.id"  :index="item.id" >
        <input type="checkbox" :id="item.id" :checked="item.isCompleted" hidden>
        <label :for="item.id" @click="alterStatus"></label>
        <span @dblclick="active" 
              @keydown.enter.esc="alter($event,item.text)" 
              @blur="alter($event, item.text)"
              :class="[item.isCompleted ? 'completed' : '']">
        {{item.text}}      
        </span>
        <button @click="deleteItem" >X</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ToDoData",
  props: ["items"],
  methods: {
    active(ev) {
      ev.target.setAttribute("contentEditable", true);
      event.target.focus();
    },
    alter(ev, text) {
      ev.target.removeAttribute("contentEditable");
      if(text !== ev.target.innerText)
        this.$emit("alterItem", ev.target.innerText, ev.target.parentElement.getAttribute('index'));
    },
    alterStatus(ev){
      this.$emit('alterStatus', !ev.target.previousElementSibling.checked, ev.target.parentElement.getAttribute('index'));
    },
    deleteItem(ev){
      this.$emit('deleteItem',ev.target.parentElement.getAttribute('index'));
    }
  }
};
</script>

<style scoped>
.data-box{
  display: flex;
  flex-flow: column;
}
.data-box li {
  display: flex;
  height: 60px;
  width: 100%;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  border: 1px solid #e6e6e6;
}
.data-box label {
  flex: 0 0 auto;
  width: 25px;
  height: 25px;
  margin: auto 10px auto;
  cursor: pointer;
  border: 1px solid #e6e6e6;
  border-radius: 50%;
  box-sizing: border-box;
}

.data-box span[contentEditable] {
  margin-right: 10px;
  border: 1px solid #999;
  outline: none;
  background: #fff;
  box-shadow: inset rgba(224, 216, 216, 0.966) 1px 1px 1px 1px;
}

.data-box input:checked + label{
  border: none;
  background:  url(../assets/images/tick.png) 0 0 /cover no-repeat;
}

.data-box span {
  flex: 1 1 auto;
  box-sizing: border-box;
  height: 100%;
  text-align: left;
  border: none;
  font-size: 24px;
  line-height: 60px;
  overflow-y:unset;
  overflow-x: hidden;
  white-space: wrap;
  
}

.data-box span.completed {
  text-decoration: line-through;
  color: #d9d9d9;
}
.data-box button {
  /* visibility: hidden; */
  font-size: 24px;
  padding-right: 20px;
  padding-left: 10px;
  height: 100%;
  line-height: 60px;
  cursor: pointer;
}
.data-box li:hover button {
  visibility: visible;
  color: brown;
}
</style>