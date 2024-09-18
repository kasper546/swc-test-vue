<template>
    <div class="left_panel" :style="{ backgroundImage: `url('${imageUrl}')` }">
        <h2 class="logo_test">Demo Test</h2>
            <ul>
            <li class="left_li" v-for="item in panel_items" :key="item">
                <img :src="item.panel_img" alt="" srcset="">
                <p>{{ item.message }}</p>
            </li>
        </ul>
    </div>
  </template>
  
  <script setup>
  import require from 'vue';
  import imageUrl from '/src/assets/dark.png';

  let panel_items = [
        { message: 'Foo', panel_img: require('/src/assets/user.png') },
        { message: 'Bar', panel_img: require('/src/assets/rim.png') },
        { message: 'Bar', panel_img: require('/src/assets/settings.png') },
      ]

  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .left_panel {
    width: 256px;
  }
  ul {
    padding-left: 0;
  }
  .logo_test {
    color: white;
    text-align: center;
  }
  .left_li {
    display: flex;
    align-items: center;
    opacity: 45%;
    color: white;
    width: 100%;
    padding-left: 20px;
  }
  .left_li img {
    padding-right: 10px;
  }
  .left_li:hover {
    background-color: rgba(255, 255, 255, 20%);
    opacity: 100%;
  }
  </style>
  