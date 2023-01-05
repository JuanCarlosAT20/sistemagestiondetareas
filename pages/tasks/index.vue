<template>
  <v-app id="inspire">
    <base-bar-navigation
    :completed-tasks="taskCompleteFilter"
    :incompleted-tasks="taskIncompleteFilter"
    ></base-bar-navigation>
    <v-main>
      <!--Componente para agregar tarea-->
      <base-button-add-user />
      <v-row class="black" md="6" lg="6" xl="6">
        <v-col  cols="6" class="shrink">
          <!--Componente para mostrar tareas-->
          <base-card
            v-for="task in taskIncompleteFilter"
            :key="task.id"
            :task-id="task.id"
            :date="task.due_date"
            :title="task.title"
            :description="task.description"
            :is-complete="task.is_completed"
            @reloadAllTasks="getAllTasks"
          ></base-card>
        </v-col>
          <v-col cols="6" class="shrink" >
            <base-card
              v-for="task in taskCompleteFilter"
              :key="task.id"
              :task-id="task.id"
              :date="task.due_date"
              :title="task.title"
              :description="task.description"
              :is-complete="task.is_completed"
              @reloadAllTasks="getAllTasks"
            ></base-card>
          </v-col>

      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import BaseCard from "../../components/BaseCard.vue";
import BaseButtonAddUser from "../../components/BaseButtonAddUser.vue";
import BaseBarNavigation from "../../components/BaseBarNavigation.vue";


export default {
  components: {
    BaseCard,
    BaseButtonAddUser,
    BaseBarNavigation,
  },
  created() {
    this.getAllTasks();
  },
  methods: {
    async getAllTasks() {
      const token =
        "e864a0c9eda63181d7d65bc73e61e3dc6b74ef9b82f7049f1fc7d9fc8f29706025bd271d1ee1822b15d654a84e1a0997b973a46f923cc9977b3fcbb064179ecd";

      const response = await axios.get(
        "https://ecsdevapi.nextline.mx/vdev/tasks-challenge/tasks",
        {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        }
      );
      this.allTasks = response.data;
      console.log(response.data);
    },
  },
  data() {
    return {
      allTasks: [],

    };
  },
  computed: {
    taskCompleteFilter() {
      return this.allTasks.filter((task) => task.is_completed === 1);
    },
    taskIncompleteFilter() {
      return this.allTasks.filter((task) => task.is_completed === 0);
    },
  },
};
</script>