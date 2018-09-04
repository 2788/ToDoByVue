<template>
    <main class="todolist" >
        <ToDoInput :isAllChecked="isAllChecked" @completeAllItems="completeAllItems" @add="add" />
        <ToDoData :items="items[curTab]"  @alterItem="alterItem"  @alterStatus="alterStatus" @deleteItem="deleteItem"/>
        <ToDoResult :number="items[curTab].length"  
                    :doneNumber="items['Done'].length" 
                    @modifyTabs='modifyTabs'
                    :curTab="curTab"
                    @deleteAllDone="deleteAllDone"
        />
    </main>
</template>

<script>
import ToDoInput from "./ToDoInput";
import ToDoData from "./ToDoData";
import ToDoResult from "./ToDoResult";
let count =
  localStorage && localStorage.getItem("count")
    ? parseInt(localStorage.getItem("count"))
    : 0;

let initItems =
  count === 0
    ? [
        {
          text: "one thing",
          isCompleted: false,
          id: "todoItems" + count++
        }
      ]
    : null;
export default {
  name: "ToDoList",
  components: {
    ToDoInput,
    ToDoData,
    ToDoResult
  },
  data() {
    return {
      isAllChecked:
        localStorage && localStorage.getItem("isAllChecked") === "true"
          ? true
          : false,
      allItems:
        localStorage && localStorage.getItem("allItems")
          ? JSON.parse(localStorage.getItem("allItems"))
          : initItems,
      curTab:
        localStorage && localStorage.getItem("curTab")
          ? localStorage.getItem("curTab")
          : "All"
    };
  },
  watch: {
    allItems: {
      handler: function(val, oldVal) {
        localStorage.setItem("allItems", JSON.stringify(val));
        localStorage.setItem("count", count);
      },
      deep: true
    },
    isAllChecked(val, oldVal) {
      localStorage.setItem("isAllChecked", val);
    },
    curTab(val, oldVal) {
      localStorage.setItem("curTab", val);
    }
  },
  methods: {
    completeAllItems(isAllChecked) {
      this.isAllChecked = isAllChecked;
      for (let o of this.allItems) o.isCompleted = isAllChecked;
    },
    add(text) {
      this.allItems.push({
        text,
        isCompleted: false,
        id: "todoItems" + count++
      });
    },
    modifyTabs(curTab) {
      this.curTab = curTab;
    },
    alterItem(text, id) {
      for (let o of this.allItems) {
        if (o.id === id) {
          o.text = text;
          break;
        }
      }
    },
    alterStatus(isCompleted, id) {
      for (let o of this.allItems) {
        if (o.id === id) {
          o.isCompleted = isCompleted;
          break;
        }
      }
    },
    deleteItem(id) {
      for (let i = 0; i < this.allItems.length; i++) {
        if (this.allItems[i].id === id) {
          this.allItems.splice(i, 1);
          break;
        }
      }
    },
    deleteAllDone() {
      for (let i = this.allItems.length - 1; i >= 0; i--) {
        if (this.allItems[i].isCompleted) {
          this.allItems.splice(i, 1);
        }
      }
    }
  },
  computed: {
    items() {
      return {
        All: this.allItems,
        Active: this.allItems.filter(function(v, i) {
          return !v.isCompleted;
        }),
        Done: this.allItems.filter(function(v, i) {
          return v.isCompleted;
        })
      };
    }
  }
};
</script>

<style scoped>
.todolist {
  flex: 0 1 auto;
  width: 550px;
}
@media screen and (max-width: 600px) {
  .todolist {
    width: 90%;
  }
}
</style>
