<template>
  <h1>Add Project</h1>
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
  data(){
    return{
        title:"",
        detail:""
    }
  },
  methods:{
    AddProject(){
      fetch("http://localhost:3000/projects",{method:"POST",
      headers:{
        "Content-Type":"application/json"
      },
      body:JSON.stringify(
        {
          title:this.title,
          detail:this.detail,
          complete:false
        }
      )
      })
      .then(()=>{
        this.$router.push("/")
      })
      .catch(()=>{

      })
    }
  }
}
</script>

<style>
form{
  background:white;
  padding: 20px;
  border-radius: 10px;
}
label{
  display: block;
  color: aqua;
  text-transform: uppercase;
  font-style: italic;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input{
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea{
  border: 1px solid #ddd;
  padding: 10px;
  height: 100px;
  width: 100%;
  box-sizing: border-box;
}
form button{
  display: block;
  margin: 20px auto 0;
  background: cadetblue;
  color: #000;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>