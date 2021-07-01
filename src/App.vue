<template>
  <div id="app">
    <div class="todoList">
      <div class="top">
        <img src="https://img.onl/pxxRwn" alt>
        <div class="opacity"></div>
        <div class="time">
          <span>{{nowDay}}</span>
          <span>{{nowMonth}}</span>
          <span>{{nowYear}}</span>
        </div>
      </div>
      <p class="middleWord">Do something !</p>
      <div class="list">
        <div class="input" v-if="!isEditing">
          <input type="text" v-model="todo" class="textArea">
          <span class="click" @click="storeTodo">Add</span>
        </div>
        <div class="input" v-else>
          <input type="text" v-model="todo" class="textArea editing">
          <span class="click" @click="updateTodo">Update</span>
        </div>
        <ol>
          <li v-for="(todo,index) in todos" :key="index">
            <div class="listData">
              <p>{{index+1+'.'}}</p>
              <p>{{todo}}</p>
            </div>

            <div class="actions">
              <div class="action click" @click="editTodo(todo,index)">
                <img src="https://img.onl/lVN0ML" alt>
              </div>
              <div class="action click" @click="deleteTodo(index)">
                <img src="https://img.onl/eSMh54" alt>
              </div>
            </div>
          </li>
        </ol>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "app",
  data() {
    return {
      nowDay: "",
      nowMonth: "",
      nowYear: "",
      isEditing: false,
      selectedIndex: null,
      todo: "",
      todos: ["Try to edit me!", "Try to delete me !"]
    };
  },
  components: {},
  methods: {
    getTime() {
      var dt = new Date();
      var month = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ];
      this.nowDay = dt.getDate();
      this.nowMonth = month[dt.getMonth()];
      this.nowYear = dt.getFullYear();
    },
    storeTodo() {
      console.log("storeTodo");
      this.todos.push(this.todo);
      this.todo = "";
    },
    editTodo(todo, index) {
      console.log("editTodo");
      this.todo = todo;
      this.selectedIndex = index;
      this.isEditing = true;
    },
    deleteTodo(index) {
      console.log("deleteTodo");
      this.todos.splice(index, 1);
    },
    updateTodo() {
      console.log("updateTodo");
      this.todos.splice(this.selectedIndex, 1, this.todo);
      this.todo = "";
      this.isEditing = false;
    }
  },
  created() {},
  mounted() {
    this.getTime();
  }
};
</script>


<style lang="scss">
* {
  font-family: "Helvetica", "Arial", "LiHei Pro", "黑體-繁", "微軟正黑體",
    sans-serif;
  letter-spacing: 2px;
}
html,
body {
  width: 100%;
  height: 100%;
  background-color: #f6f2ef;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
}
.todoList {
  width: 350px;
  min-height: 500px;
  background-color: #fffefe;
}
.top {
  width: 100%;
  overflow: hidden;
  height: 162px;
  position: relative;
  img {
    position: absolute;
    top: -170%;
    left: 0%;
    width: 100%;
  }
}
.opacity {
  width: 100%;
  height: 100%;
  background-color: #fff;
  opacity: 0.4;
  position: absolute;
  top: 0;
  left: 0;
}
.time {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 24px;
  font-weight: bold;
  letter-spacing: 2px;
  color: #333333;
  span {
    margin-bottom: 5px;
  }
  span:nth-last-child(1) {
    font-size: 14px;
    font-weight: 400;
    margin-top: 5px;
  }
}
.middleWord {
  text-align: center;
  color: #707070;
  font-weight: 500;
  border-bottom: 1px solid #999999;
  padding-bottom: 16px;
}
.list {
  width: 85%;
  margin: auto;
}
.input {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20px 0 25px 0;
  span {
    color: #707070;
  }
}
.textArea {
  width: 79%;
  border: 1px solid #c5c5c5;
  border-radius: 3px;
  padding: 5px 8px;
  background-color: #fffefe;
}
.editing {
  width: 70%;
}
ol {
  padding-inline-start: 0;
  color: #707070;
  height: 200px;
  overflow: scroll;
}
ol::-webkit-scrollbar {
  display: none;
}
li {
  padding-left: 5px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.listData {
  display: flex;
  p:nth-child(1) {
    margin-right: 7px;
  }
}
.actions {
  display: flex;
}
.action {
  width: 20px;
  overflow: hidden;
  margin-left: 10px;
  img {
    width: 100%;
  }
}
.click {
  cursor: pointer;
}
</style>