<template>
  <div>
    <ul id="todolist">
      <li v-for="(item, index) in items" v-bind:key="item.id">
        {{ item.message }}<button id="remove-button" @click="$emit('remove', $event, index)">削除</button>
      </li>
    </ul>
  </div>
</template>
 
<script>
export default {
  name: 'todo-list',
  props: {  
    items: {
      type: Array,
      default: function() {
        return [];
      }
    },
  },
}
</script>
 
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  /* list-style-type: none; */
  text-align: left;
  padding: 0;
  width: 100px;
  white-space: nowrap;
  margin: auto;
}
li {
  display: list-item;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>