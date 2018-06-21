<template>
  <div id="app">
    <leftNav></leftNav>
    <div class="main" id="main">
      <router-view/>
    </div>
  </div>
</template>

<script>
import leftNav from '@/components/common/leftNav'
import Pos from '@/components/page/Pos'
export default {
  name: 'App',
  components:{
      leftNav,
      Pos
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow: hidden;
}
body{
  margin: 0;
  padding: 0;
}
.main{
  float: left;
  width: 95%;
}
</style>
<!--笔记 Vue 实战 第四节 编写独立的侧边栏组件-->
<!--
1.用正常的流程写组件，在App.vue中import xx from '@/components/common/xx'，
2.注册此组件components:{
    xx
}
3.在结构中用<xx></xx>直接使用组件
4.Vue是复用一切可以复用的结构，真把DOM当模板了，
-->

<!--笔记 Vue 第五节 开启Element封印-->
<!--
1.Element是饿了么前端推出的依据Vue2.0框架开发的前端组件，仿BootstrapUI框架
-->

<!--笔记 Vue 第六、七节 利用Element快速布局(1)(2)-->

<!--笔记 Vue 第八节 使用Axios从远程获取数据-->
<!--
1.Axios是依据原生ES6 promise实现的HTTP库，首先环境要支持promise。
2.用法:get请求
axios.get('')
  .then(response => {

  })
  .catch(error = > {

  });
或者
axios.get('',{
    params: {
      id: xxx
    }
  })
 .then(response=>{

 })
 .catch(error=>{

 });
3.用法:post请求
axios.post('',{
    fitstName: xxx,
    lastName: xxx
  })
  .then(response=>{

  })
  .catch(error=>{

  });
4.用法:执行多个并发请求
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}
axios.all([getUserAccount(),getUserPermissions])
 .then(axios.spread(function(){
    //等请求都执行完
 }));
5.用法: axios API
axios({
  method: 'post',
  url: 'xxx',
  data: {
    firstName: xxx,
    lastName: xxx
  }
});
6.创建实例:
var instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
7.总结:
后面要把webpack、axios的配置文档，从头到尾看一遍，细究原理。
-->
