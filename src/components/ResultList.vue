<template>
  <div>
    <div>
      <select
          name="lang"
          v-model="language"
          @change="fetchResults"
          id="lang">
        <!-- ideally, I would fetch all the available languages from another API -->
        <option value="en">en</option>
        <option value="fr">fr</option>
        <option value="es">es</option>
      </select>
    </div>
    <div v-show="hasError">
      Something failed, please try later
    </div>
    <div v-if="!results.length && searchQuery">
      Sorry, no results found...
    </div>
    <ul>
        <li v-for="item in results" :key="item.id">
          <result-list-item
            :item="item"
          ></result-list-item>
        </li>
        <li>
          <div class="search-field">
            <input
                @keyup="fetchResults"
                v-model="searchQuery"
                type="text"
                placeholder="Search for pages containing [x]...">
          </div>
        </li>
      </ul>
  </div>
</template>

<script>
import axios from "axios";
import ResultListItem from "@/components/ResultListItem";
import { debounce } from 'lodash'

export default {
  components: {
    ResultListItem
  },
  data() {
    return {
      results: [],
      language: "en",
      searchQuery: "",
      hasError: false,
    }
  },
  methods: {
    // adding a debounce with 500ms of delay, so the search doesn't fire for every typed character
    fetchResults: debounce(function() {
      this.hasError = false;
      let cleanedQuery = encodeURI(this.searchQuery)
      // don't execute the search if field is empty
      if (!cleanedQuery) return;

      let url = "https://" + this.language + ".wikipedia.org/w/rest.php/v1/search/title?q=" + cleanedQuery + "&limit=10";

      axios.get(url)
          .then(res => {
            this.results = res.data.pages || [];

          }).catch(() => {
            this.results = [];
            this.hasError = true;

      });
    }, 500)
  },
}
</script>
<style>
/*
I would've normally put this in a dedicated css file,
but since it's a prototype, I'm taking advantage of the <style> tags
*/

ul {
  list-style-type: none;
}

.search-field {
  border: 1px solid lightgray;
  background-color: white;
  min-height: 70px;
  position: fixed;
  bottom: 0;
  width: 50%;
}

.search-field input {
  width: 95%;
}

</style>