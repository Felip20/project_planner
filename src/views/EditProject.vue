<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="AddProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button @click="UpdateProject">Update Project</button>
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
    },
    methods:{
        UpdateProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail
                    }
                )
            })
            .then(()=>{
                this.$router.push("/")
            })
        }
    }
}
</script>

<style>

</style>