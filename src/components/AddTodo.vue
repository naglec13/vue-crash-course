<template>
  <form @.prevent="onSubmit">
    <input type="text">
    <button type="submit" v-model="title">Create</button>
  </form>
</template>

<script>
export default {
  data(){
    return{
      title: ''
    }
  },
  methods:{
    onSubmit(){
      console.log('submit',this.title)
    }
  }
}
</script>


<style scoped>
  form{
    display: flex;
  }
  input{
    width: 400px;
  }
</style>