<template>
  <!-- <div class="card-container row gap-5" v-if="projects?.length">
    <div
      class="info-card p-0 project-card"
      v-for="project in projects"
      :key="project.id"
    >
      <div class="image"><img :src="project.img_url" alt="project-img" /></div>
      <div class="info">
        <h5>{{ project.projectName }}</h5>
        <div class="description">{{ project.description }}</div>
        <div class="buttons-box">
          <a class="btn" type="button" :href="project.github" target="blank"
            >GitHub</a
          >
          <a
            class="btn"
            type="button"
            :href="project.hosted_link"
            target="blank"
            >Live site</a
          >
        </div>
      </div>
    </div>
  </div> -->

  
  <div class="container row gap-5" v-if="projects?.length">
    <div class="card" v-for="project in projects"
    :key="project.id">
      <div class="card__image-container">
        <img
          class="card__image"
          :src="project.img_url" 
          alt="project-img"
        />
      </div>

      <svg class="card__svg" viewBox="0 0 800 500">
        <path
          d="M 0 100 Q 50 200 100 250 Q 250 400 350 300 C 400 250 550 150 650 300 Q 750 450 800 400 L 800 500 L 0 500"
          stroke="transparent"
          fill="#333"
        />
        <path
          class="card__line"
          d="M 0 100 Q 50 200 100 250 Q 250 400 350 300 C 400 250 550 150 650 300 Q 750 450 800 400"
          stroke="pink"
          stroke-width="3"
          fill="transparent"
        />
      </svg>

      <div class="card__content">
        <h5>{{ project.projectName }}</h5>
        <p>{{ project.description }}</p>
      </div>
    </div>
  </div>
  <SpinnerComp v-else />

</template>

<script setup>
import SpinnerComp from "@/components/Spinner.vue";
import { computed, onMounted } from "vue";
import { useStore } from "vuex";
const store = useStore();
const projects = computed(() => store.state.projects);

onMounted(() => store.dispatch("fetchProjects"));
</script>

<style scoped>



img {
  max-width: 100%;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #444;
}

.card {
  position: relative;
  background: #333;
  width: 300px;
  height: 20rem;
  border-radius: 6px;
  padding: 2rem;
  color: #aaa;
  box-shadow: 0 0.25rem 0.25rem rgba(0, 0, 0, 0.2), 0 0 1rem rgba(0, 0, 0, 0.2);
  overflow: hidden;
  font-size: 1rem;
}
.card__image-container {
  margin: -2rem -2rem 1rem -2rem;
}
.card__line {
  opacity: 0;
  animation: LineFadeIn 0.8s 0.8s forwards ease-in;
}
.card__image {
  opacity: 0;
  animation: ImageFadeIn 0.8s 1.4s forwards;
}
.card__title {
  color: white;
  margin-top: 0;
  font-weight: 800;
  letter-spacing: 0.01em;
}
.card__content {
  margin-top: -1rem;
  opacity: 0;
  animation: ContentFadeIn 0.8s 1.6s forwards;
}
.card__svg {
  position: absolute;
  left: 0;
  top: -15px;
}

@keyframes LineFadeIn {
  0% {
    opacity: 0;
    d: path("M 0 300 Q 0 300 0 300 Q 0 300 0 300 C 0 300 0 300 0 300 Q 0 300 0 300 ");
    stroke: #fff;
  }
  50% {
    opacity: 1;
    d: path("M 0 300 Q 50 300 100 300 Q 250 300 350 300 C 350 300 500 300 650 300 Q 750 300 800 300");
    stroke: #888BFF;
  }
  100% {
    opacity: 1;
    d: path("M -2 100 Q 50 200 100 250 Q 250 400 350 300 C 400 250 550 150 650 300 Q 750 450 802 400");
    stroke: #545581;
  }
}
@keyframes ContentFadeIn {
  0% {
    transform: translateY(-1rem);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
@keyframes ImageFadeIn {
  0% {
    transform: translate(-0.5rem, -0.5rem) scale(1.05);
    opacity: 0;
    filter: blur(2px);
  }
  50% {
    opacity: 1;
    filter: blur(2px);
  }
  100% {
    transform: translateY(0) scale(1);
    opacity: 1;
    filter: blur(0);
  }
}











img[alt="project-img"] {
  /* perspective: 1000;
  height: 7rem;
  position: absolute;
  top: -1rem;
  left: 50%;
  transform: translateX(-50%); */
  height: 100%;
}

.project-card {
  height: 25rem;
  display: flex;
  flex-direction: column;
  margin: auto;
  width: 18rem;

  & .project-header {
    align-items: flex-start;
    font-size: 1rem;
    width: 90%;
  }
}

/**button */
/* From Uiverse.io by adamgiebl */
.btn {
  --purple: #5a639c;
  /* padding: 0.6rem 1.5rem; */
  letter-spacing: 0.08em;
  position: relative;
  font-family: inherit;
  width: 7rem;
  font-weight: bold;
  border-radius: 0.6em;
  overflow: hidden;
  transition: all 0.3s;
  border: 2px solid var(--purple);
  background: linear-gradient(
    to right,
    rgba(155, 126, 218, 0.1) 1%,
    transparent 40%,
    transparent 60%,
    rgba(155, 126, 218, 0.1) 100%
  );
  color: var(--purple);
  box-shadow: inset 0 0 10px rgba(155, 126, 218, 0.4),
    0 0 9px 3px rgba(155, 126, 218, 0.1);
}
/**comment */
.btn:hover {
  color: #bfa3f3;
  box-shadow: inset 0 0 10px rgba(155, 126, 218, 0.6),
    0 0 9px 3px rgba(155, 126, 218, 0.2);
}

.btn:before {
  content: "";
  position: absolute;
  left: -4em;
  width: 4em;
  height: 100%;
  top: 0;
  transition: transform 0.4s ease-in-out;
  background: linear-gradient(
    to right,
    transparent 1%,
    rgba(155, 126, 218, 0.1) 40%,
    rgba(155, 126, 218, 0.1) 60%,
    transparent 100%
  );
}

.btn:hover:before {
  transform: translateX(15em);
}
/**button */

/* Container */
.card-container {
  width: 100vw;
  margin: auto;
  background-color: #f7fafc;
  padding: 40px auto;
  align-items: center;
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
}
.card-container > .title {
  width: 100%;
  font-weight: 600;
  margin-bottom: 24px;
}

/* Card Component */
.info-card {
  width: 304px;
  height: 300px;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: auto;
  margin-right: 40px;
  margin-bottom: 40px;
  transition: transform 500ms;
  transition-timing-function: cubic-bezier(1, -0.65, 0, 1.31);
  cursor: pointer;
}
.info-card.-expanded {
  transform: scale(1.08);
}
.info-card > .image {
  background-color: #293745;
  width: 100%;
  height: 224px;
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
}
.info-card > .image > img {
  width: 100%;
  height: 100%;
  -o-object-fit: cover;
  object-fit: cover;
  transition: opacity 400ms ease-in, transform 500ms ease-in;
}
.info-card.-expanded > .image > img {
  opacity: 0.2;
  transform: scale(1.1);
}
.info-card > .info {
  width: 280px;
  height: 280px;
  color: #f5f7f8;
  border-radius: 4px;
  padding: 16px 24px;
  position: absolute;
  bottom: -2rem;
  background-color: #151823;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
  transition: box-shadow 400ms;
}
.info-card:hover > .info,
.info-card.-expanded > .info {
  box-shadow: 0 6px 60px rgba(0, 0, 0, 0.1);
}

.info-card > .info > .description {
  /* font-weight: 300; */
  color: #f5f7f8;
  height: 60%;
  text-overflow: ellipsis;
  line-height: 1.5rem;
  font-size: 1rem;
  overflow: hidden;
  transition: height 500ms;
  transition-timing-function: cubic-bezier(1, -0.65, 0, 1.31);
}
</style>
