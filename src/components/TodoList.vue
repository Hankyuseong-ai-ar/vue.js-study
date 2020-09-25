<!-- 템플릿 주석 -->
<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
        <i class="checkBtn fa fa-check" aria-hidden="true"></i>
        {{ todoItem }}
        <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
          <i class="fa fa-trash-o" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<!-- 스크립트 주석 -->
<script>
// 메소드 코드
export default {
  // 데이터 전달 props
  props: ['propsdata'],
  
  // 메소드 코드
  // 투두리스트 삭제 코드
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    }
  }
}
</script>

<!-- 스타일 주석 -->
<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
      transition:all 0.4s;
  }
    li:hover{
        background:#42aafd;
        color:white;
    }
  .checkBtn {
    line-height: 45px;
    color: #ee2375;
    margin-right: 5px;
    transition:all 0.4s;
  }
  .removeBtn {
    margin-left: auto;
    color: #de4343;
    cursor: pointer;
    transition:all 0.4s;
  }
   li:hover .checkBtn, li:hover .removeBtn{color:white;}
  .list-item {
    display: inline-block;
    margin-right: 10px;
  }
  .list-move {
    transition: transform 1s;
  }
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
</style>
