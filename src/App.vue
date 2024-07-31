<script>
import axios from "axios";
import ProjectCard from "./components/ProjectCard.vue";

export default {
  name: "App",
  components: {
    ProjectCard,
  },
  data() {
    return {
      projects: [],
      pagination: {
        current_page: 1,
        last_page: 1,
        prev_page_url: null,
        next_page_url: null,
      },
    };
  },
  methods: {
    fetchProjects(url = "http://127.0.0.1:8000/api/projects") {
      axios
        .get(url)
        .then((response) => {
          this.projects = response.data.data;
          this.pagination = {
            current_page: response.data.current_page,
            last_page: response.data.last_page,
            prev_page_url: response.data.prev_page_url,
            next_page_url: response.data.next_page_url,
          };
        })
        .catch((error) => {
          console.error("There was an error fetching the projects:", error);
        });
    },
    loadPage(url) {
      this.fetchProjects(url);
    },
    getPageUrl(page) {
      return `http://127.0.0.1:8000/api/projects?page=${page}`;
    },
  },
  mounted() {
    this.fetchProjects();
  },
};
</script>
<template>
  <div class="container text-center">
    <h1>APP</h1>
    <div
      class="row justify-content-center row-cols-1 row-cols-sm-2 row-cols-md-3"
    >
      <ProjectCard
        v-for="project in projects"
        :key="project.id"
        :project="project"
      />
    </div>
    <div class="pagination-controls fixed-bottom text-center py-3">
      <button
        class="btn btn-secondary mx-1"
        :disabled="!pagination.prev_page_url"
        @click="loadPage(pagination.prev_page_url)"
      >
        Previous
      </button>
      <button
        v-for="page in pagination.last_page"
        :key="page"
        class="btn btn-secondary mx-1"
        :class="{ 'btn-primary': page === pagination.current_page }"
        @click="loadPage(getPageUrl(page))"
      >
        {{ page }}
      </button>
      <button
        class="btn btn-secondary mx-1"
        :disabled="!pagination.next_page_url"
        @click="loadPage(pagination.next_page_url)"
      >
        Next
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.pagination-controls {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: white;
  padding: 1rem 0;
  box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.1);
}
</style>
