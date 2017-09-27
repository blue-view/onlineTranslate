<template>
  <div id="app">
    <h1>在线翻译</h1>
    <h5 class="text-muted">简单/易用/便捷</h5>
    <TransLateForm @formSubmit="transLateText"></TransLateForm>
    <TransLateOutPut :translatedText="transLateTextValue"></TransLateOutPut>
  </div>
</template>

<script>
import TransLateForm from './components/TransLateForm'
import TransLateOutPut from './components/TransLateOutPut'
import md5 from 'js-md5'

export default {
  name: 'app',
  components: {
    TransLateForm,
    TransLateOutPut
  },
  data(){
    return {
      transLateTextValue:''
    }
  },
  methods: {
    transLateText: function(text,lanuage) {
      var sign = md5('20170927000085557' + text + '1435660288' + 'tp8GYV2hdgnBfYOF925t');
      var url = `http://api.fanyi.baidu.com/api/trans/vip/translate?q=${text}&from=zn&to=${lanuage}&appid=20170927000085557&salt=1435660288&sign=${sign}`;
      // console.log(url);
      // this.$http.get(url).then((res) => {
      //   console.log(res.trans_result);
      // }).catch(e => {
      //   // 打印一下错误
      //   console.log(e)
      // });
      this.$http.jsonp(url, {},
        {
          headers: {},
          emulateJSON: true
        }).then((response) => {
          // console.log(response.data.trans_result[0].dst);
          this.transLateTextValue=response.data.trans_result[0].dst;
        });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
