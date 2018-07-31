<template>
    <div class="TodoApp">
        <div class="Title">오늘 할 일</div>
        <div class="InputWrapper">
            <input 
                v-model="todo"
                @keypress.enter="addTodo"
                class="TodoInput" 
                type="text" 
                name="todo" 
                autofocus />
            <div class="AddButton" @click="addTodo">추가</div>
        </div>
        <div class="TodoItemList">
        <div class="Line" v-for="(todo, index) in todos" :key="index" @click="onToggle(todo.id)">
            <div class="RemoveButton" @click.stop="onRemove(todo.id)">&times;</div>
            <div class="TodoItem" v-bind:class="{Checked: todo.checked}">{{todo.text}}</div>
            <div v-if="todo.checked" class="CheckMark">&#x2713;</div>
        </div>
    </div>
    </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      id: 3,
      todo: "",
      todos: [
        { id: 0, text: "리액트 소개", checked: false },
        { id: 1, text: "JSX 사용해보기", checked: true },
        { id: 2, text: "라이프 사이클 이해하기", checked: false }
      ]
    };
  },
  methods: {
    addTodo() {
      this.todos = this.todos.concat({
        id: this.id++,
        text: this.todo,
        checked: false
      });
      this.todo = "";
    },
    onToggle(id) {
      const { todos } = this;

      const index = todos.findIndex(todo => todo.id === id);

      const selected = todos[index];

      const nextTodos = [...todos];

      nextTodos[index] = {
        ...selected,
        checked: !selected.checked
      };

      this.todos = nextTodos;
    },
    onRemove(id) {
      //   const index = this.todoList.findIndex(todo => todo.id === id);
      //   this.todoList.splice(index, 1);
      let removed = this.todos.filter(todo => todo.id !== id);
      this.todos = removed;
    }
  }
};
</script>

<style scoped>
.TodoApp {
  width: 50%;
  margin: 0 auto;

  display: flex;
  flex-direction: column;

  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  background: var(--oc-gray-0);
}

.Title {
  display: flex;
  justify-content: center;
  padding-top: 1.25rem;
  padding-bottom: 1.25rem;
  font-size: 2rem;
  font-weight: 700;
  color: var(--oc-gray-8);
  user-select: none;
}

.InputWrapper {
  display: flex;
  align-items: center;
  padding-left: 1rem;
  padding-right: 1rem;
}

.TodoInput {
  flex: 1; /* 버튼을 뺀 빈 공간을 모두 채워줍니다 */
  font-size: 1.25rem;
  height: 2rem;
  outline: none;
  border: none;
  border-bottom: 1px solid #c5f6fa;
}

.TodoInput::placeholder {
  color: var(--oc-indigo-7);
}

.AddButton {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  margin-left: 1rem;
  background: #22b8cf;
  border-radius: 3px;
  color: white;
  font-weight: 600;
  cursor: pointer;
}

.AddButton:hover {
  background: var(--oc-indigo-6);
}

.AddButton:active {
  background: var(--oc-indigo-7);
}

@media screen and (max-width: 320px) {
  .TodoApp {
    width: 100%;
  }
}

@media screen and (max-width: 414px) {
  .TodoApp {
    width: 100%;
  }
}

.TodoItemList {
  display: flex;
  flex-direction: column;
  /* margin: 1rem; */
}
.TodoItem {
  height: 2rem;

  display: flex;
  align-items: center;

  font-size: 1.25rem;
  font-weight: 600;
  padding: 1rem;
}

.Line {
  display: flex;
  align-items: center;
}

.RemoveButton {
  text-align: center;
  padding: 1rem;
  color: var(--oc-red-8);
  opacity: 0;
}

.Line:hover {
  cursor: pointer;
  background: var(--oc-gray-3);
}

.Line:hover .RemoveButton {
  opacity: 1;
}

.Line + .Line {
  border-top: 1px solid var(--oc-gray-8);
}

.Checked {
  color: var(--oc-gray-5);
  text-decoration: line-through;
}

.CheckMark {
  margin-left: auto;
  padding: 1rem;
  color: #3bc9db;
  font-weight: 800;
  font-size: 1.25rem;
}
</style>