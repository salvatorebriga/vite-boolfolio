<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    axios
      .get("http://127.0.0.1:8000/api/projects")
      .then((response) => {
        this.projects = response.data;
      })
      .catch((error) => {
        console.error("There was an error fetching the projects:", error);
      });
  },
};
</script>

<template>
  <div class="container text-center">
    <h1>APP</h1>
    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
      <div
        class="col mb-4 d-flex justify-content-center"
        v-for="project in projects"
        :key="project.id"
      >
        <div class="card" style="width: 18rem">
          <img
            src="https://www.openmindt.com/wp-content/uploads/2023/11/how-to-choose-your-programming-language-for-your-software.jpg"
            class="card-img-top"
            alt="Project Thumb"
          />
          <div class="card-body">
            <h5 class="card-title">{{ project.name }}</h5>
            <p class="card-text">{{ project.description }}</p>
            <p><strong>Category:</strong> {{ project.category.name }}</p>
            <p>
              <strong>Technologies: </strong>
              <span
                v-for="(tech, index) in project.technologies"
                :key="tech.id"
              >
                {{ tech.name
                }}<span v-if="index < project.technologies.length - 1">, </span>
              </span>
            </p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
