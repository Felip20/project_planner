<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="AddProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
    props:["id"],
    data(){
        return{
            title:"",
            detail:""
        }
    },
    mounted(){
        fetch("http://localhost:3000/projects/"+this.id)
        .then((response)=>{
            return response.json()
        })
        .then((datas)=>{
            this.title = datas.title,
            this.detail = datas.detail
        })
        .catch(()=>{

        })
    }
}
</script>

<style>

</style>