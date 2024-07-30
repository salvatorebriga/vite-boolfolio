<script>
import axios from "axios";
import ProjectCard from "./components/ProjectCard.vue";

export default {
  name: "App",
  components: {
    ProjectCard,
  },
  methods: {
    index() {
      axios
        .get("http://127.0.0.1:8000/api/projects")
        .then((response) => {
          this.projects = response.data;
        })
        .catch((error) => {
          console.error("There was an error fetching the projects:", error);
        });
    },
  },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    this.index();
  },
};
</script>

<template>
  <div class="container text-center">
    <h1>APP</h1>
    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
      <ProjectCard
        v-for="project in projects"
        :key="project.id"
        :project="project"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
