<template lang="html">
  <section class="float">
    <section class="main-content-port">


      <h2>Choose your Tld</h2>

      <select v-model="selectedTld">
        <option disabled value="">Please select one</option>
        <option v-for="tld in allTlds" v-bind:value="tld.tld">{{ tld.tld }}</option>
      </select>


    </section>
  </section>
</template>

<script>

import { mapGetters }               from "vuex";

import tlds   from "../../assets/tlds/tlds-parsed.csv";

export default {
  data(){
    return {
      allTlds: null,
      selectedTld: "",
    }
  },
  mounted(){
    this.allTlds = tlds
  },
  watch: {
    selectedTld(){
      console.log(this.selectedTld);
    }
  }
}
</script>

<style lang="css">

  select {
    float:left;
    z-index:10;
    width:  calc(100% - 64px);
    font-size: 22px;
    padding: 8px;
    background: rgb(36, 35, 39);
    border: none;
    color: #81788e;
    font-weight: normal;
    outline: none;
  }

</style>
