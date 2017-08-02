<template lang="html">
  <section class="float">
    <section class="main-content-port">


      <h2>Choose your Tld</h2>


      <section class="select-tld pad">
        <select v-model="userSelectedTLD">
          <option disabled value="">Please select one</option>
          <option v-for="tld in allExistingTLDs" v-bind:value="tld.tld">{{ tld.tld }}</option>
        </select>
      </section>


      <section class="parser pad" v-if="userSelectedTLD">
        <span>Selected TLD: {{ userSelectedTLD }}</span>
        <section class="parser-status pad" v-if="isProcessing">
          Processing...
        </section>
        <section class="parser-output" v-if="!isProcessing">

          <section class="has-results" v-if="allMatchingDomainNames.length">
            <a href="#" v-for="tldResult in allMatchingDomainNames" class="tld-result-item">{{ tldResult }}</a>
          </section>

          <section class="no-results" v-if="!allMatchingDomainNames.length">
            Sorreh :(
          </section>

        </section>
      </section>


    </section>
  </section>
</template>

<script>

import { mapGetters }               from "vuex";

import tlds                         from "../../assets/tlds/tlds-parsed.csv";
import lotsOfWords                  from "../../assets/words/english-words.json";

export default {
  data(){
    return {
      allExistingTLDs: null,
      allMatchingDomainNames: [],
      userSelectedTLD: "",
      testWords: ["asshat", "factor", "maxtor", "cractor", "tractor", "aeroplane"],
      isProcessing: false,
    }
  },
  methods: {
    organiseMatch(){
      if (!this.isProcessing){
        this.isProcessing = true;
        this.searchArrayForMatches();
      }
    },
    resetArray(){
      this.allMatchingDomainNames = [];
    },
    searchArrayForMatches(){
      this.lotsOfWords.forEach((word, iteration) => {
        // will return the index if it exists or -1 if not
        let test = word.indexOf(this.userSelectedTLD);
        // important... to make a tld hack it needs to go at the end like rome.ro so cant be in the middle or start of the string
        // this means that the length of the 2 words subtracted must equal the index of the start position
        let cropPosition = Math.abs(this.userSelectedTLD.length - word.length);
        // match
        if (test > 0){
          if (cropPosition === test){
            let hostName = word.slice(0, cropPosition);
            let domainName = `${hostName}.${this.userSelectedTLD}`;
            this.allMatchingDomainNames.push(domainName);
          }
        }
        // todo = make this a promise
        this.isProcessing = false;
      });
    }
  },
  mounted(){
    this.allExistingTLDs = tlds;
    this.lotsOfWords = lotsOfWords;
  },
  watch: {
    userSelectedTLD(){
      this.resetArray();
      this.organiseMatch();
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

  .pad {
    float: left;
    width: 100%;
    margin-top: 32px;
    margin-bottom: 32px;
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

</style>
