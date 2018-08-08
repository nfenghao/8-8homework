<template>
  <div>
    <h1>{{msg}}</h1>
    <div>
      <div v-for="item in courseList">
        <li><router-link :to="{name:'detail',params:{id:item.id}}">{{item.name}}</router-link></li>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "course",
    data() {
      return {
        msg: '这是课程',
        courseList: [
          {id: 1, name: '21天学会Python', img: ''},
          {id: 2, name: '21天学会Java', img: ''},
          {id: 3, name: '21天学会Linux', img: ''},
          {id: 4, name: '21天学会大数据', img: ''},
        ]
      }
    },
    mounted() {
      this.init()
    },
    methods: {
      init() {
        var that = this;
        //向后台发送ajax
        console.log('向后台发送请求')
        this.$axios.request({
          url: 'http://127.0.0.1:8000/api/v1/courses/',
          method: 'GET',
          responseType: 'json'
        }).then(function (arg) {
          // 成功之后
          if (arg.data.code === 1000) {
            that.courseList = arg.data.data
          } else {
            alert(arg.data.error);
          }
        }).catch(function (arg) {

        })
      },
    }
  }
</script>

<style scoped>

</style>
