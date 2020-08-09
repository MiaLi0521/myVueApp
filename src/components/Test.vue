<template>
  <div class="test">
    <!-- 获取数据 -->
    <h1>{{ title }}</h1>
    <p>{{ user.firstName }}</p>
    <p v-text="user.lastName"></p>

    <!-- v-if -->
    <p v-if="showName">{{ user.firstName }}</p>
    <!-- v-else -->
    <p v-else>Nobody</p>

    <!-- v-for -->
    <ul>
      <li v-for="item in items">{{item.title}}</li>
    </ul>

    <!-- v-on 事件绑定-->
    <button v-on:click="greet('Hello Mia!')">Say Greeting</button>
    <!-- 键盘事件 -->
    <input type="text" v-on:keyup="pressKey" v-on:keyup.enter="enterHit">

    <!-- computed 计算属性 -->
    <label>First Name:</label>
    <input type="text" v-model="user.firstName">
    <br>
    <label>Last Name:</label>
    <input type="text" v-model="user.lastName">

    <h3>
      <label>Full Name:</label>
      <label>{{ fullName }}</label>
    </h3>

    <!-- props 属性 传值-->
    <h2>{{ msg }}</h2>
  </div>
</template>

<script>
export default {
  // 组件对外公开，使外部可以引用
  name: "test",
  props: {
    msg: {
      type: String,
      default: "默认就是这些文字!"
    }
  },
  data() {
    return {
      title: "Hello mia!",
      user: {
        firstName: "Mia",
        lastName: "Li"
      },
      showName: true,
      items: [
        { title: "item 1" },
        { title: "item 2" },
        { title: "item 3" },
        { title: "item 4" }
      ]
    };
  },
  methods: {
    greet: function(greeting) {
      alert(greeting);
    },
    pressKey: function() {
      console.log("Pressing.... ....");
    },
    enterHit: function() {
      console.log("You pressed enter key...");
    }
  },
  computed: {
    fullName: function() {
      return this.user.firstName + " " + this.user.lastName;
    }
  }
};
</script>

<style scoped>
/*scoped标识: 划分局部作用域，只对当前组件生效*/
</style>


