<template>
  <div class="hello">
  	<h1>{{ msg }}</h1>
  	<h1>from father: {{ msgfromfather }}</h1>
  	<button v-on:click="onClickMe">open mouse!</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      msg: 'this message is from componentA'
    }
  },
  props: ['msgfromfather'],
  methods: {
  	onClickMe: function () {
  		//console.log(this.msgfromfather)
  		this.$emit('child-tell-me-something', this.msg);
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: darkseagreen;
}
</style>
