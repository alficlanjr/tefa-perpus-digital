<script setup lang="ts">
import Chart from 'chart.js/auto';

const labels = [
    'January',
    'Pebruari',
    'Marc',
    'April',
    'May',
    'june',
];

const data = {
    labels: labels,
    datasets: [{
        labels: 'My First dataset',
        backgroundColor: 'rgb(197, 224, 239)',
        borderColor: 'rgb(225, 99, 132)',
        data: [0, 10, 5, 2, 20, 30, 45],
    }]
}

const config = {
    type:'bar',
    data: data,
    options: {}
};

onMounted(() => {
    const myChart = new Chart(document.getElementById("myChart"),config);
});
</script>

<template>
    <div>
        <canvas id="myChart"></canvas>
    </div>
</template>