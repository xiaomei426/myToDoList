<template>
  <div id="app">
  	<h1>{{ title }}</h1>
  	<input v-model="newItem" v-on:keyup.enter="addNew">
  	<ul>
  		<li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinished(item)">
  			{{ item.label }}
  		</li>
  	</ul>
  	<p>child tells me: {{ childWords }}</p>
  	<component-a msgfromfather="pia! you die!" v-on:child-tell-me-something="listenToMyBoy"></component-a>
  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/componentA'
export default {
	data: function () {
		return {
			title: 'this is a todo list',
			items: Store.fetch(),
			newItem: '',
			childWords: ''
		}
	},
	components: { ComponentA },
	watch: {
		items: {
			handler: function (items) {
				Store.save(items)
			},
			deep: true
		}
	},
	methods: {
		toggleFinished: function (item) {
			item.isFinished = !item.isFinished
		},
		addNew: function () {
			this.items.push({
				label: this.newItem,
				isFinished: false
			})
			this.newItem= ''
		},
		listenToMyBoy: function (msg) {
			this.childWords = msg;
		}
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
  margin-top: 60px;
}
ul {
	width: 260px;
	margin: 20px auto;
}
.finished {
	text-decoration: underline;
}
p{
	color: powderblue;
}
</style>
