<template>
  <div class="lab-detail-panel">
    <div class="row justify-content-center">
        <span><h3>{{ 'gogoboard.labdetail_panel.' + 'lab' + parentData | translate }}</h3></span><br><br>

        <!--<div class="btn btn-micro btn-primary" @click="switchLab(1)" v-on:click="isActive = 1" v-bind:class="{ 'focus': isActive == 1}">
          {{'gogoboard.lab_panel.lab1' | translate}}
        </div>-->
        <!--<div v-if="lab == 0">
          A
        </div>-->

        <div :form="form"></div>

        <div class="row">
            <div class="col-sm-12">
                <fieldset>
                <div class="form-group form-group-w-btn">
                    <div class="input-group">
                    <input id="input-w-btn"  required v-model="userName"/>
                    <label class="control-label" for="input-w-btn">{{'gogoboard.labdetail_panel.name'
                        | translate}}</label><i class="bar"></i>
                    </div>
                    <div class="btn btn-micro btn-lab2 btn-font" v-on:click="enterUsername()" >
                    {{'gogoboard.labdetail_panel.enter' | translate}}
                    </div>
                </div>
                </fieldset>
            </div>
        </div>

        <div class="row">
            <div class="col-sm-12 text-center">
                {{'gogoboard.labdetail_panel.see_detail' | translate}} :
                <div class="btn btn-micro btn-lab"  @click="etr()" v-on:click="callDetail()">
                    {{'gogoboard.labdetail_panel.detail' | translate}}
                </div>
            </div>
        </div>

    </div>
    <header-detail :isOpen="openDetail" :isLab="lab"></header-detail>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'
import vueSlider from 'vue-slider-component'
import VueSlideBar from 'vue-slide-bar'
import { setInterval } from 'timers'
import LabDisplayPanel from './LabDisplayPanel.vue'
import HeaderDetail from './HeaderDetail'

//var lab_selected = 99
//var lab

export default {
  name: 'lab-detail-panel',
  props: ['parentData'],
  components: {
    vueSlider,
    VueSlideBar,
    LabDisplayPanel,
    HeaderDetail
  },
  data() {
    return {
      message: 'You loaded this page on ',
      lab: 1,
      userName : '',
      form: {
        name: ''
      },
      openDetail: false,
      //lab: localStorage.getItem("lab_selected")

    }
  },
  methods: {
    etr () {
      /*if(this.parentData == 1){
        this.openDetail = !this.openDetail
      }else if(this.parentData == 2){
        this.$swalDetail2({})
      }else if(this.parentData == 3){
        this.$swalDetail3({})
      }else{
        this.$swalDetail1({})
      }*/
      this.openDetail = !this.openDetail
    },
    enterUsername (event) {
      this.$emit('detailToStatus', this.userName)
    },
    callDetail (event) {
      this.lab = this.parentData
      this.$emit('detailToStatuss', this.parentData)
      console.log(this.parentData)
    }
  },
  mounted() {

  },
  updated() {    

  },
  computed: {
    labselected () {
      return 99
    }
  }
}
</script>

<style lang="scss" scoped>

.btn-lab {
  background-color: #fee042;
}
.btn-lab2 {
  background-color: #90d948;
}
.btn-font {
  color: #ffffff;
}


</style>
