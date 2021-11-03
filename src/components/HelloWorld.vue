<template>
  <section>
    <h2 class="text-danger text-center">My calander vue</h2>
  </section>
  <section class="bg-primary d-flex flex-column justify-content-center"
  ><h1 class="text-black">{{ getCurrentMonthName }}, {{ currentYear }}</h1></section>
  <section>
    <div class="days d-flex flex-row">
      <br>
      <p class="text-center " v-for="(day,key) in days" :key="key"><b>{{ day }}</b></p>
    </div>
    <div class="dates d-flex flex-row">
      <p class="text-center" v-for="(date,key) in getFastDayInMonth" :key="key"></p>
      <p :class="todayDate(date) ? 'text-primary':'' " v-for="(date,key) in getLastDayInMonth" :key="key">{{ date }}</p>
    </div>
  </section>
  <br>
  <br>
  <br>
  <section class="d-flex justify-content-around">
    <button class="btn btn-primary" @click="prev()">prev</button>
    <button class="btn btn-primary" @click="next()">next</button>
  </section>
</template>

<script>

export default {
  name: 'HelloWorld',
  data: function () {
    return {
      days: ['Sun', 'Mon', 'Tu', 'Wed', 'Thus', 'Fri', 'Sat'],
      currentYear: (new Date()).getFullYear(),
      currentMonth: (new Date()).getMonth(),
      currentDay: (new Date()).getDate(),
    }
  },
  computed: {
    getCurrentMonthName() {
      return new Date(this.currentYear, this.currentMonth, this.currentDay).toLocaleString('default', {month: 'long'});
    },
    getLastDayInMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    getFastDayInMonth() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    }
  },
  methods: {
    prev() {
      if (this.currentMonth == 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    next() {
      if (this.currentMonth == 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    todayDate(date){
      console.log(new Date(this.currentYear, this.currentMonth, date).toDateString());
      return  new Date(this.currentYear, this.currentMonth, date).toDateString() == new Date().toDateString();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.days p, .dates p {
  width: 14.28%;
}

.dates {
  flex-wrap: wrap;
}
</style>
