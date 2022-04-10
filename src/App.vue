<template>
  <button @click="test()">hey</button>
  <small>{{seriesList[0]}}</small>
  <div class="row">
    <template v-for="(pokemon,index) in seriesList[0].total + 1" :key="index">
      <div  class="column" v-if="index!== 0" > 
        
        
        <div class="card" >
          {{index}}
          <img v-bind:src="linkSrc + seriesList[0].id + '/' + index  +'_hires.png'">
          <!-- <small v-bind:class = "index % 18?'':'end'">No.{{index}}</small>
          <br>
          <span style="margin-bottom: 50px">{{nameList[index]}}</span> -->
        </div>
      </div>
      
    </template>
  </div>
  <!-- <small>{{seriesList}}</small> -->
</template>

<script>

  import { seriesList } from  './const/seriesList.js'
export default {
  name: 'App',
  data(){
    return{
      dataList: [],
      totalNum: 0,
      tempText: undefined,
      baseData: [],
      seriesList,
      linkSrc: 'https://images.pokemontcg.io/',
    }
  },
  methods:{
    async test(){
      const URL = 'https://api.pokemontcg.io/v2/sets'
      const res = await fetch(URL)
      const json = await res.json()
      console.log(json.data)


      this.dataList = json.data

      this.count()
      console.log(`totalnum: ${this.totalNum}`)
      
    },

    count(){
      let count = 0
      for (let item in this.dataList){
        
        // console.log(this.dataList[item].name)
        let temp = this.dataList[item]
        this.baseData.push({id: temp.id , total: temp.printedtotal, series: temp.series, name: temp.name})
        console.log(`No:${count}, total: ${temp.printedtotal}, Series: '${temp.series}', Name: '${temp.name}',id: '${temp.id}' `)
        this.tempText+=`No:${count}, total: ${temp.printedtotal}, Series: '${temp.series}', Name: '${temp.name}',id: '${temp.id}' `
        this.totalNum+=temp.printedtotal
        count++
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-right: auto;
  margin-left: auto;
  color: #2c3e50;
  margin-top: 60px;
  width: 375px;
  margin:0;
padding:0;
overflow-x:hidden;
}
* {
  box-sizing: border-box;
}
body {
  font-family: Arial, Helvetica, sans-serif;
}
/* Float four columns side by side */
.column {
  float: left;
  width: 33%;
  padding: 0 10px;
}
/* Remove extra left and right margins, due to padding in columns */
.row {margin: 0 -5px;}
/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
/* Style the counter cards */
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2); /* this adds the "card" effect */
  padding: 0px;
  text-align: center;
  background-color: #f1f1f1;
  margin-bottom: 15px;
  height: auto;
  font-size: 80%;
}
img{
  display:block;
  width:70%;
  height: auto;
  margin-top: 10px;
  margin-left:auto;
  margin-right:auto;
}
.caught{
  opacity: 0.35;
}
.end{
  color:red;
}
/* Responsive columns - one column layout (vertical) on small screens */
/* @media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
} */
</style>