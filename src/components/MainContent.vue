<template>
    <div class="main">
    <header>
        <div class="header_left">
            <h1>Vechicles</h1>
            <p class="count">256</p>
        </div>
        <div class="header_right">
            <div class="plus_button">+</div>
            <div class="account">
                <img :src="photo" alt="" class="account_img">
                <p class="account_text">John Doe</p>
            </div>
            <div class="language">
                <img :src="uk" alt="" class="uk_img">
                <p class="language_p">En</p>
                <img :src="arrow" alt="" class="arrow_img">
            </div>
        </div>
    </header>
    <div class="under_header">
        <div class="search_block">
            <input v-model="vin" @keyup.enter="fetchData" class="search_input" type="text">
            <img class="search_img" :src="zoom" alt="" srcset="" @click="fetchData">
        </div>
        <div class="select_number">
            <p class="select_p">Select vehicles per page:</p>
            <select @change="fetchData" class="number_select" v-model="itemCount">
                <option v-for="itemCount in count" :key="itemCount" >
                    {{ itemCount }}
                  </option>
            </select>
        </div>
        <div class="red_button">
            <p class="red_button_plus">+</p>
            <p class="red_button_text">ADD VECHICLE</p>
        </div>
    </div>
    <ul class="ul_items">
        <li v-for="item in cars.slice(0, itemCount)" :key="item.id">
        <div class="img_block">
        <img class="car_img" v-if="item.photo && item.photo.processed_url" :src="item.photo.processed_url" alt="фото автомобиля" />
    </div>
    <div class="text_block">
        <p class="car_name">{{ item.vehicle_name }}</p>
          <p class="car_WDB">WDB 1400321A333419</p>
          <div class="line"></div>
          <div class="count_and_days">
            <p class="count_p" :class="{ 'green_p': item.angles_count === 30 }">{{ item.angles_count }}/30</p>
            <p class="days_p">3 days left</p>
          </div>
        </div>
        </li>
      </ul>
    <footer>
        <div class="footer_left">
            <div class="footer_left_P">Showing {{ itemCount }} out of 256 </div>
        </div>
    
        <div class="footer_right">
            <img @click="prevPage()" :src="left" alt="" srcset="">
            <p class="footer_right_number_p">{{page}}</p>
            <p class="footer_right_p">of</p>
            <p class="footer_right_number_p">28</p>
            <img @click="nextPage()" :src="right" alt="" srcset="">
        </div>
    </footer>
</div>
  </template>
  
  <script setup>

import { ref, onMounted } from 'vue';
  import photo from '/src/assets/Photo.png';
  import uk from '/src/assets/uk.png';
  import arrow from '/src/assets/chevron_down.png';
  import zoom from '/src/assets/zoom.png';
  import left from '/src/assets/chevron_left.png';
  import right from '/src/assets/chevron_right.png';

const count = ref(20);
  const page = ref(1);
  const cars = ref([]);
  const itemCount = ref(20);
  const vin = ref('');

const fetchData = async () => {
  try {
    const response = await fetch(`https://api.caiman-app.de/api/cars-test?search=${vin.value}&per_page=${itemCount.value}&page=${page.value}`); 
    if (!response.ok) {
      throw new Error('ошибка');
    }

    const jsonData = await response.json(); 
    cars.value = jsonData.data; 
    console.log(cars.value); 
  } catch (error) {
    console.error(error);
  }
};
const nextPage = () => {
if (page.value < 28) {
  page.value++;
  fetchData(); 
    }
};

const prevPage = () => {
  if (page.value > 1) {
    page.value--;
    fetchData(); 
  }
};

onMounted(fetchData);
  </script>
  
  <style scoped>
  .main {
    width: 100%;
  }
  header {
    display: flex;
    justify-content: space-between;
    width: 100%;
    height: 100px;
    border-bottom: 1px solid #E4E4E4;
  }
  
  .header_right {
    display: flex;
    align-items: center;
  }
  .account {
    display: flex;
  }
  h1 {
    margin-left: 30px;
    margin-right: 30px;
  }
  
  .count {
    padding: 10px;
    background-color: #F3F6F8;
    border-radius: 15px;
  }
  .language {
    display: flex;
    align-items: center;
  }
  .language_p {
    margin-left: 10px;
    margin-right: 10px;
  }
  .plus_button {
    color: #E86E84;
    padding: 15px;
    border: 1px solid #E86E84; 
    border-radius: 15px;
  }
  .account_img {
    margin-left: 42px;
    margin-right: 14px;
  }
  .account_text {
    margin-right: 39px;
  }
  .arrow_img {
    padding-right: 50px;
  }
  .header_left {
    display: flex;
    align-items: center;
  }
  .count_p {
    background-color: #EDEDED;
    border-radius: 15px;
    padding: 10px;
  }
  .green_p {
    color: #7FC75E;
    background-color: #E4F5DD;
  }


  .under_header {
    justify-content: space-around;
    margin-top: 38px;
  }
  .select_number {
    display: flex;
    align-items: center;
  }
  .select_p {
    margin-right: 20px;
  }
  .search_img {
    margin-left: -40px
  }
  .select_p {
    margin-left: 50px;
  }
  .number_select {
    width: 85px;
    height: 42px;
    border-radius: 15px;
  }
  .search_block {
    display: flex;
    align-items: center;
  }
  .search_input {
    height: 42px;
    width: 354px;
    border-radius: 15px;
  }
  .under_header {
    display: flex;
    align-items: center;
  }
  .red_button {
    background-color: #D90E32;
    width: 180px;
    display: flex;
    justify-content: space-around;
    color: white;
    font-size: 12px;
    height: 42px;
    border-radius: 15px;
  }
  .car_img {
    width: 260px;
    height: 135px;
    justify-content: center;
  }
  .car_name {
    color: #293148;
    font-size: 20px;
    font-weight: bold;
  }
  .img_block {
    height: 175px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .car_WDB {
    color: #293148;
    opacity: 45%;
  }
  .ul_items {
    display: grid;
    grid-template-columns: 30% 30% 30%;
    gap: 20px;
    margin-left: 25px;
  }
  .days_p {
    opacity: 60%;
  }
  .count_and_days {
    color: #293148;
    display: flex;
    justify-content: space-between;
  }
  .text_block {
    margin-left: 24px;
    margin-right: 24px;
  }
  .line {
    width: 100%;
    background-color: #E4E4E4;
    height: 1px;
  }


  footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-left: 50px;
    margin-right: 50px;
  }
  .left_panel {
    width: 256px;
  }

  ul {
    color: white;
  }
  li {
    background-color: #F3F6F8;
    width: 354px;
    height: 335px;
    border-radius: 15px;
  }
  .footer_right {
    display: flex;
    align-items: center;
  }
  .footer_right_p {
    margin-left: 15px;
    margin-right: 15px;
  }
  .footer_right_number_p {
    padding: 10px;
    border: 1px solid#E4E4E4;
    border-radius: 10px;
  }
  </style>
  