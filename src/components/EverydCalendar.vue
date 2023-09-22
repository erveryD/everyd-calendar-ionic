<template>
  <div class="calendar">
    <h2>{{ currentMonth }}</h2>
    <table style="height: 70vh">
      <thead>
        <tr>
          <th v-for="day in daysOfWeek" :key="day">{{ day }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(week, index) in weeks" :key="index">
          <td v-for="day in week" :key="day" :class="{ today: day === selectedDay }" @click="clickDate(day)">
            <div class="date__area">
              <span>
                {{ day }}
              </span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
  import { computed, ref } from 'vue'

  const daysOfWeek = ['일', '월', '화', '수', '목', '금', '토']
  const currentMonth = ref('')
  const currentDate = new Date()
  const selectedDay = ref(currentDate.getDate())

  const weeks = computed(() => {
    const year = currentDate.getFullYear()
    const month = currentDate.getMonth()
    const firstDay = new Date(year, month, 1)
    const lastDay = new Date(year, month + 1, 0)
    const startDay = firstDay.getDay()
    const endDay = lastDay.getDate()

    const weeks = []
    let week = []

    for (let i = 0; i < startDay; i++) {
      week.push('')
    }

    for (let day = 1; day <= endDay; day++) {
      week.push(day)

      if (week.length === 7) {
        weeks.push(week)
        week = []
      }
    }

    if (week.length > 0) {
      while (week.length < 7) {
        week.push('')
      }
      weeks.push(week)
    }

    currentMonth.value = `${year}년 ${month + 1}월`
    return weeks
  })

  function isToday(day: any) {
    const today = new Date()
    return today.getFullYear() === currentDate.getFullYear() && today.getMonth() === currentDate.getMonth() && today.getDate() === day
  }

  function clickDate(day: any) {
    console.log('[day: any]', day)
    selectedDay.value = day
  }
</script>

<style scoped>
  .calendar {
    text-align: center;
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  th {
    border: 1px solid #ccc;
    padding: 10px;
    background-color: #f2f2f2;
  }
  td {
    border: 1px solid #ccc;
    padding: 5px;
  }

  td.today {
    background-color: #009688;
    color: #fff;
    font-weight: bold;
  }

  .date__area {
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    height: 100%;
  }
</style>
