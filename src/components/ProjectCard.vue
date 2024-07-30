<script>
export default {
  name: "ProjectCard",
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
};
</script>

<template>
  <div class="col mb-4 d-flex justify-content-center">
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
          <span v-for="(tech, index) in project.technologies" :key="tech.id">
            {{ tech.name
            }}<span v-if="index < project.technologies.length - 1">, </span>
          </span>
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
