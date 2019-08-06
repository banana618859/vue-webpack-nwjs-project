<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ msg2 }}</h1>
    <p>
      <button @click="doSome">按钮</button>
    </p>
    <h3 style="text-align:left;">
       也可以http请求数据：
    </h3>
    <div style="border:5px solid red; height:300px; overflow:auto;">
       <el-table
        :data="tableDataMusic"
        border
        style="width: 100%">
        <el-table-column
          prop="cate_sname"
          label="cate_sname"
          width="180">
        </el-table-column>
        <el-table-column
          prop="ch_name"
          label="ch_name"
          width="180">
        </el-table-column>
        <el-table-column
          prop="name"
          label="name">
        </el-table-column>
      </el-table>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome yizheng to use nwjs',
      msg2: 'nw在dev下居然是热响应的，太厉害了！',
      tableDataMusic: []
    }
  },
  mounted(){
    this.getApiData();
  },
  methods:{
    doSome(){
      alert('you click the button!')
    },
    getApiData(){
      console.log('mounted runed!');
      this.axios.get('https://api.apiopen.top/musicBroadcasting')
      .then((res)=>{
        console.log('开放api可以直接获取，不需要代理转发:',res)
        // console.log('rel:',res,res.data.result[0].channellist.length)
        this.tableDataMusic = res.data.result[0].channellist
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
