<!-- 템플릿 주석 -->
 <template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="오늘 할일을 입력하세요" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fa fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">할 일을 입력하세요.
        <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<!-- 스크립트 주석 -->
<script>
// 임포트 코드
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false
    }
  },
    // 메소드 코드
  methods: {
      // 투두리스트 추가 코드
    addTodo() {
      if (this.newTodoItem !== "") {
        var value = this.newTodoItem && this.newTodoItem.trim();
				this.$emit('addTodo', value)
        this.clearInput();
       fetch("http://localhost:8888/save", {
          method: "post",
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },

          body: JSON.stringify({
            text: this.newTodoItem
          })
        })
      } else {
        this.showModal = !this.showModal;
      }
    },
      // 투두리스트 삭제 코드
    clearInput() {
      this.newTodoItem = '';
    }
  },
    // 컴포넌트 불러오기 코드
  components: {
    Modal: Modal
  }
}
</script>

<!-- 스타일 주석 -->
<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  position:fixed;
    top:40px;
    right:10px;
  background:#ee2375;
  display: inline-block;
  width: 3rem;
  border-radius:5px;
    cursor:pointer;
}
.addBtn {
  color: white;
  vertical-align: middle;
    transition:all 0.4s;

}
.addContainer:hove{transform:rotate(360deg);}
</style>
