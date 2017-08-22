<template>


<div class="home">
    <!-- header -->
    <mt-header fixed title="葡萄ToDo">
        <mt-button  slot="left"  @click.native="popupVisible = true">
          <img src="../assets/menu.png">
        </mt-button>
        <mt-button class="mr10" slot="right" @click.native="addPrompt">
          <img src="../assets/add.png">
        </mt-button>
        <mt-button  slot="right">
          <img src="../assets/more.png">
        </mt-button>
    </mt-header>

    <!-- 内容容器 -->
    <ul class="todo-list">
      <li v-for="(todo,index) in todos1" :class="todo.completed ? 'classA' : 'classB' ">
        <div class="view">
          <label @click="getIndex(index)" >
            {{ todo.title }}
          </label>
        </div>          
      </li>
    </ul>

     <!-- 一系列弹出框 -->

    <!-- action-sheet 点击TODO事件后屏幕下方弹出选项 -->
     <mt-actionsheet :actions="actions" v-model="sheetVisible"></mt-actionsheet>

    <!-- popup  点击弹出左侧导航菜单-->
     <mt-popup v-model="popupVisible" position="left" class="popup-3" popup-transition="popup-fade">
        <Menu></Menu>   
    </mt-popup>

  </div> 

</template>

<script>

// mintui 引用
import Vue from 'vue'
import { Popup, MessageBox, Actionsheet } from 'mint-ui'
Vue.component(Popup.name, Popup)
Vue.component(MessageBox.name, MessageBox);
Vue.component(Actionsheet.name, Actionsheet);
import Menu from '@/components/Menu.vue'

// 状态
var filters = {
  	all: function (todos1) {
   		return todos;
  	},
  	active: function (todos1) {
   		return todos1.filter(function (todo) {
     		return !todo.completed;
   		});
  	},
  	completed: function (todos1) {
   		return todos.filter(function (todo) {
     		return todo.completed;
   		});
  	}
  };


export default {
  name: 'home', 

  data(){
    return{ 
      popupVisible:false,     //左侧导航菜单不可见
      sheetVisible:false,     //action-sheet组件不可见
      actions:[],             //存放action-sheet组件里的选项数据name和methods
      todos1:[],              //数组，存放每次添加TODO事件push进来的数据
      index:'',               //存放点击todos1数组对象所获得相对应的下标index
      value:'',               //存放index相对应的todos1.title数据
      activeColor :'red',
    } 
   },
   components:{
    Menu          //左侧导航菜单
   },
   // watch:{
   //    todos: {
   //           handler: function (todos1) {
   //             todoStorage.save(todos1);
   //           },
   //           deep: true
   //       }
   // },
   mounted() {
    // 钩子函数，action-sheet组件里的选项数据name和methods
      this.actions = [{
        name: '已完成',
        method: this.doneTodo
      }, {
        name: '编辑',
        method: this.editTodo     
      }, {
        name: '删除',
        method: this.removeTodo
      }];
    },

   methods:{
    // 函数方法

    // 弹出信息框
   	addPrompt(){
   		var that= this;
   		MessageBox.prompt(' ','添加ToDo').then(({ value }) => {
   			if (value) {
   				that.todos1.push({ title: value, completed: false });
   				console.log(that.todos1);
   				MessageBox.alert(`添加的TODO是${value}`,'添加成功')
   			};
   		})
   	},

    // 使action-sheet组件可见，并且获取相对应下标index和内容title，分别放进全局参数index和value
    getIndex(index){
      this.sheetVisible = true;
      this.index = index;
      this.value = this.todos1[this.index].title;
    },

    doneTodo(){
      this.todos1[this.index].completed = true ;

    },

    // 点击编辑选项，弹出信息框，输入并编辑
   	editTodo(){
      MessageBox.prompt(' ', '编辑ToDo', {inputPlaceholder: this.value} ).then(({ value, action }) => {
        this.todos1[this.index].title = value;
      })
   	},

    // 点击删除选项，从数组todos1中删除对应的数据
   	removeTodo(index){
   		this.todos1.splice(this.index,1);
   	}   	
   },

   computed: {
    filteredTodos: function () {
        return filters[this.visibility](this.todos1);
    }
   }
   
}

</script>
<style>
*{
	margin: 0;
	padding:0;
}
.mr10{
  margin-right:10px;
}
.mint-header {
	background-color: #66CCCC
}
ul{
	list-style:none; 
}
.todo-list li{
	text-align: center;
	margin: 10px 0;
	height: 45px;
	width: 90%;
	display: inline-block;
	line-height: 45px
}
.classA{
  background: #dbdbdb;
}
.classB{
  background: #ccffcc
}
label {
    width: 100%
}
.popup-3 {
        width: 80%;
        height: 100%;
        background-color: #fff;
      }
</style>