# vue3-aj-captcha

## 说明
该项目为码云GVP项目 AJ-Captcha[https://gitee.com/anji-plus/captcha] 前端部分。该项目暂未提供vue3版本的组件，本人只好自己改。

### 使用
将component下的verifition文件夹拷贝至项目中,在项目引入组件即可。参考可看App.vue,详情参数去查看原项目[https://gitee.com/anji-plus/captcha]

### 本地运行

```
yarn install
yarn serve

//项目中使用请添加 axios、crypto-js
```



### Verify.vue

- `@success:`  `Verify` 子组件`VerifySlide`或者`VerifyPoints` 验证码验证成功的回调函数
- `@error`: 子组件验证失败的回调函数,同`@success`

#### 回调事件

| 参数            | 类型     | 说明                                                         |
| :-------------- | :------- | :----------------------------------------------------------- |
| success(params) | funciton | 验证码匹配成功后的回调函数,params为返回需回传服务器的二次验证参数 |
| error           | funciton | 验证码匹配失败后的回调函数                                   |
| ready           | funciton | 验证码初始化成功的回调函数                                   |

#### 验证码参数

| 参数        | 类型   | 说明                                                         |
| :---------- | :----- | :----------------------------------------------------------- |
| captchaType | String | 1）滑动拼图 `blockPuzzle` <br />2）文字点选 `clickWord`      |
| mode        | String | 验证码的显示方式，弹出式pop，固定fixed，默认：mode : ‘pop’   |
| vSpace      | String | 验证码图片和移动条容器的间隔，默认单位是px。如：间隔为5px，默认:vSpace:5 |
| explain     | String | 滑动条内的提示，不设置默认是：'向右滑动完成验证'             |
| imgSize     | Object | 其中包含了width、height两个参数，分别代表图片的宽度和高度，支持百分比方式设置 如:{width:'400px',height:'200px'} |



#### API接口

 [location](./src/components/verifition/api/index.js)

- [axios.js](.src/components/verifition/utils/axios.js): 需要配置你的验证码接口
- 你需要更改成你自己的code api接口







## example:

### fun-ui-v3: 

#### App.vue:

- 任何一个vue页面即可,你想要用于`verify`组件即可

```vue
<templeate>
<Verify
      @error="verifyError"
      @sucess="verifySuccess"
      mode="pop"
      :captchaType="captchaType"
      :imgSize="{width:'400px',height:'200px'}"
      ref="verify"
    ></Verify>
  <button @click="onShow('blockPuzzle')">滑块</button>
    
</templeate>
<script>
import { ref }  from 'vue'
import Verify from '@/components/verifition/Verify'
   // 
    const  verify = ref(null); 
    // 两个回调函数
    const verifySuccess= (params)=>{
       
   }
   const verifyError= () => {
       
   }
   
   const onShow = (param) => {
       verify.value.show()
   } 
    // 
</script>


```

## Hint: 

- 可以通过检索`todo`关键字对必要的配置进行修改.适用于vue3 

| config    | 客制化配置处                          |
| --------- | ------------------------------------- |
| **note**  | 回调函数的说明                        |
| **todo**  | 将要做的事                            |
| fixme     | 标记问题                              |
| hack      | 标记一些不是常规的解决方案            |
| customize | 用于第三方配置,以及接口函数扩展的标记 |

