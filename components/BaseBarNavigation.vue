<template>
    <div>
      <v-navigation-drawer class="black white--text" v-model="drawer" app>
        <the-profile-card />
        <div class="container">
          <h3>
            <v-icon class="blue">mdi-glass-stange</v-icon> Proyectos totales:
            {{ numberOfProyects }}
          </h3>
          <h3>
            <v-icon class="green">mdi-glass-stange</v-icon> Completados:
            {{ numberOfProyectsCompleted }}
          </h3>
          <h3>
            <v-icon class="red">mdi-glass-stange</v-icon>En progreso:
            {{ numberOfProyectsIncompleted }}
          </h3>
        </div>
      </v-navigation-drawer>
      <v-app-bar class="black" app>
        <v-app-bar-nav-icon
          class="white"
          @click="drawer = !drawer"
        ></v-app-bar-nav-icon>
  
        <v-toolbar-title class="white--text">Gestor</v-toolbar-title>
      </v-app-bar>
    </div>
  </template>
      
      <script>
  import TheProfileCard from "../components/TheProfileCard.vue";
  
  export default {
    name: "BaseBarNavigation",
  
    components: {
      TheProfileCard,
    },
  
    props: {
      completedTasks: {
        type: Array,
        required: true,
      },
      incompletedTasks: {
        type: Array,
        required: true,
      },
    },
  
    computed: {
      numberOfProyectsCompleted() {
        return this.completedTasks.length;
      },
      numberOfProyectsIncompleted() {
        return this.incompletedTasks.length;
      },
      numberOfProyects() {
        return this.completedTasks.length + this.incompletedTasks.length;
      },
    },
  
    data() {
      return {
        drawer: null,
      };
    },
  };
  </script>