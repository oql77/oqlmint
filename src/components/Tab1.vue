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
		
		<ul class="todo-list">
      <li v-for="todo in todos1" >
        <div class="view">
          <label @click="sheetVisible = true"  >
            {{ todo.title }}
          </label>
        </div>          
      </li>
    </ul>


		<!-- action-sheet -->
		 <mt-actionsheet :actions="actions" v-model="sheetVisible"></mt-actionsheet>
      <!-- popup -->
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
// import todoStorage from '@/js/store.js'

// 状态
var filters = {
  	all: function (todos) {
   		return todos;
  	},
  	active: function (todos) {
   		return todos.filter(function (todo) {
     		return !todo.completed;
   		});
  	},
  	completed: function (todos) {
   		return todos.filter(function (todo) {
     		return todo.completed;
   		});
  	}
  };

// 存储数据
(function (exports) {
 'use strict';
 var STORAGE_KEY = 'todos-vuejs';
 exports.todoStorage = {
     fetch: function () {
         return JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
     },
     save: function (todos) {
         localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
     }
 };
})(window);



export default {
  name: 'home', 

  data(){
    return{ 
      todos:todoStorage.fetch(),
      popupVisible:false,
      sheetVisible:false,
      actions:[],
      todos1:[]
    } 
   },
   components:{
    Menu
   },
   watch:{
   		
      todos: {
             handler: function (todos) {
               todoStorage.save(todos);
             },
             deep: true
         }
   },

   mounted(){
   	this.actions = [{
      name:'已完成',
      method:this.doneTodo
    },{
   		name:'编辑',
   		method:this.editTodo
   	},{
   		name:'删除',
   		// method:this.removeTodo(todo)
   	}]
   },

   methods:{
   	addPrompt(){
   		var that= this;
   		MessageBox.prompt('添加ToDo').then(({value})=>{
   			if (value) {
   				that.todos1.push({ title: value, completed: false });
   				console.log(that.todos1);
   				MessageBox.alert(`添加的TODO是${value}`,'添加成功')
   			};
   		})
   	},
   	editTodo(){
   	},
   	removeTodo(){
   		this.todos.$remove(todo);
   	}   	
   },

   computed: {
    filteredTodos: function () {
        return filters[this.visibility](this.todos);
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
	background: #CCFFCC;
	height: 45px;
	width: 90%;
	display: inline-block;
	line-height: 45px
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