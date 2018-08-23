<template>
  <v-container>
    <v-layout row wrap v-bind:class="[disabled ? 'disabled' : '']">
      <v-flex md4 printer-model v-for="(item, i) in objectives" :key="i" @click="select(i, item)" v-bind:class="[(loading && (i == selected)) ? 'selected' : '']">
        <v-card>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ item.name }}<v-progress-circular v-if="loading && (i == selected)" indeterminate></v-progress-circular></h3>
            </div>
            <div class="image-container">
              <img :src="item.image"/>
            </div>
          </v-card-title>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'PrinterOrder',
  props: ['loading', 'disabled'],
  data () {
    return {
      objectives: [{
        name: 'Shaman',
        image: '/static/shaman.png',
        objective: 'QmRp9ymfsLBLVntVtXdT1BAdrMCdfNBfzSeintGvtFiPfN'
      }, {
        name: 'Phone holder',
        image: '/static/holder.png',
        objective: 'QmQvSdkVkGmkXvow4aBAGq3gdhgFZSYwzpMdu4QU3YetMG'
      }, {
        name: 'Ethereum',
        image: '/static/ethereum.png',
        objective: 'QmexZKkmKQkmEysCqMkWBwqb1hkQfdwtZzbZHTiauWmSsY'
      }],
      selected: null
    }
  },
  methods: {
    select (index, item) {
      if (!this.disabled) {
        this.selected = index
        this.$emit('select', item.objective)
      }
    }
  }
}
</script>

<style>
  .disabled {
    opacity: 0.5;
  }
  .printer-model:hover .v-card, .printer-model.selected .v-card {
    background: #dcdcdc!important;
  }
  .disabled .printer-model:not(.selected):hover .v-card {
    background: none!important;
  }
  .image-container {
    width: 100%;
    height: 180px;
    overflow: hidden;
  }
  .image-container img {
    width: 100%;
    min-height: 180px;
  }
  .v-progress-circular {
    height: 16px !important;
    margin-top: -5px;
  }
</style>
