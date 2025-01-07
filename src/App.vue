<script setup lang="ts">
import { reactive, ref } from 'vue'

import data from '@/data/data.json'
const search = ref('')
type Province = {
  id: number
  china_name: string
  phien_am: string
  viet_name: string
}
const dataP: Province[] = data

const results = reactive<Province[]>([])

const fetchResults = (query: string) => {
  // Use results.value to update the reactive array
  results.splice(
    0,
    results.length,
    ...dataP.filter((item) => item.viet_name.toLowerCase().includes(query.toLowerCase())),
  )
}
const handleInput = () => {
  fetchResults(search.value)
}

const copyText = (event: any) => {
    const text = event.target.previousElementSibling.innerText; // Get the text of the previous span element
    const textArea = document.createElement('textarea');
    textArea.value = text;
    document.body.appendChild(textArea);
    textArea.select(); // Select the text
    document.execCommand('copy'); // Copy the text
    document.body.removeChild(textArea); // Remove the textarea after copying
    alert('Đã copy hihi: ' + text); // Optional: alert user
  };
</script>

<template>
  <div>
    <div class="border2">
      <h1>Tìm kiếm tỉnh thành, quận huyện trong tiếng Trung</h1>
      <input
        id="search"
        type="text"
        @input="handleInput"
        placeholder="Nhập từ khóa tìm kiếm ..."
        v-model="search"
      />
    </div>
    <ol class="gradient-list">
      <li v-for="(item, index) in results" :key="index">{{ item.viet_name }} - <span class="china_text">{{ item.china_name }}</span> <button @click="copyText">Copy</button> </li>
    </ol>
  </div>
</template>

<style lang="css">
.border2 {
  padding: 20px;
  border-radius: 5px;
  max-width: 600px;
  margin: 0 auto;
}

#search {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 20px;
  font-size: 16px;
}

.gradient-list {
  list-style: none;
  padding: 0;
  margin: 0;
  width: 100%;
}

.gradient-list li {
  padding: 10px;
  margin-bottom: 10px;
  background: linear-gradient(90deg, rgba(255, 255, 255, 1) 0%, rgba(240, 240, 240, 1) 100%);
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}
.china_text {
  color: red;
  font-weight: bold;
}
/* * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  background: linear-gradient(to right, #22c1c3, #fdbb2d);
  font-family: 'Raleway', sans-serif;
  color: rgb(73, 73, 73);
}

.container {
  position: absolute;
  top: 25%;
  left: 50%;
  transform: translateX(-50%);
}

input#search {
  color: inherit;
  padding: 12px 10px;
  width: 60vw;
  border-top-right-radius: 5px;
  border-top-left-radius: 5px;
  border: none;
  outline: none;
}

ul {
  background: #fff;
  border-bottom-right-radius: 5px;
  border-bottom-left-radius: 5px;
  height: 0;
  overflow: hidden;
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.2);
  transition: 0.4s height;
}

ul li {
  font-size: 13px;
  padding: 10px 10px;
  list-style: none;
  border-top: 1px solid #ddd;
}

.match {
  font-weight: 600;
  color: green;
}

@media only screen and (min-width: 600px) {
  input#search {
    width: 40vw;
  }
}
.border input {
  border-radius: 20px !important;
  background-color: #fff;
  padding-left: 20px;
}
*:focus {
  outline: none;
}
input:focus {
  outline: none;
} */

/*** FONTS ***/
@import url(https://fonts.googleapis.com/css?family=Montserrat:900|Raleway:400,400i,700,700i);
/*** VARIABLES ***/
/* Colors */
/*** EXTEND ***/
/* box-shadow */
ol.gradient-list > li::before,
ol.gradient-list > li {
  box-shadow:
    0.25rem 0.25rem 0.6rem rgba(0, 0, 0, 0.05),
    0 0.5rem 1.125rem rgba(75, 0, 0, 0.05);
}

ol.gradient-list {
  counter-reset: gradient-counter;
  list-style: none;
  margin: 1.75rem 0;
  padding-left: 1rem;
  width: 100%;
}
ol.gradient-list > li {
  background: white;
  border-radius: 0 0.5rem 0.5rem 0.5rem;
  counter-increment: gradient-counter;
  margin-top: 1rem;
  min-height: 3rem;
  padding: 1rem 1rem 1rem 3rem;
  position: relative;
}
ol.gradient-list > li::before,
ol.gradient-list > li::after {
  background: linear-gradient(135deg, #83e4e2 0%, #a2ed56 100%);
  border-radius: 1rem 1rem 0 1rem;
  content: '';
  height: 3rem;
  left: -1rem;
  overflow: hidden;
  position: absolute;
  top: -1rem;
  width: 3rem;
}
ol.gradient-list > li::before {
  align-items: flex-end;
  content: counter(gradient-counter);
  color: #1d1f20;
  display: flex;
  font: 900 1.5em/1 'Montserrat';
  justify-content: flex-end;
  padding: 0.125em 0.25em;
  z-index: 1;
}
ol.gradient-list > li:nth-child(10n + 1):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.2) 0%, rgba(253, 220, 50, 0.2) 100%);
}
ol.gradient-list > li:nth-child(10n + 2):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.4) 0%, rgba(253, 220, 50, 0.4) 100%);
}
ol.gradient-list > li:nth-child(10n + 3):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.6) 0%, rgba(253, 220, 50, 0.6) 100%);
}
ol.gradient-list > li:nth-child(10n + 4):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.8) 0%, rgba(253, 220, 50, 0.8) 100%);
}
ol.gradient-list > li:nth-child(10n + 5):before {
  background: linear-gradient(135deg, #a2ed56 0%, #fddc32 100%);
}
ol.gradient-list > li:nth-child(10n + 6):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.8) 0%, rgba(253, 220, 50, 0.8) 100%);
}
ol.gradient-list > li:nth-child(10n + 7):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.6) 0%, rgba(253, 220, 50, 0.6) 100%);
}
ol.gradient-list > li:nth-child(10n + 8):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.4) 0%, rgba(253, 220, 50, 0.4) 100%);
}
ol.gradient-list > li:nth-child(10n + 9):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0.2) 0%, rgba(253, 220, 50, 0.2) 100%);
}
ol.gradient-list > li:nth-child(10n + 10):before {
  background: linear-gradient(135deg, rgba(162, 237, 86, 0) 0%, rgba(253, 220, 50, 0) 100%);
}
ol.gradient-list > li + li {
  margin-top: 2rem;
}
button {
  background-color: #008CBA;
  border: none;
  color: white;
  padding: 10px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>
