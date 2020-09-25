<!-- 템플릿 주석 -->
 <template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<!-- 스크립트 주석 -->
<script>
// 컴포넌트 불러오기
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      todoItems: []
    }
  },
    
  // 메소드 코드
  methods: {
    // 전체삭제 코드
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
        // 투두리스트 추가 코드
		addTodo(todoItem) {
			localStorage.setItem(todoItem, todoItem);
			this.todoItems.push(todoItem);
		},
    // 투두리스트 삭제 코드
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  // 투두리스트 저장 코드
  created() {
		if (localStorage.length > 0) {
			for (var i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
  },
  // 컴포넌트 불러오기 코드
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }
}
</script>

<!-- 스타일 주석 -->
<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>
