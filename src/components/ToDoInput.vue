<template>
    <section class="box">
    <input type="checkbox" class="box-checkbox hidden" id="completeAll" :checked="isAllChecked" @change="completeAllItems" />
    <label for="completeAll" class="box-label"></label>
    <input type="text" class="box-input" :placeholder="placeholder" @keydown.enter="addItem" />
  </section>
</template>
<script>
export default {
  name: "ToDoInput",
  props: ["isAllChecked"],
  data() {
    return {
      placeholder: `What needs ?`
    };
  },
  methods: {
    completeAllItems(event) {
      this.$emit("completeAllItems", event.target.checked);
    },
    addItem(event) {
      if (event.target.value.trim() !== "") {
        this.$emit("add", event.target.value.trim());
      }
      event.target.value = "";
    }
  }
};
</script>

<style>
.box {
  display: flex;
  width: 100%;
  height: 60px;
  flex-flow: row nowrap;
  background: #fff;
  border: 1px solid #ededed;
}
.hidden {
  display: none;
}
.box-label {
  position: relative;
  height: 100%;
  width: 45px;
  flex: 0 1 auto;
}
.box-input {
  flex: 1 1 0px;
  font-size: 24px;
  outline: none;
}
::-webkit-input-placeholder {
  color: #d9d9d9;
  font-style: italic;
}

.box-label:before,
.box-label:after {
  content: "";
  position: absolute;
  left: 10px;
  display: block;
  width: 0;
  height: 0;
  border: 10px solid transparent;
}
.box-label:before {
  top: 27px;
  border-top-color: #e6e6e6;
}
.box-label:after {
  top: 25px;
  border-top-color: #fff;
}
.box-label:hover::before {
    border-top-color: #bdb8b8;
}
.box-checkbox:checked + .box-label:before {
  border-top-color: #737373;
}
</style>
