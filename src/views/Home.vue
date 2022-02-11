<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleProject :vic="project" @dele="deleProject"
      @complete="doneProject"></SingleProject>
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
    },
    doneProject(dv){
      let findProject = this.projects.find(project=>{
        return project.id === dv;
      });
      findProject.complete =! findProject.complete 
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
