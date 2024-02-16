<template>
  <button @click="onShow('blockPuzzle')">滑块</button>
  <button @click="onShow('clickWord')">点击文字</button>
  <!-- note @error, @success 为子组件的回调函数 -->
  <Verify
    @error="verifyError"
    @sucess="verifySuccess"
    mode="pop"
    :captchaType="captchaType"
    :imgSize="{ width: '400px', height: '200px' }"
    ref="verify"
  ></Verify>
</template>

<script>
import { ref, getCurrentInstance } from "vue";
import Verify from "@/components/verifition/Verify";
export default {
  name: "App",
  components: {
    Verify,
  },
  setup(props, context) {
    const verify = ref(null);
    const captchaType = ref("");
    const onShow = (type) => {
      captchaType.value = type;
      // note : verify show method  
      verify.value.show();
    };
    /**
     *  note 
     *  验证码校验成功的返回函数
     */
    const verifySuccess = (data: string) => {
      console.log("<-- 验证码校验成功--> ");
      console.log(data);
      // console.log(data)
      // todo  login
      // loginFormData.code = data.captchaVerification
      // console.log(loginFormData)
      handleLogin(data);
    };

    /**
     * note 
     * 验证码校验失败  的 callback
     */
    const verifyError = () => {
      console.log("验证码校验失败, 内容如下-----");
      // console.log(data.tipWords)
      ElMessage.error("验证码失效或校验失败, 请重试");
    };
    return {
      verify,
      onShow,
      captchaType,
    };
  },
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
