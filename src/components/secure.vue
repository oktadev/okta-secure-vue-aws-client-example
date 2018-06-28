<template>
  <div>
    <h1>Secure Page</h1>
    <h5>Data from GET /secure-data:</h5>
    <div class="results">
      <pre>{{ data }}</pre>
    </div>
    <div>
      <router-link to="/">Go back</router-link>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      data: null
    }
  },
  async mounted () {
    let accessToken = await this.$auth.getAccessToken()
    const client = axios.create({
      baseURL: 'https://YOUR-ENDPOINT-HERE/dev',
      headers: {
        Authorization: `Bearer ${accessToken}`
      }
    })
    let { data } = await client.get('/secure-data')
    this.data = data
  }
}
</script>

<style>
  .results {
    width:300px;
    margin: 0 auto;
    text-align: left;
    background: #eee;
    padding: 10px;
  }
</style>
