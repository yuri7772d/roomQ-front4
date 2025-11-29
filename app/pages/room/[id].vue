<template>
  <div class="flex">
    <div class="w-1/2 p-4">
      <div class="bg-white shadow-md rounded-md p-4 ">
        <div class="flex justify-between items-center" style="width: 100%;">
          <button @click="onPassMonth()">
              < </button>
              <h2 class="text-xl font-semibold mb-4">{{showYM}}</h2>
              <button @click="onNextMonth()"> > </button>
          </div>

          <div class="grid grid-cols-7 gap-2">

          <div v-for="dayName in WeekDayNames">
            <p class="text-center">{{ dayName }}</p>
          </div>
          <div v-for="day in showdayInCall">
            <p class="text-center">{{ day }}</p>
          </div>

        </div>
      </div>
    </div>


    <div class="w-1/2 p-4">
      <div class="bg-white shadow-md rounded-md p-4">
        <h2 class="text-xl font-semibold mb-4">Details for 13/10/2025</h2>
        <div class="space-y-4">
          <div>
            <h3 class="font-semibold">puri</h3>
            <p>งานประชุมครั้งที่ 1</p>
            <ul class="list-disc pl-5">
              <li>กินข้าว</li>
              <li>นอน</li>
            </ul>
          </div>

          <div>
            <h3 class="font-semibold">lung</h3>
          </div>

          <div>
            <h3 class="font-semibold">nerd</h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  middleware: 'role'
})
function getDaysInMonth(year, month) {
  const nextMonth = new Date(year, month + 1, 1);
  const lastDayOfMonth = new Date(nextMonth - 1);
  return lastDayOfMonth.getDate();
}
  const showdayInCall = ref(null);
function render(date) {
  const currentDate = new Date(date);
  
  let dayInCall = [];


  const firstDay = new Date(currentDate.getFullYear(), currentDate.getMonth(), 1)
  const firstDayNumber = firstDay.getDay()
  for (let index = 0; index < firstDayNumber; index++) {
    dayInCall.push(null)
    console.log('asdfaf')
  }

  const year = currentDate.getFullYear();
  const month = currentDate.getMonth();
  const daysInMonth = getDaysInMonth(year, month);

  for (let index = 0; index < daysInMonth; index++) {
    dayInCall.push(index + 1)
    console.log('asdfaf')
  }
  showdayInCall.value = dayInCall
  showYM.value = `${month+1}/${year}`;
}

const WeekDayNames = ["Sat", "Mon", "Tue", "Wed", "Thu", "Thu", "Fri"];
let currentDate = new Date();
const showYM = ref(null);
render(currentDate);

function onNextMonth() {
  currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth() + 1, 1)
  render(currentDate)
}
function onPassMonth() {
  currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth() - 1, 1)
  render(currentDate)
}
</script>
