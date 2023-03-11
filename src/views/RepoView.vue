<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';


const repo = ref({});
const loading =ref(false);
  
const {params} = useRoute();
const router = useRouter()
const url = `https://api.github.com/repos/medinasheriff/${params.name}`;


const fetchData = async () => {
      try {
        loading.value = true;
        const response = await fetch(
         url
        );
       const data = await response.json() ;

        repo.value = data
        
        console.log(repo.value)
        loading.value =false;
      } catch (error) {
        console.log(error)
      }
    };

    onMounted(() => {
        fetchData()
    })
</script>

<template>
    <div v-if="loading">Loading...</div>

<div className="data" v-else>
      <h2 className="repo-head">Repository Data</h2>
      <p>
        <h3>Description:</h3> {{repo.description}}
      </p>
      <p>
        <h3>Name:</h3> {{repo.name}}
      </p>
      <p>
        <h3>ID:</h3> {{repo.id}}
      </p>
      <p>
        <h3>Date of Creation:</h3> {{repo.created_at}}
      </p>
      <button className="btn" @click="router.push('/repos')">Back</button>
    </div>
</template>