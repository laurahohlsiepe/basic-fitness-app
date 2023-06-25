


<template>
  <header>
      <div class="flex flex-wrap justify-center items-center mx-auto max-w-screen-xl">
         <h1 class="text-pink-400 text-2xl text-center mt-7">This the most basic Fitness App ever</h1>       
      </div>
  </header>
  <body class=" full-screen">

  <section class="flex flex-col md:flex-col sm:mx-16 lg:mx-20">
    <h2 class="text-2xl text-center py-6">Make yourself your workout with the name/description and choose the repetitions</h2>
  <div class="flex flex-col justify-center align-between">

    <div class="flex justify-center">
         <input type="text" class="w-1/2 rounded bg-fuchsia-200 px-5 py-2.5 mr-2 mt-2" v-model="workoutText" placeholder="add new workout here with sets and repetitions"> 
    </div>

    <div class="flex justify-center m-6">
          <label for="reps" class="mx-4">Choose your reps:</label>
    <select v-model="selectedValue">
      <option v-for="repetition in repetitions" :key="repetition.value" :value="repetition.value">{{ repetition.name }}</option>
    </select>
    </div>

    <div class="flex justify-center">
      <button class="text-white bg-pink-400 font-medium rounded-lg px-5 py-2.5 w-32 h-1/3 text-center" type="submit" @click="addWorkout(); clearAfterSubmit(); showSelectedOption()">send</button>    
    </div>

  </div>

  <div class="flex">
    <div class="overflow-x-auto mt-6 mb-12">
       <table class="table-fixed w-full text-sm text-left text-gray-500 dark:text-gray-400">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
        <tr>
          <th scope="col" class="px-6 py-3">Name</th>
      </tr>
      </thead>
      <tbody>
        <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">RDLs</th>
        </tr>
        <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <th  scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">Squats</th>
        </tr>
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-for="workout in workouts">
            <td scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
              {{ workout.text }}
            </td>
          </tr>
      </tbody>
    </table>  
    </div>

      <div class="overflow-x-auto mt-6 mb-12">
      <table class="table-fixed w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
          <tr>
          <th scope="col" class="px-6 py-3">Reps</th>
      </tr>
        </thead>
        <tbody>
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700"> 
              <th class="px-6 py-4 text-gray-900">3x10-12</th>
          </tr>
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700"> 
              <th class="px-6 py-4 text-gray-900">4x10-12</th>
          </tr>
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-if="showOutput" v-for="(option, index) in selectedOptions" :key="index">
            <td class="px-6 py-4 text-gray-900 whitespace-nowrap dark:text-white">
               {{ getDescription(option) }}
            </td>   
          </tr>
        </tbody>
    </table>
  </div>
</div>
  </section>
</body>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      workouts: [],
      workoutText: '',
      selectedValue: '',
      selectedOptions: [],
      repetitions: [
     {value: 'easy', name: 'Easy'},
     {value: 'medium', name: 'Medium'},
     {value: 'advanced', name: 'Advanced'}
      ],
      showOutput: false
    }
  },
  created() {
    this.initialSelectedOption = this.selectedValue;
  },
  computed: {
    latestSelectedOption() {
      return this.selectedOptions[this.selectedOptions.length - 1]; 
    }
  },
  methods: {
    addWorkout(option) {
      const newWorkouts = this.workoutText;
      this.workoutText = '';
      this.workouts = [
        ...this.workouts,
        {text: newWorkouts}
      ]
    },
    showSelectedOption() {
      if (this.selectedValue) {
        this.selectedOptions = [...this.selectedOptions, this.selectedValue]; 
        this.showOutput = true; 
      }
    },
    clearAfterSubmit() {
      this.workoutText = '';
    },
    getDescription(option) {
      if (option === 'easy') {
        return '4x10-12';
      } else if (option === 'medium') {
        return '4x8-10';
      } else if (option === 'advanced') {
        return '3x8-10';
      }
      return '';
    }
  }
}
</script>


