<script setup>
</script>
<template>
    <header>
        <nav class="container">
            <div class="branding">
                <img src="../assets/bird_logo.png" alt="bird logo of todo app" />
                <h1>To-Do List Web App</h1>
            </div>
        </nav>
    </header>
</template>

<style lang="scss" scoped>
* {
    font-family: "Rubik", sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .container {
    max-width: 1100px;
    margin: 0 auto;
    margin-bottom: 20px;
    
    .branding {
      display: flex;
      align-items: center;
    }
    img {
      width: 100px;
    }
  }
header {
    background-color: #f1f1f1;
    nav {
      display: flex;
      align-items: center;
      padding: 25px 16px;
  
      .branding {
        display: flex;
        align-items: center;
        gap: 8px;
        img {
          max-width: 50px;
        }
  
        h1 {
          font-size: 24px;
        }
      }
    }
  }
</style>
