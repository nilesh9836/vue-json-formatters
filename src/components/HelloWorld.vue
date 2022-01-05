<template>
  <v-container class="pa-0 ma-0 pa-4" fluid style="background-color: violet;">
     <jsonFormatter></jsonFormatter>
  </v-container>
</template>

<script>
  import jsonFormatter from '/src/components/json-formatter.vue';
  export default {
    name: 'HelloWorld',
    components: {
      jsonFormatter
    },


      data() {
    return {
      data: { "store": { "book": [{ "category": "reference", "author": "Nigel Rees", "title": "Sayings of the Century", "price": 8.95 }, { "category": "fiction", "author": "Evelyn Waugh", "title": "Sword of Honour", "price": 12.99 }, { "category": "fiction", "author": "J. R. R. Tolkien", "title": "The Lord of the Rings", "isbn": "0-395-19395-8", "price": 22.99 }], "bicycle": { "color": "red", "price": 19.95 } } },
    };
  }
  }
</script>
