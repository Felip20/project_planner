<template>
  
  <nav class="filter-nav">
      <button @click="filterBy('all')" :class="{ active : cur === 'all'}">All</button>
      <button @click="filterBy('complete')" :class="{ active : cur === 'complete'}">Complete</button>
      <button @click="filterBy('ongoing')" :class="{ active : cur === 'ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['cur'],
    methods:{
        filterBy(value){
            this.$emit("current",value);
        }
    }
}
</script>

<style>
.filter-nav button{
    background: none;
    border: none;
    color: #bbb;
    font-size: 12px;
    outline: none;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
button.active{
    color: #333;
}
</style>