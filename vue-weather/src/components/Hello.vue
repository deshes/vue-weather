<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-col :span="24" class="toolbar">
      <el-form :inline="true">
        <el-form-item>
          <el-input placeholder="请输入城市名称" v-model="input2"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button v-on:click="greet">查询</el-button>
        </el-form-item>
      </el-form>
    </el-col>
    <el-col :span="24" v-if="show">
      <el-button type="primary">{{city}}</el-button>
            <el-button type="primary">{{country}}</el-button>

    </el-col>
    <el-col :span="24" v-if="show">
      <el-table
        :data="gridData"
        stripe
        fit
        style="width: 80% ;text-align: center;">
        <el-table-column
          align="center"
          prop="dt"
          label="日期">
        </el-table-column>
        <el-table-column
          align="center"
          prop="weather.main"
          label="天气">
        </el-table-column>
        <el-table-column
          align="center"
          prop="temp.day"
          label="日间温度">
        </el-table-column>
        <el-table-column
          align="center"
          prop="temp.night"
          label="夜间温度">
        </el-table-column>
        <el-table-column
          align="center"
          prop="pressure"
          label="气压值">
        </el-table-column>
        <el-table-column
          align="center"
          prop="weather.icon"
          label="天气情况">
          <template scope="scope">
              <img :src="scope.row.weather.icon" />
          </template>
        </el-table-column>
      </el-table>
    </el-col>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'A Simple VUE Weather Demo',
      input2:null,
      show:false,
      gridData:[],
      city:null,
      country:null
    }
  },
  methods: {
      greet: function() {
						this.$http.get(`http://api.openweathermap.org/data/2.5/forecast/daily?q=${this.input2}&mode=json&units=metric&cnt=7&appid=f12159c1f548ea9ab7b5ff1907b1df50`)
							.then((response) => {
                this.city=response.data.city.name;
                this.country=response.data.city.country;
               this.gridData=response.data.list
               console.log(this.gridData);
               for(let i=0;i<this.gridData.length;i++){
                //  this.gridData[i].img= '<img src="http://openweathermap.org/img/w/'+this.gridData[i].weather[0].icon+'.png">'
                 this.gridData[i].weather.main=this.gridData[i].weather[0].main  
                 this.gridData[i].weather.icon= 'http://openweathermap.org/img/w/' + this.gridData[i].weather[0].icon + '.png';                  
                 var date = new Date(this.gridData[i].dt*1000);
                 this.gridData[i].dt = `${date.getFullYear()}-${date.getMonth() +1}-${date.getDate()}`
               } 
               
               this.show = true             
							})
							.catch(function(response) {
								console.log(response)
							})
					}
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bounce-enter-active {
  animation:bounce-in .5s;
}
.bounce-leave-active{
  animation:bounce-out .5s;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes bounce-out {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(0);
  }
}
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
.el-table{
  margin:5% 10%;
}
.el-row {
    margin-bottom: 20px;
    
  }
  .el-row:last-child {
      margin-bottom: 0;
    }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>
