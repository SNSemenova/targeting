<template>
  <form @submit.prevent="addRules">
    <label for="ruleType">Type</label>
    <select id="ruleType" v-model="ruleType">
      <option v-for="option in ruleTypesList" :value="option.id" :key="option.id">{{ option.name }}</option>
    </select>
    <label for="rules">Rules</label>
    <select multiple id="rules" v-model="rules">
      <option v-for="option in rulesList" :value="option.id" :key="option.id">{{ option.name }}</option>
    </select>
    <button type="reset">Reset</button>
    <button type="submit">Add rule</button>
  </form>
</template>

<script>
const BASE_URL = 'https://private-anon-ebead8e484-adcashdsp.apiary-mock.com/';

function getTypesList(path) {
  return fetch(`${BASE_URL}${path}`)
    .then(response => response.text())
    .then(data => {
      // there are trailing commas in json, so I can't parse it
      let result;
      eval(`result = ${data}`);
      return result;
    });
}

export default {
  name: 'RulesForm',
  data() {
    return {
      ruleType: '',
      ruleTypesList: [],
      rules: [],
      rulesList: [],
    }
  },
  async created() {
    this.ruleTypesList = await getTypesList('types');
  },
  watch: {
    async ruleType(newValue) {
      switch (newValue) {
        case 1: {
          this.rulesList = await getTypesList('categories');
          return;
        }
        case 2: {
          this.rulesList = await getTypesList('countries');
          return;
        }
        case 3: {
          this.rulesList = await getTypesList('devices');
          return;
        }
      }
    }
  },
  methods: {
    addRules() {
      return fetch(`${BASE_URL}rules`, {
        method: 'POST',
        body: {
          targeting_type_id: this.ruleType,
          rules: this.rules
        }
      })
        .then(response => response.text())
        .then(data => {
          console.log(data);
        });
    }
  }
}
</script>