<template>
  <div class="project" :class="{complete: project.isComplete }">
      <div class="flexing">
        <div @click="showDetail=!showDetail">
          <h3>{{project.name}}</h3>
        </div>
        <div>
          <span class="material-icons" @click="deleteProject">
          delete
          </span>
          <router-link :to="{name:'Edit',params:{id:project.id}}">
            <span class="material-icons">
            edit
            </span>
          </router-link>
          <span class="material-icons" @click="completeProject">
          done
          </span>
        </div>
      </div>
      <div v-if="showDetail">
        <p>{{project.detail}}</p>
      </div>
      
  </div>
</template>

<script>
export default {
props:['project'],
  data(){
    return{
      showDetail : false,
      api: "http://localhost:3000/projects/"
    }
  },
  methods: {
    deleteProject(){
      let deleteApi = this.api+this.project.id;
      fetch(deleteApi,{method: "DELETE"})
      .then(()=>{
        this.$emit("delete",this.project.id)
      })
      .catch((error)=>
      {
        console.log(error)
      })
    },
    completeProject(){
      let updateApi = this.api+this.project.id;
      fetch(updateApi,{
          method:"PATCH",
          headers:{
            "Content-Type":"application/json"
          },
          body:JSON.stringify(
            {
              isComplete:!this.project.isComplete
            }
          )
        }
      )
      .then(()=>
      {
        this.$emit("completProject",this.project.id)
      })
      .catch((error)=>{
        console.log(error);
      })
    }
  }
}
</script>

<style>
.project{
  padding: 20px;
  background-color: #f2f2f2;
  margin: 10px;
  border-radius: 10px;
  border-left: 6px solid red;
}
 p{
  text-align: left;
}
h3{
  cursor : pointer;
}
span{
  cursor : pointer;
  margin-left: 15px;
}
.flexing{ 
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.complete{
  border-left: 6px solid green;
}
</style>