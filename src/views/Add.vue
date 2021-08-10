<template>
    <h2>Add Projects</h2>
    <form @submit.prevent="addProject">
        <label for="title">Project Title</label>
        <input type="text" v-model="title">
        <label for="detail">Project Detail</label>
        <input type="text" v-model="detail">
        <button>Add Project</button>
    </form>
</template>

<script>
export default {
    data(){
        return{
            title: "",
            detail: "",
            api: "http://localhost:3000/projects"
        }
    },
    methods:{
        addProject(){
            fetch(this.api,{
                method: "POST",
                headers:{
                    "Content-Type" : "application/json"
                },
                body:JSON.stringify(
                    {
                        name: this.title,
                        detail: this.detail,
                        isComplete: false,
                    }
                )
            })
            .then(()=>{
                this.$router.push('/')
            })
            .catch(err=>{
                console.log(err)
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