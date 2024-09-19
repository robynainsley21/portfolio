<template>
  <div class="row contact-content">
    <div class="col-md-6">
      <div v-if="contact?.length">
        <p>{{ contact[0].number }}</p>
      </div>
      <SpinnerComp v-else />
    </div>
    <form
      class="col-md-6 form-box"
      action="https://formspree.io/f/xwkgyjal"
      method="POST"
      id="contact-form"
      target="_blank"
    >
      <div class="contact-box">
        <div class="mb-3 contact-item">
          <input
            placeholder="Your name"
            class="input form-control"
            name="text"
            type="text"
            aria-describedby="emailHelp"
            required
          />
        </div>
        <div class="mb-3 contact-item">
          <input
            placeholder="Email address"
            class="input form-control"
            name="text"
            type="email"
            aria-describedby="emailHelp"
            required
          />
        </div>
        <div class="mb-3 contact-item">
          <input
            placeholder="Your message"
            class="input form-control message"
            name="message"
            type="text"
            aria-describedby="message"
            required
          />
        </div>
      </div>

      <div class="d-flex justify-content-around">
        <button type="submit" class="btn submit-btn fw-bold">Submit</button>
        <button type="reset" class="btn pink-btn fw-bold">Clear</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import SpinnerComp from "@/components/Spinner.vue";
import { computed, onMounted } from "vue";
import { useStore } from "vuex";
const store = useStore();
const contact = computed(() => store.state.contact);

onMounted(() => {
  store.dispatch("fetchContact");
});
</script>

<style scoped>
#contact-form {
  width: 70%;
  margin: auto;
}

.form-box{
  border: 3px solid #000;
  box-shadow: 15px 15px 0 -2.5px #fff, 15px 15px 0 0 #000;
  padding: 2rem;
}

.contact-box {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.contact-item {
  width: 80%;

  & .message {
    height: 5rem;
  }
}

/* From Uiverse.io by anniekoop */
.input {
  font-family: "SF Pro";
  padding: 0.875rem;
  font-size: 1rem;
  border: 1.5px solid #000;
  border-radius: 0.5rem;
  box-shadow: 2.5px 3px 0 #000;
  outline: none;
  transition: ease 0.25s;
  font-family: "Share Tech Mono", monospace ;
}

.input:focus {
  box-shadow: 5.5px 7px 0 black;
}

.contact-content {
  margin-bottom: 7rem;
  font-family: "Share Tech Mono", monospace ;
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


/**mobile */
@media screen and (max-width: 768px) {
  .contact-item{
    width: 100%;
    margin: 0;
  }

  .form-box{
    padding: .8rem;
  }

  .btn{
    width: 5rem;
  }
}
/**mobile */
</style>
