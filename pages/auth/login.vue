<template>
    <div class="container">
      <header class="header-login">
        <div class="bar">
          <p class="logo-text">BayarAja!</p>
        </div>
      </header>
      <div class="content">
        <n-card hoverable size="huge">
          <div class="title-wrapper">
            <p class="card-title-1">Welcome Back!</p>
            <span class="card-title-2">Let's login</span>
          </div>
  
          <div class="divider" />
  
          <div class="card-content-wrapper">
            <div class="wrapper-form">
              <n-space vertical>
                <div class="form-input">
                  <div class="username">
                    <label for="username">Username</label>
                    <n-input
                      v-model:value="username"
                      type="text"
                      placeholder="Username"
                      size="large"
                      class="input-form"
                    />
                  </div>
                  <div class="password">
                    <label for="password">Password</label>
                    <n-input
                      v-model:value="password"
                      type="password"
                      show-password-on="mousedown"
                      placeholder="Password"
                      :maxlength="16"
                      size="large"
                      class="input-form"
                    />
                  </div>
                  <n-button class="button-login" @click="handleShowNotification" :theme-overrides="buttonThemeOverrides">
                    <p style="font-weight: 500">Login</p>
                  </n-button>
                </div>
              </n-space>
            </div>
          </div>
  
          <template #footer>
            <div class="footer-wrapper">
              <p>Forgot your account? Contact the admin</p>
            </div>
          </template>
        </n-card>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
import { useNotification, type ButtonProps, type InputProps } from 'naive-ui';

  const username = ref('')
  const password = ref('')
  const notification = useNotification()
  
  const handleShowNotification = () => {
    notification.success({
      title: 'Login success',
      content: 'Welcome to the app!',
      duration: 2000
    })
  }

  type ButtonThemeOverrides = NonNullable<ButtonProps['themeOverrides']>; 

  const buttonThemeOverrides: ButtonThemeOverrides = {
    color: "black",
    colorHover: "black",
    colorFocus: "black",
    border: "#dff348",
    borderHover: "#dff348",
    borderFocus: "#dff348",
    borderPressed: "#dff348",
    textColor: "#dff348",
    textColorFocus: "#dff348",
    textColorHover: "#dff348",
  }
  </script>
  
  <style scoped>
  .divider {
    border: 1px solid rgb(207, 207, 207);
  }
  
  .button-login {
    margin-top: 20px;
    padding: 20px;
  }
  
  .footer-wrapper {
    display: flex;
    justify-content: center;
  }
  
  .wrapper-form {
    margin: 30px 0px;
  }
  
  .form-input {
    display: grid;
    gap: 20px;
  }
  
  .title-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .card-title-1 {
    font-size: 30px;
  }
  
  .container {
    display: flex;
    flex-direction: column;
    height: 100vh;
  }
  
  .header-login {
    display: flex;
    flex-shrink: 0;
  }
  
  .bar {
    background-color: black;
    width: 100%;
    padding: 1rem 5rem;
  }
  
  .logo-text {
    font-size: 25px;
    font-weight: bold;
    color: #dff348;
  }
  
  .content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
    background-color: rgb(243, 243, 243);
  }
  
  .n-card {
    max-width: 450px;
    border: 1px solid rgb(195, 195, 195);
  }
  </style>