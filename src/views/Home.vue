<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @current="current=$event" :cur="current"></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">
      <SingleProject :vic="project" @dele="deleProject"
      @complete="doneProject"></SingleProject>
    </div>
    {{current}}
  </div>
  
</template>

<script>

import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'

export default {
  name: 'Home',
  components: {
    FilterNav,
    SingleProject, 
    },
  data(){
    return{
      projects:[],
      current:""
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
  computed:{
    filterProjects(){
      if (this.current === "complete") {
        return this.projects.filter(project=>{
          return project.complete
        })
      }
      if (this.current === "ongoing") {
        return this.projects.filter(project=>{
          return !project.complete
        })
      }
      return this.projects;
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
