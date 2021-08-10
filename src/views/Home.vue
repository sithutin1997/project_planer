<template>
  <h1>Projects</h1>
  <FilterNav @filterProject="current=$event" :current="current"></FilterNav>
  <div v-for="project in filteredProject" :key="project.id">
    <Project :project="project" @delete="deleteProject" @completProject="completeProject"></Project>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import Project from '../components/Project'
// @ is an alias to /src
export default {
  data(){
    return{
      projects : [],
      current : "all",
    }
  },
  components: {
    FilterNav,
    Project, 
  },
  computed:{
    filteredProject(){
      if(this.current === "complete")
      {
        return this.projects.filter((p)=>{
          return p.isComplete === true
        })
      }
      if(this.current === "ongoing")
      {
        return this.projects.filter((p)=>{
          return p.isComplete === false
        })
      }
      return this.projects;
    }
  },
  mounted(){
    fetch("http://localhost:3000/projects")
    .then(response=>{
      return response.json();
    })
    .then(datas=>{
      this.projects = datas;
    })
    .catch(error=>{
      console.log(error.message());
    })
  },
  methods: {
    deleteProject(id){
      this.projects=this.projects.filter((project)=>
      {
        return project.id != id;
      })
    },
    completeProject(id){
      let findProject = this.projects.find((project)=>
      {
        return project.id == id;
      });
      findProject.isComplete = !findProject.isComplete;
    }
  }
}
</script>
