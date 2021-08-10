<template>
  <nav class="main">
    <router-link to="/">Projects</router-link>
    <router-link :to="{name:'Add'}">Add Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
    .main{
    display: block;
    margin: 20px auto;
    }
    .main a{
        text-decoration: none;
        font-weight: 100;
        color: grey;
        margin: 10px 10px;
    }
    .main .router-link-active{
        text-decoration: underline;
    }

</style>