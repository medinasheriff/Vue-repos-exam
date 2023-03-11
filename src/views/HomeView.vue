<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div>
    <h2>Medina's Altschool Third Semester Exam (Vue): Question 1.</h2>
    <nav className="navbar">
      <p className="logo">Github Repositories</p>

      <div className="navtabs">
        <RouterLink to="/"> Home </RouterLink>
        <RouterLink to="/about"> Description </RouterLink>
        <RouterLink to="/repos"> Repositories </RouterLink>
        <RouterLink to="/not-found"> Not Found </RouterLink>
      </div>
    </nav>
    <div className="bg"></div>
    <div className="bg2"></div>
    <RouterView />
  </div>
</template>
