<template>
  <div class="header-detail">
    <!-- <button class="btn btn-warning" @click="showLargeModal()">
      {{'modal.large' | translate }}
    </button> -->
    <vuestic-modal :show.sync="show" v-bind:large="true" ref="labDetailAlert" 
      :okClass="'none'" :okText="'modal.confirm' | translate"
      :cancelClass="'none'" :cancelText="'modal.cancel' | translate"
      :headerBgColor="'#3298a8'"
      >
      <div slot="title"><i class="fa fa-lightbulb-o"></i> {{'gogoboard.labdetail_panel.lab' + isLab| translate}}</div>

        <div class="row">
            <div class="col-sm-12 text-center" style="background-color:lightcyan;"><h5>
                <div v-if="isLab==1">
                  <img src="/static/gogo-img/demo-carControl.png" width="150" height="160">
                </div>
                <div v-else-if="isLab==2">
                  <img src="/static/gogo-img/demo-lightControl.png" width="150" height="160">
                </div>
                <div v-else-if="isLab==3">
                  <img src="/static/gogo-img/demo-balancing.png" width="150" height="160">
                </div>
                </h5>
            </div>
                <div class="col-sm-3 text-right" style="background-color:lightcyan;">
                  <div class="btn btn-micro btn-nav col-sm-12 space" @click="chooseToShow('head1')" v-on:click="isActive = 2" v-bind:class="{ 'focus': isActive == 2}">
                    รายละเอียด
                  </div>
                  <div class="row">
                    <div class="col-sm-12 text-right" style="background-color:lightcyan;">
                    <div class="btn btn-micro btn-nav col-sm-12 space" @click="chooseToShow('tool1')" v-on:click="isActive = 2" v-bind:class="{ 'focus': isActive == 2}">
                      อุปกรณ์
                    </div>
                    </div>
                    <div class="col-sm-12 text-right" style="background-color:lightcyan;">
                    <div class="btn btn-micro btn-nav col-sm-12 space" @click="chooseToShow('exercise')" v-on:click="isActive = 2" v-bind:class="{ 'focus': isActive == 2}">
                      แบบฝึกหัด
                    </div>
                    </div>
                  </div>
                </div>
                <div class="col-sm-9 space" style="background-color:lavender;">
                  <h6><p>
                    {{ 'gogoboard.labdetail_panel.lab'+ isLab +'_detail.' + navChoose | translate}}
                  </p></h6>
                </div>
        </div>
        <!--<div class="row" v-else-if="isLab==2">
            <div class="col-sm-3 text-right" style="background-color:lightcyan;"><h5>
                <img src="/static/gogo-img/demo-lightControl.png" width="150" height="160"></h5>
            </div>
            <div class="col-sm-3 text-right space" style="background-color:lightcyan;"><h5><p>{{ 'gogoboard.labdetail_panel.lab2_detail.head' | translate}} :</p></h5></div>
            <div class="col-sm-6 space" style="background-color:lavender;"><h6><p>{{ 'gogoboard.labdetail_panel.lab2_detail.head1' | translate}}</p></h6></div>
            <div class="col-sm-6 text-right space" style="background-color:lightcyan;"><h5><p>{{ 'gogoboard.labdetail_panel.lab2_detail.tool' | translate}} :</p></h5></div>
            <div class="col-sm-6 space" style="background-color:lavender;"><h6><p>{{ 'gogoboard.labdetail_panel.lab2_detail.tool1' | translate}}<br>
            {{ 'gogoboard.labdetail_panel.lab2_detail.tool2' | translate}}</p></h6></div>
        </div>
        <div class="row" v-else-if="isLab==3">
            <div class="col-sm-3 text-right" style="background-color:lightcyan;"><h5>
                <img src="/static/gogo-img/demo-balancing.png" width="150" height="160"></h5>
            </div>
            <div class="col-sm-3 text-right space" style="background-color:lightcyan;"><h5><p>{{ 'gogoboard.labdetail_panel.lab3_detail.head' | translate}} :</p></h5></div>
            <div class="col-sm-6 space" style="background-color:lavender;"><h6><p>{{ 'gogoboard.labdetail_panel.lab3_detail.head1' | translate}}</p></h6></div>
            <div class="col-sm-6 text-right space" style="background-color:lightcyan;"><h5><p>{{ 'gogoboard.labdetail_panel.lab3_detail.tool' | translate}} :</p></h5></div>
            <div class="col-sm-6 space" style="background-color:lavender;"><h6><p>{{ 'gogoboard.labdetail_panel.lab3_detail.tool1' | translate}}<br>
            {{ 'gogoboard.labdetail_panel.lab3_detail.tool2' | translate}}</p></h6></div>
        </div>-->

      <hr width="50%">
      
    </vuestic-modal>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import notification from 'services/notification'
import { SidebarMenu } from 'vue-sidebar-menu'

const releaseUrl =
  'https://api.github.com/repos/gogoremote/remotelab-plugin/releases/latest'
const macUrl =
  'https://github.com/LILCMU/gogo-plugin/releases/download/v0.9.4/gogo-plugin-0.9.4.dmg'
const winUrl =
  'https://github.com/gogoremote/remotelab-plugin/releases/download/1.0.0/GoGo.Plugin-Remote.Lab.msi'

export default {
  name: 'header-detail',
  components: {
      SidebarMenu
  },
  props: {
    isOpen: {
      type: Boolean,
      required: false
    },
    isLab: {
      required: false
    }
  },
  data () {
    return {
      show: false,
      macUrl: macUrl,
      winUrl: winUrl,
      navChoose: 'head1'
    }
  },
  watch: {
    isOpen: function (val) {
        console.log(val+":"+this.isLab)
        this.showLargeModal()
    }
  },
  mounted () {
    // this.fetchDownloadUrl()
  },
  methods: {
    showLargeModal () {
      this.navChoose = 'head1'
      this.$refs.labDetailAlert.open()
    },
    hideLargeModal () {
      if (this.$refs.labDetailAlert) {
        this.$refs.labDetailAlert.clickMask()
      }
    },
    chooseToShow (choose) {
      this.navChoose = choose
    }
  },
  computed: {
  }
}
</script>

<style lang="scss" scoped>

.btn-nav {
  border-radius: 2px;
  background-color: lavender;
}

.spacehead {
  margin-top: 20px;
  margin-bottom: 60px;
}

.space {
  padding-top: 20px;
  padding-bottom: 20px;
}

.block {
  padding-left: 30px;
  padding-right: 30px;
  color: $brand-info;
}

.mac a {
  color: $cc-pink;
}

.windows a {
  color: $brand-info;
}
</style>

<style lang="scss">
.vuestic-modal .modal-content {
  border-radius: 12px;
  /*.modal-body {
    // height: calc(100vh - 55px);
    height: calc(100vh - 100px);
    padding: 0px;

    iframe {
      // height: calc(100vh - 55px);
      height: calc(100vh - 100px);
    }
  }*/
}
</style>
