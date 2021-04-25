<template>
  <main>
    <h1>ブログ一覧</h1>
    <ul>

      <li v-for="content in contents" :key="content.id">
        <a :href='`/blog/${content.id}`'>
          {{ content.title }}
        </a>
      </li>
    </ul>
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
    async asyncData({$config}){

            const { data }  = await axios.get(
                `${$config.baseUrl}/blog`,
                {
                    headers: { 'X-API-KEY': $config.apiKey }
                }
            )   
            return data;
    },
    methods:{
        // async asyncData() {

            // const self = <DataType>this

            // const apiKey = process.env.API_KEY;
            // const url = process.env.blog_url;

            // console.log('Key:' + apiKey);
            // console.log('Url:' + url);
            // if(!apiKey || !url){return};
            
            // self.contents = await axios.get(
            //     ``,
            //     {
            //         headers: { 'X-API-KEY': 'deaab22f-3276-4aed-8dd2-d35c1ceb6d55' }
            //     }
            // )   
            // console.log('data:' + self.contents);
        // }
    }
})
</script>
