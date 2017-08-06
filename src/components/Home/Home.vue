<template lang="html">
  <section class="float">
    <section class="main-content-port">


      <section class="intro-text">
        <h1>DomainDictiona.ry</h1>
        <h2>Summary</h2>
        <p>Generate a funky domain name and check it's availability and price.</p>
        <p>Helpful for when you need to operate in reverse. Thikning of a cool domain hack and then checking its unavailable is a ballache!</p>
        <h2>Usage</h2>
        <p>Select a TLD from the dropdown below and cycle through one. You can then query the price and availability.</p>
        <!--<section class="user-options">
          <button type="button" name="button">Most popular words</button>
          <button type="button" name="button">Entire English language</button>
          <button type="button" name="button">All words in treasure island</button>
          <button type="button" name="button">Upload your own definition file!!</button>
        </section>-->

      </section>


      <section class="select-tld pad">

        <select v-model="userSelectedTLD" ref="tldSelectRef">
          <option disabled value="">Please select one</option>
          <option v-for="tld in allTLDs" v-bind:value="tld">{{ tld }}</option>
        </select>


        <div class="navigation-buttons">
          <button type="button" name="button" v-on:click="getPrevOptionIndex" v-bind:disabled="isPrevButtonDisabled">Prev</button>
          <button type="button" name="button" v-on:click="getNextOptionIndex" v-bind:disabled="isNextButtonDisabled">Next</button>
        </div>

      </section>


      <section class="parser pad" v-if="userSelectedTLD">
        <section class="parser-output">
          <button type="button" name="button">Query Whois Availability</button>


          <ul class="website-results">
            <li v-for="tldResult in structuredWords[userSelectedTLD]" class="website-result-item">
              <span class="website-name">
                <a href="#"  class="tld-result-item">{{ tldResult }}</a>
              </span>
              <span class="website-availability"></span>
            </li>
          </ul>

          </ul>
        </section>
      </section>


    </section>
  </section>
</template>

<script>

import { mapGetters }                   from "vuex";

import structuredWords                  from "../../assets/structuredWords.json";

export default {
  data(){
    return {
      allTLDs: [],
      structuredWords: null,
      userSelectedTLD: "",
      isPrevButtonDisabled: false,
      isNextButtonDisabled: false,
      newIndex: null,
    }
  },
  methods: {
    enumerateAndBuildTLDIndex(){
      for (let tld in this.structuredWords){
        if (this.structuredWords[tld].length){
          this.allTLDs.push(tld);
        }
      }
    },
    getNextOptionIndex(){
      this.newIndex = this.$refs.tldSelectRef.selectedIndex + 1;
      if (this.newIndex >= this.allTLDs.length ){
        this.newIndex = 1;
      }
      this.updateSelectOption();
    },
    getPrevOptionIndex(){
      this.newIndex = this.$refs.tldSelectRef.selectedIndex - 1;
      if (this.newIndex <= 0 ){
        this.newIndex = this.allTLDs.length;
      }
      this.updateSelectOption();
    },
    resetArray(){
      this.allMatchingDomainNames = [];
    },
    updateSelectOption(){
      // so other html elements (like <buttons>) can programatically update the model
      this.userSelectedTLD = this.$refs.tldSelectRef[this.newIndex].value;
    }
  },
  mounted(){
    this.structuredWords = structuredWords;
  },
  watch: {
    structuredWords(){
      this.enumerateAndBuildTLDIndex();
    }
  }
}
</script>

<style lang="css">

  select {
    float:left;
    z-index:10;
    width:  100%;
    font-size: 18px;
    padding: 8px;
    background: rgb(31, 31, 33);
    border: none;
    color: #585858;
    font-weight: normal;
    outline: none;
    text-align: center;
    font-family: 'Titillium Web', sans-serif;
    width: 100%;
  }

  .pad {
    float: left;
    width: 100%;
    margin-top: 16px;
    margin-bottom: 16px;
  }

  .tld-result-item {
    padding: 8px;
    margin-right: 8px;
    margin-bottom: 8px;
    background: rgba(255,255,255,0.04);
  }

  .parser-output {
    width: 100%;
  }

  .navigation-buttons {
    margin-top: 32px;
    width: 100%;
    float: left;
  }

  .navigation-buttons button {
    width: 50%;
  }

  .navigation-buttons button[disabled=disabled] {
    opacity: 0.3;
  }

  .intro-text {
  }

  .intro-text h1 {
    font-size: 2em;
    margin-bottom: 4px;
  }

  .intro-text h2{
    font-size: 0.85em;
    margin-bottom: 4px;
  }

  .intro-text p {
    font-size: 0.7em;

  }

  .website-results {
    list-style: none;
  }


  .website-result-item {
    width: 100%;
    float: left;
  }


</style>
