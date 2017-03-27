<style lang="scss">
    $border_color:#e3e8ee;

    .maskClass{
        position: fixed;
        left: 0;
        top:0;
        right:0;
        bottom:0;
        height:100%;
        background-color: rgba(55,55,55,.6);
        z-index:9999;
    }
    .modal{
        position: fixed;
        overflow: auto;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        -webkit-overflow-scrolling: touch;
        outline: 0;
        z-index:10000;
    }
    .modal_content{
        width: 520px;
        margin: 0 auto;
        position: relative;
        outline: 0;
        top: 100px;
        background-color: #fff;
        border: 0;
        border-radius: 6px;
        background-clip: padding-box;
    }
    .modal_header{
        position: relative;
        border-bottom: 1px solid $border_color;
        padding: 14px 16px;
        line-height: 1;
    }
    .close_icon{
        font-size: 12px;
        position: absolute;
        right: 16px;
        top: 8px;
        overflow: hidden;
        cursor: pointer;
    }
    .header_text{
        display: inline-block;
        width: 100%;
        height: 20px;
        line-height: 20px;
        font-size: 14px;
        color: #464c5b;
        font-weight: 700;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    .modal_body{
        padding: 16px;
        font-size: 12px;
        line-height: 1.5;
    }
    .modal_footer{
        border-top: 1px solid $border_color;
        padding: 12px 18px 12px 18px;
        text-align: right;
    }
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
    .fade-enter-active,.fade-leave-active{
        transition: all .3s ease;
    }
    .fade-enter,.fade-leave-active{
        opacity: 0;
    }

</style>
<template>
    <div>
        <transition name="fade">
            <div class="maskClass" v-show="visible"></div>
        </transition>
        <transition name="fade">
            <div class="modal" v-show="visible">
                <div class="modal_content">
                    <div class="modal_header" v-if="headerFlag">
                        <slot name="header">
                            <a class="close_icon" v-if="closeFlag">x</a>
                            <div class="header_text" v-if="textFlag">{{headerText}}</div>
                        </slot>
                    </div>
                    <div class="modal_body">
                        <slot></slot>
                    </div>
                    <div class="modal_footer">
                        <slot name="footer">
                            <button @click="cancel" class="btn" v-if="cancelFlag">{{cancelText}}</button>
                            <button @click="confirm" class="btn btn_primary" v-if="confirmFlag">{{confirmText}}</button>
                        </slot>

                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>

    export default{
        data(){
            return{
                visible:this.value
            }
        },
        props:{
            value:{
                type:Boolean,
                default:false
            },
            headerFlag:{
                type:Boolean,
                default:true
            },
            closeFlag:{
                type:Boolean,
                default:true
            },
            textFlag:{
                type:Boolean,
                default:true
            },
            headerText:{
                type:String,
                default:'modal'
            },
            cancelFlag:{
                type:Boolean,
                default:true
            },
            confirmFlag:{
                type:Boolean,
                default:true
            },
            cancelText:{
                type:String,
                default:'取消'
            },
            confirmText:{
                type:String,
                default:'确定'
            }
        },
        watch:{
            value(val){
                this.visible=val;
            }
        },
        methods:{
            close(){
                this.visible=false;
                this.$emit('input',false);
            },
            cancel(){
                this.close();
                this.$emit('cancel');
            },
            confirm(){
                this.close();
            }
        },
        components:{
        }
    }
</script>
