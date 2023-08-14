<script setup>
import { onBeforeMount,onMounted, onBeforeUnmount, ref } from 'vue';

let pieChart = null
// chart data
const data = {
  labels: [
    'Red',
    'Green',
    'Blue',
    'Purple'
  ],
  datasets: [{
    data: [30, 30, 30, 10],
    backgroundColor: [
      'red',
      'green',
      'blue',
      'purple'
    ],
    hoverOffset: 4
  }]
};

// Pie chart configuration
const pieConfig = {
  type: 'pie',
  data: data,
  options: {
    responsive: true
  }
};

onBeforeMount(() => {
  console.log("Before Mounted")
})

onMounted(() => {
  // Get a reference to the canvas element
  const pieCtx = document.getElementById('myPieChart').getContext('2d');
  // Create the pie chart
  pieChart = new Chart(pieCtx, pieConfig);
})

onBeforeUnmount(() => {
  pieChart.destroy()
  console.log("Before Unmounted all data cleanup done")
})

const colorName = ref('')
const colorPercent = ref('')

function updateChart(){
  data.labels.push(colorName.value)
  data.datasets[0].data.push(colorPercent.value)
  data.datasets[0].backgroundColor.push(colorName.value.toLowerCase())

  pieChart.update()

}
</script>

<template>
  <div class="container flex flex-col mx-auto items-center justify-between-center pt-10">
    <div class="w-2/6">
      <h1 class="text-4xl text-gray-900 text-center">Pie Chart</h1>
      <canvas id="myPieChart"></canvas>
    </div>
    <form>
      <div class="grid gap-6 mb-6 md:grid-cols-3 mt-5">
        <div>
          <input v-model="colorName" type="text" id="color_name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Adding Color Name">
        </div>
        <div>
          <input v-model="colorPercent" type="number" id="color_percent" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Percent">
        </div>
        <div>
          <button @click.prevent="updateChart()" type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add to Chart</button>
        </div>
      </div>
    </form>
  </div>

</template>

<style scoped>

</style>
