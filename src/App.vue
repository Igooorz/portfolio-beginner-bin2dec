<template>
  <div class="container form-group">
    <div class="form-row">
      <h1 class="title mt-5">Binary to Decimal Converter</h1>
    </div>
    <div class="form-row mt-3">
      <div class="col-11">
        <input class="mb-3 mr-2 form-control" type="text" id="binary" v-model="binaryString">
      </div>
      <div class="col-1">
        <button class="btn btn-outline-danger btn-sm" @click="resetBinaryString"><i class="fas fa-undo"></i></button>
      </div>
    </div>
    <div class="form-row mt-2">
      <p v-if="validBinary" class="col-12">Decimal Value: <strong>{{decimalString}}</strong></p>
      <p v-else class="alert alert-danger col-12 text-center">Input content is not a binary</p>
    </div>
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
      if (newBin.length !== 0 && newBin.match(/^[0-1]+$/g) === null) {
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

<style scoped>

  .text-center {
    text-align: center
  }

</style>
