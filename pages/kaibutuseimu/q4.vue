<template>
  <div>
    <h1 style="text-align: center" class="kbsmh1">謎4</h1>
    <img src="question4.gif" width="80%" style="display: block; margin: auto" />
    <div style="text-align: center; margin-top: 1em">
      <form @submit.prevent>
        <input v-model="answer" type="text" class="inputfield" name="answer" />
        <div class="button">
          <button @click="submit">解答する</button>
        </div>
      </form>
      <p v-if="answerResult">不正解</p>
      <div class="button">
        <a href="questionindex">謎の選択に戻る</a>
      </div>
    </div>
  </div>
</template>
<style>
.button button {
  position: relative;
  display: inline-block;
  padding: 0.25em 2em;
  text-decoration: none;
  color: #fff;
  background: #d1ae6b; /*背景色*/
  border-bottom: solid 2px #8f6e31; /*少し濃い目の色に*/
  border-radius: 4px; /*角の丸み*/
  box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.2),
    0 2px 2px rgba(0, 0, 0, 0.19);
  font-weight: bold;
}
.button button:active {
  border-bottom: solid 2px #cfb177;
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.3);
}
.inputfield{
  background-color: -internal-light-dark(rgb(255, 255, 255), rgb(59, 59, 59));
  background-color: white;
  margin: 0em;
  padding: 1px 2px;
  border-style: inset;
}
</style>

<script>

export default {
	layout:'kaibutuseimu',
	data() {
		return{
      answer: "",
      answerResult: false,
		}
	},
  methods:{
    submit(){
      if(this.answer==="佐野鼎"){
        const str1 = String(this.$cookies.get('kaibutuseimu'));
        this.$cookies.set('kaibutuseimu',  str1.replace(/(?<=^.{3})./, "1") , {maxAge: 60 * 60 * 24 * 7},)
        this.$router.push({ path: 'good4' });
      }
      else if(this.answer !== ""){
        this.answerResult=true
      }
    }
  }
}
</script>