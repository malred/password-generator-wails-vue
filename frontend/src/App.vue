<template>
  <div class="container">
    <input
      type="text"
      v-model="inp"
      placeholder="Input your password to encrypt"
    />
    <br />
    <select name="alg" id="alg" v-model="sel">
      <option :value="v" v-for="v in crypto" :key="v">{{ v }}</option>
    </select>
    <br />
    <button @click="Gen">Generator!</button>
    <br />
    <div>{{ genStr }}</div>
  </div>
</template>
<script setup>
import crypto from './crypto'
import { ref } from 'vue'
import { MD5, Sha1, HMAC_SHA256 } from '../wailsjs/go/main/App'
const sel = ref('bcrypt')
const inp = ref('')

// 加密后的字符串
let genStr = ref('')

const Gen = () => {
  if (!inp.value) {
    return
  }
  // console.log(sel.value)
  if (sel.value === 'md5') {
    MD5(inp.value).then(res => {
      genStr.value = res
    })
  } else if (sel.value === 'sha1') {
    Sha1(inp.value).then(res => {
      genStr.value = res
    })
  } else if (sel.value === 'HMAC-SHA256') {
    HMAC_SHA256(inp.value).then(res => {
      genStr.value = res
    })
  }

  inp.value = ''
}
</script>
<style scoped>
.container {
  text-align: center;
  margin-top: 16rem;
}
select {
  margin-top: 2rem;
  border: none;
  outline: none;
  width: 16rem;
  height: 3rem;
  background-color: #faf1d8;

  font-size: 1.2rem;
  line-height: 1.2rem;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  /* padding-right: 2px; */
  text-align: center;
  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

  border-radius: 0.5rem;
}

button {
  background-color: #f2c64f; /* Green */
  border: none;
  color: black;
  border-radius: 0.5rem;
  padding: 3rem 4rem;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 1.2rem;
  margin: 4px 2px;
  cursor: pointer;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
}
button:hover {
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
}
div {
  color: black;
  font-weight: bold;
  margin-top: 2rem;
}
button {
  margin-top: 2rem;
  position: relative;
  background-color: #4caf50;
  border: none;
  font-size: 12rempx;
  color: #ffffff;
  padding: 1rem;
  width: 200px;
  text-align: center;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
}
button:after {
  content: '';
  background: #90ee90;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s;
}
button:active:after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s;
}

input {
  outline: none;
  /* background-color: #4368d092; */
  /* padding: 1rem .5rem;  */
  border: 1px solid #fff;
  border-radius: 0.5rem;

  background-color: #faf1d8;
  text-indent: 1rem;

  width: 16rem;
  height: 3rem;
  font-size: 1rem;
  font-weight: bold;

  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
}
input:placeholder-shown {
  /* border: 3px solid rgba(224, 224, 56, 0.762); */
}
input::-webkit-input-placeholder {
  /* color: #2feb2f; */
  font-size: 1rem;
  font-weight: normal;
}
</style>
