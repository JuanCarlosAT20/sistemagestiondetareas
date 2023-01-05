<template>
  <v-app>
    <v-form ref="form" v-model="valid" lazy-validation>
      <h2>Agregar Tarea</h2>

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
        <v-date-picker v-model="task.due_date" @input="menu2 = false"></v-date-picker>
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
          <span>Se agrego usuario correctamente</span>
          <v-btn color="blue" @click="snackbar = false">Close</v-btn>
        </v-snackbar>
        <v-btn @click="addTask" depressed color="primary"> Agregar </v-btn>
        <v-btn dark to="/tasks" color="blue-grey">Salir</v-btn>
      </v-row>
    </v-form>
  </v-app>
</template>
  
  <script>
import axios from "axios";

export default {
  name: "BaseNewTaskForm",

  data() {
    return {
      snackbar: false,
      valid: true,
      DataRules: [(v) => !!v || "Este campo es requerido"],
      options: ['En progreso', 'Completada'],
      
      task: {
        token: '',
        title: '',
        is_completed: [],
        due_date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
        description: '',
        comments: '',
        tags: ''
      },
      menu: false,
      modal: false,
      menu2: false,
    };
  },
  computed: {
 value: function (){
  return Number(this.options)
 }
  },
  methods: {
    async addTask() {
      if (this.$refs.form.validate()) {
        const url = "https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks";
        const token =
          "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";

        const data = Object.entries(this.task),
          params = new URLSearchParams(data);

        const response = await axios.post(url, params, {
          headers: {
            'Authorization': `Bearer ${token}`,
            "Content-Type": "application/x-www-form-urlencoded",
          },
        });
        if (response.status == 200 || 201) {
          this.snackbar = true;
        }
      }
    },
  },
};
</script>
  
  <style  scoped>
h2 {
  text-align: center;
}
</style>