<template>
  <n-message-provider>
    <div class="container-wrapper">
      <Navbar />
      <main class="content">
        <RouterView />
      </main>
    </div>
  </n-message-provider>
</template>
  
  <style scoped>
  .container-wrapper {
    display: flex;
  }
  
  .content {
    padding: 20px;
    flex: 1;
    background-color: #edf1f5;
  }
  </style>
  