<template>
  <v-app>
<v-container>
  <v-card class="grey lighten-5" elevation="10" v-for="task in infoTask" :key="task.id">
    <div class="light-blue darken-2 white--text">
      <p>{{task.due_date}}</p>
    </div>
    <v-card-title>{{task.title}}</v-card-title>
    <v-card-subtitle>{{task.description}}</v-card-subtitle>
    <v-btn
          class="white--text"
          :style="{ 'background-color': task.is_completed ? '#616161' : '#039BE5' }"
        >
          <v-icon color="white">mdi-checkbox-marked-circle</v-icon>
          {{ task.is_completed ? 'Tarea Completa' : 'Tarea Incompleta'}}
        </v-btn>
        <v-card-text>
          <div class="text--primary">
            <h3>Comentarios</h3>
              <v-icon>mdi-message-reply</v-icon> {{ task.comments }}
          </div>
        </v-card-text>
        <v-card-text>
          <div class="text--primary">
            <h3>Etiquetas</h3>
          </div>
        </v-card-text>
        <v-card-text>
          <v-chip-group
            active-class="deep-purple accent-4 white--text"
          >
            <v-chip>{{ task.tags }}</v-chip>
          </v-chip-group>
        </v-card-text>
        <v-btn dark to="/tasks" color="blue-grey">Salir</v-btn>
  </v-card>
</v-container>
</v-app>
</template>

<script>
import axios from 'axios'
export default {

  data() {
    return {
      infoTask:{}
    };
  },

  created(){
    this.getInfoTasks()
  },

  methods: {
    async getInfoTasks(){
      const token = "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";
    
      const response = await axios.get(
        `https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks/${this.$route.params.id}`,
        {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        }
      );
      this.infoTask = response.data;
      console.log(response.data)
    }
  },

};
</script>
