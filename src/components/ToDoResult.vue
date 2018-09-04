<template>
   <section class="result-box">
       <div class="number">{{number}} left</div>
       <div class="tabs">
           <span @click="modifyTabs" :class="[curTab==='All' ? 'checked' : '']">All</span >
           <span @click="modifyTabs" :class="[curTab==='Active' ? 'checked' : '']">Active</span>
           <span @click="modifyTabs" :class="[curTab==='Done' ? 'checked' : '']">Done</span>
        </div>
       <button :class="[curTab!=='Active' && doneNumber!==0 ? 'show' : 'hide']" @click="deleteAllDone">
       Clear Done
       </button>
   </section>
</template>

<script>
export default {
  name: "ToDoResult",
  props: ["number", "curTab", 'doneNumber'],
  methods: {
    modifyTabs(event) {
      this.$emit("modifyTabs", event.target.innerText);
    },
    deleteAllDone(ev){
        this.$emit('deleteAllDone');
    }
  }
};
</script>

<style scoped>
.result-box {
  position: relative;
  display: flex;
  flex-flow: row nowrap;
  width: 100%;
  height: 50px;
  justify-content: space-between;
  background: #fff;
  border: 1px solid #ededed;
  font-size: 12px;
}
.number {
  padding-left: 15px;
  line-height: 50px;
}
.tabs {
  display: flex;
  width: 100px;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  z-index: 1;
}

.tabs span {
  padding: 5px;
  margin: 3px;
  cursor: pointer;
}

.checked {
  border: 1px solid rgba(80, 20, 20, 0.4);
  border-radius: 5px;
}

.result-box button{
    cursor: pointer;
    padding-right: 15px;
    z-index: 1;
}
button.hide {
  visibility: hidden;
}

button.show{
    visibility: visible;
}

.result-box:before {
  content: "";
  position: absolute;
  z-index: 0;
  right: 0;
  bottom: 0;
  display: block;
  width: 100%;
  height: 50px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
    0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
    0 17px 2px -6px rgba(0, 0, 0, 0.2);
}
</style>