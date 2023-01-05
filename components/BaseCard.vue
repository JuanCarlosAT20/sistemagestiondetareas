<template>
  <v-container>
    <v-card class="grey lighten-5" elevation="10" >
      <div class="light-blue darken-2 white--text">
        <p>{{ date }}</p>
        <v-btn :to="'/edittask/' + taskId" class="mr-2" fab dark color="cyan"
          ><v-icon dark> mdi-pencil</v-icon></v-btn
        >
        <!--Acciones de boton delete-->
        <v-btn
          @click="showDialog = deleteTask(taskId)"
          class="mr-2"
          fab
          dark
          color="error"
          ><v-icon dark>mdi-delete</v-icon></v-btn
        >
      </div>
      <v-card-title>{{ title }}</v-card-title>
<!--Boton para mostrar informacion-->
      <div class="text-center">
        <v-btn
          :to="'/tasks/' + taskId"
          rounded color="black" 
          dark 
          class="ma-3"
        >
          Mostrar tarea
        </v-btn>
      </div>

      <v-btn
        class="white--text"
        :style="{ 'background-color': isComplete ? '#616161' : '#039BE5' }"
      >
        <v-icon color="white">mdi-checkbox-marked-circle</v-icon>
        {{ isComplete ? "Tarea completada" : "Tarea en progreso" }}
      </v-btn>
    </v-card>
  </v-container>
</template>
<script>
import axios from "axios";

export default {
  name: "BaseCard",

  props: {
    taskId: {
      type: Number,
      required: false,
    },
    date: {
      type: String,
      required: false,
    },
    title: {
      type: String,
      required: true,
    },
    isComplete: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      snackbar: false,
    };
  },
  methods: {
    async deleteTask(id) {
      const confirmDelete = confirm('Quieres eliminar este registro?');
      const token = "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";

      if(confirmDelete == true){
       const response =  await axios.delete(
        "https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks/" + id,
        {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        }
        
      );
      if (response.status == 200 || 201) {
        this.$emit("reloadAllTasks");
        }
       
      }

    },
  },
};
</script>