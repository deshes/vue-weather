# vue-weather

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

Vue简洁的语法和组件化开发方式极大的提高了前端开发的工作效率

花了一些空余时间做了一个vue-weather的demo与大家分享  

demo基于element前端框架  由ele的前端团队开发 风格也比较简约大方 也是基于vue的组件式开发的

直接调用ele框架自带的组建就可以极其方便的构建页面的布局

下边 就是页面代码
```  
     <template>
     <div class="hello">
     <h1>{{ msg }}</h1>
     <el-col :span="24" class="toolbar">
     <el-form :inline="true">
     <el-form-item>
          <el-input placeholder="请输入城市名称" v-model="input2" @keyup.enter="greet"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button @click="greet" >查询</el-button>
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
          prop="date"
          label="日期">
        </el-table-column>
        <el-table-column
          align="center"
          prop="cond.txt_d"
          label="天气">
        </el-table-column>
        <el-table-column
          align="center"
          prop="tmp.max"
          label="日间温度">
        </el-table-column>
        <el-table-column
          align="center"
          prop="tmp.min"
          label="夜间温度">
        </el-table-column>
        <el-table-column
          align="center"
          prop="pres"
          label="气压值">
        </el-table-column>
        <!--<el-table-column
          align="center"
          prop="weather.icon"
          label="天气情况">
          <template scope="scope">
              <img :src="scope.row.weather.icon" />
          </template>
        </el-table-column>-->
      </el-table>
    </el-col>
    </div>
    </template>
```
element-ui table中的data属性只要绑定数据源就可以通过props自动循环

当然在使用element-ui前 我们需要在npm中 安装element-ui至本地 cnpm i element-ui --save

同时在main.js全局引入element-ui中的css文件

    import Vue from 'vue'
    import ElementUI from 'element-ui'
    import 'element-ui/lib/theme-default/index.css'
    import App from './App'
    import Vueresource from 'vue-resource'
    Vue.use(ElementUI)
    Vue.use(Vueresource)
    /* eslint-disable no-new */
    new Vue({
    el: '#app',
    template: '<App/>',
    components: { App }
    })

搭建好页面结构后  我们通过vue-resource引入数据源 ,这里的数据源来自和风天气  和风天气免费版提供三天国内城市的天气api  

        this.$http.get(`https://free-api.heweather.com/x3/weather?city=${this.input2}&key=2723a31a831b4d82aba437c1de05ac95`)
							.then((response) => {
              this.gridData=response.data['HeWeather data service 3.0'][0].daily_forecast;

通过上面三行代码就能获取数据源到本地,Vue-resource简化了ajax的语法同时也支持jsonp 搭配vue使用很不错

最后把数据通过data() return 给页面 整个页面就完成了  十分简单 

这里能感受到element-ui上手十分简单,国内一线大厂的前端团队果然牛逼 哈哈

