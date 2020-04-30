<template>
  <div class="box">
    <div v-for="(index,item) in info"
         :key="item.id">
      <p>{{info[item].name}}</p>
      <img :src="info[item].album.picUrl" />
      <audio :src='info[item].url'
             controls='true'>
        您的浏览器不支持 audio 标签。
      </audio>
    </div>
  </div>
</template>
<script>
export default {
  name: 'music',
  data () {
    return {
      info: null
    }
  },
  mounted () {
    this.$axios({
      method: 'get',
      url: '/api/search?keyword=周杰伦' // 接口地址
    })
      .then(response => {
        this.info = response.data.data.list
        console.log(response.data.data)
      })
      .catch(error => { console.log(error, 'error', this.errored = true) }) // 失败的返回
      .finally(() => { this.loading = false })
  }
}
</script>
<style scoped>
</style>
