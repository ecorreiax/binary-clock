<template>
  <div class="clock-cointainer">
    <div class="clock">
      <div class="clock-col" 
        v-for="(clock, colIdx) in settings" 
        :key="colIdx"
      >
        <ul>
          <li 
            class="clock-slot" 
            v-for="(slot, slotIdx) in clock.slots" 
            :key="slotIdx"
            :class="isActive(colIdx, slotIdx) ? 'l-active' : ''"
          ></li>
        </ul>
      </div>
    </div>
    <h1>{{time}}</h1>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data() {
    return {
      time: null,
      interval: null,
      settings: [{
        slots: 2,
        binary: 0
      }, {
        slots: 4,
        binary: 0
      }, {
        slots: 3,
        binary: 0
      }, {
        slots: 4,
        binary: 0
      }, {
        slots: 3,
        binary: 0
      }, {
        slots: 4,
        binary: 0
      }],
    }
  },
  beforeDestroy() {
    clearInterval(this.interval)
  },
  created() {
    this.interval = setInterval(() => {
      this.time = Intl.DateTimeFormat(navigator.language, {
        hour: 'numeric',
        minute: 'numeric',
        second: 'numeric'
      }).format()
      this.getBinarySum()
    }, 1000)
  },
  methods: {
    getBinarySum() {
      let self = this
      let parsedTime = this.time.replaceAll(':', '')
      for (let index = 0; index < parsedTime.length; index++) {
        let number = parseInt(parsedTime[index])
        self.settings[index].binary = Number(number).toString('2')
      }
    },
    isActive(colIdx, slotIdx) {

      // [{
      //   slots: 4,
      //   binary: 1
      // }]

      // <li id="0"> 0 >= 3 ? false
      // <li id="1"> 1 >= 3 ? false
      // <li id="2"> 2 >= 3 ? false
      // <li id="3"> 3 >= 3 ? true => check if is 1 or 0

      // slotSize / binaryLength => 1

      // let validator = this.settings[colIdx].slots / this.settings[colIdx].binary.length

      let binaryLength = this.settings[colIdx].binary.length
      let validator = parseInt(binaryLength) -  this.settings[colIdx].slots

      if (slotIdx >= validator) {
        return this.settings[colIdx].binary[slotIdx + validator] == 1 ? true : false
      } else {
        return false
      }
    }
  }
}
</script>

<style>

</style>