<template>
  <div>
    <h1>Binary to Decimal Converter</h1>
    <input class="mb-3 mr-2" type="text" id="binary" v-model="binaryString">
    <button class="btn btn-outline-danger btn-sm" @click="resetBinaryString"><i class="fas fa-undo"></i></button>
    <p v-if="validBinary">Decimal Value: <strong>{{decimalString}}</strong></p>
    <p v-else class="alert alert-danger">Input content is not a binary</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      binaryString: '',
      validBinary: true,
    }
  },
  watch: {
    binaryString: function(newBin) {
      if (newBin.match(/^[0-1]+$/g) === null || newBin == '') {
        this.validBinary = false
      } else {
        this.validBinary = true
      }
    }
  },
  computed: {
    decimalString: function() {
      let accumulator = 0
      const reverseBin = this.binaryString.split('').map(Number).reverse()
      reverseBin.map((bin, index) => {
        if (bin == 1) {
          accumulator += Math.pow(2,index)
        }
      })
      return accumulator
    }
  },
  methods: {
    resetBinaryString: function() {
      this.binaryString = ''
    }
  },
}
</script>
