<template>
  <main>
    <h1>{{ title }}</h1>
    <p>{{ date }}</p>
    <div v-html="contents"></div>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from "axios";

export type DataType = {
    contents: any;
}

export default Vue.extend({
    data () {
        return {
            contents: {},
        }
    },
    async asyncData({ params,$config: {baseUrl, apiKey}}){

    console.log('Url:'+ baseUrl)
    console.log('Key:'+ apiKey)
    
    const { data } = await axios.get(
        `${baseUrl}/blog/${params.slug}`,
        {
            headers: { 'X-API-KEY': apiKey }
        }
    )
    return data
  }
})
</script>