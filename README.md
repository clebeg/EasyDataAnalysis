# EasyDataAnalysis

## 技术栈
Vue + Vue Router + Vuex + Element-UI

## 部署
### （前提）Step 0：部署 CBoard 后台
请根据 CBoard 的官方文档部署好完整的项目，确保能访问。  
[CBoard github](https://github.com/TuiQiao/CBoard)  
[安装与配置文档](https://peter_zhang921.gitee.io/cboard_docsify/#/zh-cn/manual/install)
后台代码后续也会改成用 spring boot 编写

### Step 1: 编译打包 EasyDataAnalysis
clone 本项目，  
npm install,  

src/utils/http/api.js 中修改：  
const baseurl = '你的 CBoard 项目访问地址';

npm run build  

生成文件index.html 和目录static

### Step 2: 
将目录 static 加入cboard根目录下，  
将 index.html 改名为 starter.html 替换cboard根目录下原来的文件。

### 开发调试（chrome）
1、config/index.js 中修改： 

```
module.exports = {
  dev: {
    proxyTable: {
      '/api': {
          // 修改为实际访问CBoard后台的地址
          target: 'http://localhost:8080/cboard_war_exploded/',
          // secure: false, // https需要设置
          changeOrigin: true,  // 设置跨域
          pathRewrite: {
            '^/api': '/'
          },
          headers: {
            'Host': 'localhost',
            // 修改为实际访问已搭好的 CBoard 项目登录，获得 cookie JSESSIONID 值，设置到下面
            'Cookie': 'JSESSIONID='
          }
      }
    },

```

2、npm install && npm run dev 
开始调试
