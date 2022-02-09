<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleProject :vic="project" @dele="deleProject"></SingleProject>
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject'

export default {
  name: 'Home',
  components: {
    SingleProject, 
    },
  data(){
    return{
      projects:[]
    }
  },
  methods:{
    deleProject(dv){
      this.projects = this.projects.filter(project =>{
        return project.id!= dv;
      })
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json()
    })
    .then((data)=>{
      this.projects=data
    })
    .catch(()=>{

    })
  }
}
</script>
