<template>
  <div>
    <h1>Exercise Tracker</h1>
    <div class="form">
      <label for="exercise-type">Exercise Type</label>
      <select id="exercise-type" v-model="exerciseType">
        <option value="">--Please select exercise--</option>
        <option value="running">Running</option>
        <option value="bench-press">Bench Press</option>
      </select>
      <div v-if="exerciseType === 'running'">
        <label for="time">Time (in minutes)</label>
        <input type="number" id="time" v-model="runningTime" />
        <label for="distance">Distance (in miles)</label>
        <input type="number" id="distance" v-model="runningDistance" />
      </div>
      <div v-if="exerciseType === 'bench-press'">
        <label for="sets">Sets</label>
        <input type="number" id="sets" v-model="benchPressSets" />
        <label for="reps">Reps</label>
        <input type="number" id="reps" v-model="benchPressReps" />
        <label for="weight">Weight (in lbs)</label>
        <input type="number" id="weight" v-model="benchPressWeight" />
      </div>
      <label for="date">Date</label>
      <input type="date" id="date" v-model="exerciseDate" />
      <button v-on:click="addExercise">Add Exercise</button>
    </div>
    <div class="history">
      <h2>Exercise History</h2>
      <label for="filter-date">Filter by Date:</label>
      <input type="date" id="filter-date" v-model="filterDate" />
      <label for="filter-type">Filter by Exercise Type:</label>
      <select id="filter-type" v-model="filterType">
        <option value="">--All Exercises--</option>
        <option value="running">Running</option>
        <option value="bench-press">Bench Press</option>
      </select>
      <table>
        <thead>
          <tr>
            <th>Date</th>
            <th>Exercise Type</th>
            <th>Time</th>
            <th>Distance</th>
            <th>Sets</th>
            <th>Reps</th>
            <th>Weight</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="exercise in filteredExercises" v-bind:key="exercise.id">
            <td>{{ exercise.date }}</td>
            <td>{{ exercise.type }}</td>
            <td>{{ exercise.time }}</td>
            <td>{{ exercise.distance }}</td>
            <td>{{ exercise.sets }}</td>
            <td>{{ exercise.reps }}</td>
            <td>{{ exercise.weight }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      exerciseType: "",
      runningTime: null,
      runningDistance: null,
      benchPressSets: null,
      benchPressReps: null,
      benchPressWeight: null,
      exerciseDate: "",
      exercises: [],
      filterDate: "",
      filterType: "",
    };
  },
  methods: {
    addExercise() {
      let exercise = {
        id: Math.floor(Math.random()*1000000),
type: this.exerciseType,
date: this.exerciseDate,
time: this.exerciseType === "running" ? this.runningTime : null,
distance: this.exerciseType === "running" ? this.runningDistance : null,
sets: this.exerciseType === "bench-press" ? this.benchPressSets : null,
reps: this.exerciseType === "bench-press" ? this.benchPressReps : null,
weight: this.exerciseType === "bench-press" ? this.benchPressWeight : null,
};
this.exercises.push(exercise);
this.resetForm();
},
resetForm() {
this.exerciseType = "";
this.runningTime = null;
this.runningDistance = null;
this.benchPressSets = null;
this.benchPressReps = null;
this.benchPressWeight = null;
this.exerciseDate = "";
},
},
computed: {
filteredExercises() {
let filteredExercises = this.exercises;
if (this.filterDate) {
filteredExercises = filteredExercises.filter(
(exercise) => exercise.date === this.filterDate
);
}
if (this.filterType) {
filteredExercises = filteredExercises.filter(
(exercise) => exercise.type === this.filterType
);
}
return filteredExercises;
},
},
};
</script>

<style>
.form {
  margin-bottom: 30px;
}
label {
  display: block;
  margin-bottom: 10px;
}
input,
select {
  margin-bottom: 20px;
}
button {
  margin-top: 20px;
  display: block;
}
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
thead {
  background-color: #000000;
}
th,
td {
  padding: 10px;
  text-align: left;
}
</style>