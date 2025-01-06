<template>
  <div>
    <!-- <button @click="getPosts">Show Posts</button>
  <hr>
  <h2>{{ post.id }} - {{ post.title }}</h2>
  <p>{{ post.body }}</p> -->
  </div>
</template>

<script>
// export default {
//   name: 'HelloWorld',

//   data() {
//     return {
//       getData: {}, 
//     };
//   },

//   created() {
//     this.waitData(); 
//   },

//   methods: {
//     async waitData() {
//       try {
//         const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
//         this.getData = await response.json();
//         console.log(this.getData); 
//       } catch (error) {
//         console.error('Error fetching data:', error); 
//       }
//     },
//   },
// };

export default{
  name: 'HelloWorld',

  data() {
    return {
      post: {}
    }
  },
  methods: {
    getPosts() {
      fetch('https://jsonplaceholder.typicode.com/posts/1')
        .then(response => response.json())
        .then(data => this.post = data)
    }
  }

}

</script>
