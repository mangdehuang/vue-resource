<template>
  <div id="app">
    <table border="1">
      <thead>
        <tr>
          <td>name</td>
          <td>price</td>
          <td>productNumber</td>
          <td>all</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in dataList">
          <td>{{item.name}} </td>
          <td>{{item.price}} </td>
          <td>{{item.productNumber}} </td>
          <td> {{item.productNumber * item.price}} </td>
        </tr>
      </tbody>
      <tfoot>
        {{total}}
      </tfoot>
    </table>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  data(){
      return {
          dataList:[],
      }
  },
  components: {
    Hello
  },
  methods:{
      getData () {
        this.$http.get('./static/data/data.json').then(res => {
          console.log(res);
          this.dataList = res.body.data.list;
        },res => {
            console.log("error");
          }
        );
      }
  },
  computed:{
    total () {
        var totalprice = 0;
      this.dataList.forEach(item => {
        totalprice += item.price * item.productNumber;
      });
      return totalprice;
    }
  },
  mounted () {
     let _this = this;
    this.$nextTick( () => {
      _this.getData();
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
}
  .inlineDiv{
    display: inline-block;
  }
</style>
