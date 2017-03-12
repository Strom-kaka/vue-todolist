# vue-todolist

``` bash

用 vue实现 todolist功能还是非常简单的
在这我没有加任何样式，但是各种功能还是非常完善的

1. 利用 v-model 指令绑定输入框内容
	<input type="text" placeholder="what to do?" v-model="newLabel">
	<button @click="add(newLabel)">add</button>	

		add: function(text) {
			if(text) {
				var item = {
					label : text,
					isFinished: false
				};
				this.items.push(item);
				this.newLabel = '';
			}
		}	
	利用增加方法来给数组添加新的内容（屏蔽添加空内容）；
		
2. 利用 v-for 指令 循环数据

<ul>
	<li v-for="item in items" v-show="needShow(item)">
		<input type="checkbox" v-model="item.isFinished" >
		<span>{{item.label}}</span>
		<button @click="del(item)">X</button>
	</li>
</ul>

利用 v-model 更改数据完成状态

del: function(item) {
	var index = this.items.indexOf(item);
	this.items.splice(index,1);
}

利用 indexOf()查询索引并用 splice() 来删除数组中指定元素

3.分类显示数据（全部、未完成、已完成）；

<div>
	<button @click="selectedType(0)">ALL {{items.length}}</button>
	<button @click="selectedType(1)">NOTFINISHED {{notfinished.length}}</button>
	<button @click="selectedType(2)">COMPLETED {{completed.length}}</button>
</div>

selectedType(num) {
	this.type = num;
},

needShow(item) {
	if(this.type === 0) {
		return true;
	} else if (this.type === 1) {
		return item.isFinished === false;
	}else if (this.type === 2) {
		return item.isFinished === true;
	}
}
给每个类型设定特定 type值，并用needShow来确定需要显示的数据类型

4.监听数据变化并缓存到本地

vm.$watch('items',function() {
	this.save(this.items);
},{
	deep: true
});	


5.获取本地缓存数据

function fetch(){
    return JSON.parse(localStorage.getItem(STORAGE_KEY)||'[]');
}







