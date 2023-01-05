<template>
    <div>
      <v-card-actions class="px- pb-3">
        <v-flex text-xs-left>
          <nuxt-link to="/tasks/NewTask"
            ><v-btn class="mx-2" :elevation="10" fab-dart color="teal accent-4"
              >Agregar Tarea</v-btn
            ></nuxt-link
          >
        </v-flex>
      </v-card-actions>
    </div>
  </template>
  
  <script>
  export default {
    name: "BaseButtonAddUser",
  };
  </script>
  
  <style>
  a {
    text-decoration: none;
  }
  </style>