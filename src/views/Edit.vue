<template>
  <form @submit.prevent="updateProject">
        <label for="title">Project Title</label>
        <input type="text" v-model="title">
        <label for="detail">Project Detail</label>
        <input type="text" v-model="detail">
        <button>Update Project</button>
    </form>
</template>

<script>
export default {
    props:['id'],
    data(){
        return{
            title:"",
            detail:"",
        }
    },
    mounted(){
        fetch("http://localhost:3000/projects/"+this.id)
        .then((res)=>{
            return res.json();
        })
        .then((data)=>{
            this.title = data.name;
            this.detail = data.detail;
        })
        .catch((error)=>{
            console.log(error)
        })
    },
    methods:{
        updateProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-Type" : "application/json"
                },
                body:JSON.stringify({
                    name:this.title,
                    detial:this.detail,
                })
            })
            .then(()=>{
                this.$router.push('/');
            })
            .catch((error)=>{
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
form{
    width: 50%;
    display: block;
}
label{
    display: block;
    opacity: 0.7;
    margin: 20px 0px;
    width: 100%
}
input{
    display: block;
    border: none;
    border-bottom: 1px solid grey;
    margin-bottom: 10px;
    width: 100%;
    height: 30px;
}
button{
    display: block;
    background-color: rgb(107, 214, 107);
    border-radius: 10px;
    max-width: 30%;
    height: 30px;
    margin: 20px auto;
}
</style>