<template>
  <div class="users">
    <h1>Users</h1>

    <!-- 添加用戶信息 -->
    <form v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="输入姓名">
      <input type="text" v-model="newUser.email" placeholder="输入邮箱">
      <input type="submit" value="Submit">
    </form>

    <!-- 展示用戶信息 -->
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span :class="{contacted:user.contacted}">
          {{user.name}} : {{ user.email }}
          <button v-on:click="deleteUser(user)">X</button>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  // 组件对外公开，使外部可以引用
  name: "users",
  data() {
    return {
      newUser: {},
      users: [
        {
          name: "Mia Li",
          email: "miaLi0521@outlook.com",
          contacted: false
        },
        {
          name: "Mia2 Li",
          email: "miaLi0522@outlook.com",
          contacted: false
        },
        {
          name: "Mia3 Li",
          email: "miaLi0523@outlook.com",
          contacted: false
        }
      ]
    };
  },
  methods: {
    addUser: function(e) {
      //   console.log('Hello');
      this.users.push({
        name: this.newUser.name,
        email: this.newUser.email,
        contacted: false
      });
      e.preventDefault();
    },
    deleteUser: function(user) {
      this.users.splice(this.users.indexOf(user), 1);
    }
  },
  created: function(){
    this.$http.get('http://jsonplaceholder.typicode.com/users').then(function(response){
      // console.log(response);
      this.users = response.data;
    });
  }
};
</script>

<style scoped>
/*scoped标识: 划分局部作用域，只对当前组件生效*/
  .contacted{
    text-decoration: line-through;
  }
</style>


