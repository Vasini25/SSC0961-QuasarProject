<template>
    <q-layout>
        <q-header elevated class="shadows">
            <div class="q-pa-md">
              <img width="200" align="right" src="../assets/f1logo-nbg.png"/>
              <h1 class="header-title">Fórmula 1</h1>
            </div>
        </q-header>
        <q-page-container class="q-page-container">
          <router-view />
        </q-page-container>
    </q-layout>

</template>
  
  <script>

  export default {
  };
  </script>
  
  <style>
  .q-pa-md {
    padding: 12px;
    padding-left: 100px;
    padding-right: 100px;
  }
  
  .header-title {
    font-size: 64px;
    font-family: banco-bold;
    color: red;
  }

  .q-page-container {
    padding-top: 64px;
  }

  .shadows {
    box-shadow: 1px 10px 1px #000000;
  }
  </style>