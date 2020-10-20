<template>
  <div class="date-display-container">
    <p id="date-display-day">{{getDay}}</p>
    <p id="date-display-month">{{getMonth}}</p>
    <p id="date-display-year">{{getYear}}</p>
  </div>
</template>

<script>
import {getDateParts} from '../../utils/utils';

export default {   
    name: 'DateDisplay',
    components: {
    },
    props: {
      todaysDate: Date
    },
    computed: {
        getDay() {
            return getDateParts(this.todaysDate).day;
        },
        getMonth() {
            return getDateParts(this.todaysDate).month;
        },
        getYear() {
            return getDateParts(this.todaysDate).year;
        }
    },
    created() {
        console.log(this.todaysDate);
    }
}
</script>

<style scoped>
.date-display-container {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;

    height: 20rem;
    width: 75%;

    border-radius: 0.25rem;
    padding: 1rem;

    background-color: var(--colour-primary);
    color: var(--text-colour-light);
}

#date-display-day {
    font-size: 8rem;
}

#date-display-month {
    font-size: 2rem;
    text-transform: uppercase;
}

#date-display-year {
    font-size: 1rem;
}
</style>
