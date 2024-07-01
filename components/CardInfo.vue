<template>
    <div class="outer-wrapper">
      <div class="inner-wrapper">
        <n-flex>
          <div class="icon-section">
            <n-icon class="icon">
              <component :is="icon" />
            </n-icon>
          </div>
          <div class="info-section">
            <p style="font-weight: bold; font-size: 20px;">{{ countData }}</p>
            <span>{{ subText }}</span>
          </div>
        </n-flex>
      </div>
      <div class="info">
        <span style="background-color: #5bc6ad; padding: 2px 10px; border-radius: 20px; font-weight: 500;">
          {{ infoText }}
        </span>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { Book } from "@vicons/ionicons5";
  defineProps({
    icon: {
        type: Object,
    },
    countData: {
        type: Number,
    },
    subText: {
        type: String,
    },
    infoText: {
        type: String,
    }
    });
  </script>
  
  <style scoped>

  .info {
    display: flex;
    /* justify-content: center; */
    padding: 10px 10px;
  }

  .outer-wrapper {
    background-color: #dff348;
    padding: 0px 0px 5px;
    border-radius: 20px;
    position: relative;
  }
  
  .inner-wrapper {
    background-color: black;
    padding: 40px 20px;
    border-radius: 20px;
    z-index: 1;
  }
  
  .info-section {
    color: white;
  }
  
  .icon-section {
    background-color: white;
    border-radius: 30px;
    padding: 10px 20px;
    align-items: center;
  }
  
  .icon {
    font-size: 30px;
    align-items: center;
    display: flex;
  }
  </style>
  