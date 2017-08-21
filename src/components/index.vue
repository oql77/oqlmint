<template>
	<div class="home">
		
		<!-- 脚部 tabbar -->
		<mt-tabbar v-model="tabbarChoice1" fixed>

		  <mt-tab-item id="待办"  @click.native.prevent="selected = '待办0'">
		  	<img slot="icon" src="../assets/Category.png">
		  	待办
		  </mt-tab-item>

		  <mt-tab-item id="待办集" @click.native.prevent="selected = '待办集0'" >
		  	<img slot="icon" src="../assets/nav-list.png">
		  	待办集
		  </mt-tab-item>

		</mt-tabbar> 

		<!-- tabcontainer -->
		 <mt-tab-container v-model="selected" >

			<mt-tab-container-item id="待办0"> 
        <Tab1></Tab1>
			</mt-tab-container-item>

			<mt-tab-container-item id="待办集0">
				<Tab2></Tab2>
			</mt-tab-container-item>

		</mt-tab-container>

	</div>
</template>

<script>
// mintui 引用
import Vue from 'vue'
import { Tabbar, TabItem, TabContainer, TabContainerItem } from 'mint-ui'

Vue.component(Tabbar.name, Tabbar);
Vue.component(TabItem.name, TabItem);
Vue.component(TabContainer.name, TabContainer);
Vue.component(TabContainerItem.name, TabContainerItem);

import Tab1 from '@/components/Tab1.vue'
import Tab2 from '@/components/Tab2.vue'

export default {
  name: 'home', 
  data(){
    return{ 
      selected:'待办0',
      tabbarChoice1:'待办',

    } 
   },
   components:{
    Tab1,
    Tab2
   },
   watch:{
   		selected:{
   			handler:function(val,oldval){
   				console.log(oldval+"_>"+val);
   			}
   		}
   }  
}

</script>
<style>
*{
	margin: 0;
	padding:0;
}
.mint-tab-item-label {
    color: #4caf50;
}
.mint-tab-container {
    margin-top: 50px;
}

</style>