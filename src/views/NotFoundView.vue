<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div className="error">
      <h4>Oops! ERROR 404. <br/>Cant't find searched page. <br/>Please, check your URL or Click {" "}
      <RouterLink to="/"> here </RouterLink>  to go back Home.</h4>
    </div>
</template>