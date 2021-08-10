<template>
  <nav class="filter-nav">
      <button @click="filter('all')" :class="{ active : current == 'all' }">all</button>
      <button @click="filter('complete')" :class="{ active : current == 'complete' }">complete</button>
      <button @click="filter('ongoing')" :class="{ active : current == 'ongoing' }">on-going</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filter(value)
        {
            this.$emit("filterProject",value);
        }
    }
}
</script>

<style scoped>
    .filter-nav button{
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        margin-right: 10px;
        text-transform: uppercase;
        letter-spacing: 1px;
        cursor: pointer;
        font-weight: bold;
    }
    button.active{
        color: #333;
    }
</style>