<template>
  <div id="app">
    <h1>Ad Targeting</h1>
    <RulesForm />
    <RulesList />
  </div>
</template>

<script>
import RulesForm from './components/RulesForm.vue'
import RulesList from "./components/RulesList";

export default {
  name: 'App',
  components: {
    RulesForm,
    RulesList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
