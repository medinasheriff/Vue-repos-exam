<script setup>
import {ref, computed, onMounted} from "vue"
import { useRouter } from "vue-router";

const repos = ref([]);
  const loading = ref(false);
  const usersPerPage = 5;
  const pages = ref(1);
  const router = useRouter()

  const fetchData = async () => {
      try {
        loading.value = true;
        const response = await fetch(
          "https://api.github.com/users/medinasheriff/repos"
        );
       const data = await response.json() ;

        repos.value = data
        
        console.log(repos.value)
        loading.value =false;
      } catch (error) {
        console.log(error)
      }
    };

    const slicedRepos = computed(() => {
        return repos.value.slice((pages.value - 1) * usersPerPage, pages.value * usersPerPage);
     
    })

    onMounted(() => {
        fetchData()
    })

</script>

<template>
    <h2 v-if="loading">Loading...</h2>
    <div v-else>
      <h3 className="github">My {{repos.length}} Github Repositories.</h3>
      <div className="repos-container">
        <div className="repos">
            <div v-for="repo in slicedRepos" className="repo" :key="repo.id">
                  <RouterLink :to="`repos/${repo.name}`">{{repo.name}}</RouterLink>
                  <h4>{{repo.language}}</h4>
                  <p>{{repo.visibility}}</p>
                </div>
        </div>
        <div>
          Pages {{pages}} of {{ Math.ceil(repos.length / usersPerPage)}}
        </div>
        <button
          :disabled="pages <= 1"
          @click="pages--"
       
        >
          Prev
        </button>

        <button
        v-for="btn in Math.ceil(repos.length / usersPerPage)"
            :key="btn"
            :class="{active: pages === btn}"
            @click="pages = btn"
          >
            {{btn}}
          </button>
        <button
          :disabled="pages >= repos.length / usersPerPage"
          @click="pages++"
        >
          Next
        </button>
      </div>
      <button className="btn2" @click="router.push('/')">Back</button>
      
    </div>
</template>