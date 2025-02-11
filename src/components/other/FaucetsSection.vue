<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import manticoreImage from '@/assets/faucets/manticore.svg'
import evrlandImage from '@/assets/faucets/evrland.svg'

export default defineComponent({
  name: 'FaucetsSection',
  props: {
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const resourceItems = ref([
      {
        text: 'EvrLand',
        image: evrlandImage,
        url: 'https://faucet.evrland.net/'
      },
      {
        text: 'Manticore',
        image: manticoreImage,
        url: 'https://manticore.exchange/faucet'
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (url: string) => {
      window.open(url, '_blank')
    }

    return { resourceItems, backgroundImageComputed, handleClick }
  }
})
</script>

<template>
  <section class="faucets-section">
    <v-container>
      <h2 class="section-title">Faucets</h2>
      <v-row class="card-row">
        <v-col
          cols="12"
          xs="12"
          sm="12"
          md="3"
          lg="2"
          xl="2"
          v-for="(item, index) in resourceItems"
          :key="index"
          class="card-col"
        >
          <a :href="item.url">
            <img v-if="item.image" :src="item.image" :alt="item.text" class="resource-image" />
          </a>
          <p class="resource-text">{{ item.text }}</p>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.faucets-section {
  height: 650px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('@/assets/landing_sections/landing_section_f8.png');
  background-size: cover;
  background-position: center;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 2.5rem;
    font-weight: bold;
    color: #000000;
    text-align: center;
    margin-bottom: 2rem;
  }

  .card-row {
    max-width: 1200px;
    display: flex;
    align-items: start;
    justify-content: center;
    margin: 0 auto;
  }

  .card-col {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.2s ease;

    &:hover {
      transform: scale(1.05);
    }

    &:active {
      transform: scale(0.95);
    }
  }

  .resource-image {
    width: 160px;
    height: 160px;
    margin-bottom: 10px;
  }

  .resource-text {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.6;
    opacity: 0.67;
    text-align: center;
  }
}

@media (max-width: 959px) {
  .faucets-section {
    height: auto;
    height: 650px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;
      margin-bottom: 1.5rem;
    }

    .resource-image {
      width: 120px;
      height: 120px;
      margin-bottom: 10px;
    }
  }
}

@media (max-width: 599px) {
  .faucets-section {
    .section-title {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }

    .resource-image {
      width: 100px;
      height: 100px;
    }

    .resource-text {
      font-size: 0.9rem;
    }
  }
}
</style>
