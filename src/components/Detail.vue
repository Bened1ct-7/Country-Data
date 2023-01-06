<template>
  <div>
    <div @click="showdata" class="name mb-4 mb-md-3">{{ name }}</div>
    <div class="flex">
      <div>
        <p>
          <span>Official Name: </span>
          <span class="fw-light">{{ officialName }}</span>
        </p>
        <p>
          <span>Population: </span>
          <span class="fw-light">{{ population }}</span>
        </p>
        <p>
          <span>Region: </span>
          <span class="fw-light">{{ region }}</span>
        </p>
        <p>
          <span>Sub Region: </span>
          <span class="fw-light">{{ subregion }}</span>
        </p>
        <p>
          <span>Capital: </span>
          <span class="fw-light">{{ capital }}</span>
        </p>
      </div>
      
      <div>
        <p>
          <span>UN Member: </span>
          <span class="fw-light">{{ unMember }}</span>
        </p>
        <p>
          <span>Currency: </span>
          <span class="fw-light">{{ currency }} ({{ symbol }})</span>
        </p>
        <p>
          <span>Language: </span>
          <span class="fw-light">{{ language }}</span>
        </p>
      </div>
    </div>
    <div class="mt-4 mt-md-3">
      <div class="name mb-4 mb-md-3">Border Countries </div>
      <div v-if="borders" class="btns">
        <Border @getNewData="getNewData" v-for="border in borders" :key="uniqueId('border-')" :name="border" />
      </div>
      <div v-else class="else my-4">No information available</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import uniqueId from 'lodash.uniqueid'
import Border from './Border.vue'

const emit = defineEmits(['getNewData'])
const name = ref(null)
const officialName = ref(null)
const population = ref(null)
const region = ref(null)
const subregion = ref(null)
const capital = ref(null)
const unMember = ref(null)
const currency = ref(null)
const symbol = ref(null)
const language = ref(null)
const borders = ref(null)

const props = defineProps(['nations'])

const assign = (data) => {
  name.value = data.name.common
  officialName.value = data.name.official
  population.value = data.population
  region.value = data.region
  subregion.value = data.subregion
  capital.value = data.capital[0]
  unMember.value = (data.unMember === true) ? 'Yes' : 'No'
  borders.value = data.borders
}

const showdata = () => {
  console.log(props.nations)
}

const assignCurr = (obj) => {
  for (let key in obj) {
    if(obj[key]) {
      currency.value = obj[key].name
      symbol.value = obj[key].symbol
    }
  }
}

const assignLang = (obj) => {
  for (let key in obj) {
    if (obj[key]) {
      language.value = obj[key]
    }
  }
}

onMounted(async () => {
  await assign(props.nations)
  await assignCurr(props.nations.currencies)
  await assignLang(props.nations.languages)
})

const getNewData = (data) => {
  emit('getNewData', data)
}

</script>

<style scoped>
.name {
  font-size: 1.4rem;
}

.flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

p {
  margin: .1rem 0;
}

.btns {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  font-size: .9rem;
  gap: 1rem;
}

.btns a {
  border-radius: 3px;
}

.else {
  opacity: 0.7;
}

@media only screen and (max-width: 768px) {
  .flex {
    display: block;
  }
  
  .flex > div + div {
    margin-top: 2rem;
  }
  
  .name {
    margin-bottom: 2.3rem;
  }
  
  p {
    margin-top: 0.25rem;
  }
  
}
</style>