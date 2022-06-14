<template>
  <div class="hello">
    <input 
    v-model="postContent"
    type="text" id="createPost">
    <button
    @click="createContent"
    >POST</button>
    <button
    @click="getContent"
    >GET</button>
    <div
    v-for="poster in postArr"
    :key="poster.id"
    >
    {{poster.id}}
    {{poster.posterContent}}
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data(){
    return{
      postContent: null,
      postArr : []
    }
  },
  methods: {
    createContent() {
      axios.request({
        url : "http://127.0.0.1:5000/api/poster",
        method : "POST",
        data : {
          posterContent : this.createContent
          // name of column in API : what we grab off of this page
        },
      }).then(()=>{
        this.getContent();
      }).catch((error)=>{
        console.log(error);
      })
      // create content is referenced at the @click
      console.log(this.createContent);
    },
    getContent(){
      axios.request({
        url : "http://127.0.0.1:5000/api/poster",
        method : "GET"
      }).then((response)=>{
        console.log(response);
        this.postArr = response.data
      }).catch((error)=>{
        console.log(error);
      })
    },
    mounted () {
      this.getContent();
    },
  },  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">


</style>
