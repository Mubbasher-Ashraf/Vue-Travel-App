<template>
  <div>
    <GoBack />
    <section class="destination">
      <h1>{{ slug }}</h1>
      <div class="destination-details">
        <img
          :src="require(`@/assets/${destination.image}`)"
          :alt="destination.name"
        />
        <h2>Destination detail page: {{ destination.description }}</h2>
      </div>
    </section>
    <section class="experiences">
      <h2>Top Experience in {{ destination.name }}</h2>
      <div class="cards" id="experience">
        <div
          v-for="experience in destination.experiences"
          :key="experience.slug"
          class="card"
        >
          <router-link
            :to="{
              name: 'experienceDetails',
              params: { experienceSlug: experience.slug },
              hash: '#experience',
            }"
          >
            <img
              :src="require(`@/assets/${experience.image}`)"
              :alt="experience.name"
            />
            <span class="card_text">
              {{ experience.name }}
            </span>
          </router-link>
        </div>
      </div>
      <router-view :key="$route.path" />
    </section>
  </div>
</template>

<script>
import store from "@/store";
import GoBack from "../components/GoBack.vue";

export default {
  components: {
    GoBack,
  },
  data() {
    return {
      // slug: this.$route.params.slug,
    };
  },
  props: {
    slug: {
      type: String,
      required: true,
    },
  },
  computed: {
    destination() {
      return store.destinations.find(({ slug }) => slug === this.slug);
    },
  },
};
</script>

<style scoped>
img {
  max-width: 600px;
  width: 100%;
  height: auto;
  max-height: 400px;
}

.destination-details {
  display: flex;
  justify-content: space-between;
}

p {
  margin: 0 40px;
  font-size: 20px;
  text-align: left;
}
.cards {
  display: flex;
}

.cards img {
  max-height: 200px;
}

.card {
  position: relative;
  padding: 0 20px;
}

.experiences {
  padding: 40px 0;
}

.card_text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 25px;
  font-weight: bold;
  text-decoration: none;
}
</style>
