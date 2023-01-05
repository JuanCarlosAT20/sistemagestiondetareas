<template>
    <v-app>
      <v-form ref="form" v-model="valid" lazy-validation v-for="task in dataTasks" :key="task.id">
        <h2>Editar Tarea</h2>
  
        <v-menu
          v-model="menu2"
          :close-on-content-click="false"
          :nudge-right="40"
          transition="scale-transition"
          offset-y
          min-width="auto"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="task.due_date"
              label="Picker without buttons"
              readonly
              v-bind="attrs"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="dataTasks.due_date" @input="menu2 = false"></v-date-picker>
        </v-menu>
  
        <v-text-field
          v-model="task.title"
          :rules="DataRules"
          label="Titulo"
          required
        >
        </v-text-field>
  
        <v-text-field
        v-model="task.description"
        label="Descripción"
      >
      </v-text-field>

      <v-text-field
        v-model="task.comments"
        label="Comentarios"
      >
      </v-text-field>

      <v-text-field
        v-model="task.tags"
        label="Etiquetas"
      >
      </v-text-field>
  
        <v-select
          v-model="task.is_completed"
          :rules="DataRules"
          label="Estado"
          :items="options"
          required
        >
        </v-select>
        <v-row align="center" justify="space-around">
          <v-snackbar v-model="snackbar" :timeout="4000" color="succes">
            <span>Se actualizo tarea correctamente</span>
            <v-btn color="blue" @click="snackbar = false">Close</v-btn>
          </v-snackbar>
          <v-row align="center" justify="space-around">
        <v-btn @click="editTask" depressed color="primary">
          Actualizar
        </v-btn>
        <v-btn dark to="/tasks" color="blue-grey">Salir</v-btn>
      </v-row>
        </v-row>
      </v-form>
    </v-app>
  </template>
    
    <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        snackbar: false,
        valid: true,
        DataRules: [(v) => !!v || "Este campo es requerido"],
        options: ['En progreso', 'Completada'],
        menu: false,
        modal: false,
        menu2: false,
        dataTasks: {}
      };
    },
    methods: {
      async editTask() {
        if (this.$refs.form.validate()) {
          const token = "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";
  
          const data = Object.entries(this.dataTasks),
            params = new URLSearchParams(data);
            
          const response = await axios.put(`https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks/${this.$route.params.id}`, params, {
            headers: {
              'authorization': `Bearer ${token}`,
              "content-Type": "application/x-www-form-urlencoded",
            },
          });
          if (response.status == 200 || 201) {
            this.snackbar = true;
          }
          console.log(response.data);
        }
      },
    },

    async created(){
    const token = "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";
    
    const response = await axios.get(
        `https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks/${this.$route.params.id}`,
        {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        }
      );
      this.dataTasks = response.data;
      console.log(this.dataTasks);
    }
  };
  </script>
    
    <style  scoped>
  h2 {
    text-align: center;
  }
  </style>