<template>
    <div>
      <canvas id="statistik"></canvas>
    </div>
    </template>
    
<script setup>
  import Chart from 'chart.js/auto';
    
  const labels = [
    'january',
    'february',
    'march',
    'april',
    'mei',
   'june',
  ];

  const data = {
    labels:labels,
    datasets:[{
      label: 'pengunjung',
      data: [20, 30, 40, 20, 30, 40],
      backgroundColor: [
      'rgb(245, 201, 228)',
      'rgb(232, 157, 202)',
      'rgb(218, 195, 213)',
      'rgb(245, 201, 228)',
      'rgb(232, 157, 202)',
      'rgb(218, 195, 213)'
    ],
    }]
  };
  
  const  config ={
    type: 'bar',
    data: data,
    options: {}
  };
    
  onMounted(()=>{
    const myChart = new Chart(
    document.getElementById('statistik'),
    config
  );
})
    
    </script>