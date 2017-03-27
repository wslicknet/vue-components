<template>
  <div id="app">
      <button class="btn" @click="showModal">modal弹框</button>
      <modal v-model="modalFlag"
      >
          <p>这是正文，slot插入</p>
          <p>这是正文，slot插入</p>
          <p>这是正文，slot插入</p>
      </modal>
  </div>
</template>

<script>
import modal from './components/modal/modal'
export default {
    name: 'app',
    data(){
        return {
           modalFlag:false,
        }
    },
    methods:{
        showModal(){
            this.modalFlag=true;
        }
    },
    components:{
        modal
    }
}
</script>

<style lang="scss">
    .btn{
        display: inline-block;
        margin-bottom: 0;
        font-weight: 400;
        text-align: center;
        vertical-align: middle;
        -ms-touch-action: manipulation;
        touch-action: manipulation;
        cursor: pointer;
        background-image: none;
        border: 1px solid transparent;
        white-space: nowrap;
        line-height: 1.5;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        padding: 6px 15px;
        font-size: 12px;
        border-radius: 4px;
        transform: translate3d(0,0,0);
        transition: color .2s linear,background-color .2s linear,border .2s linear;
        color: #657180;
        background-color: #f7f7f7;
        border-color: #d7dde4;
    }
    .btn_primary{
        color: #fff;
        background-color: #39f;
        border-color: #39f;
    }
</style>
