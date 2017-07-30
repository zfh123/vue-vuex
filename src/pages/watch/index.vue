<style>
    .txt{
        text-align: center;
        line-height: 100px;
        font-size: 20px;
        font-weight: 900;
    }
</style>
<template>
    <div class="watch">
        <v-header title="watch">
            <router-link slot="left" to="/watch">watch</router-link>
            <router-link slot="right" to="/map">地图</router-link>
        </v-header>
        <div v-if="ox>5" v-text="ox" class="txt"></div>
        <!--main组件  -->
        <v-main :nav="list"></v-main>
        <v-footer>
            <li>首页</li>
            <li>结算</li>
            <li>我</li>
        </v-footer>
    </div>
</template>
<script>
import { mapActions, mapState } from 'vuex'
export default {
    data() {
        return {
            ox: 0,
            timers :null,
            list:['大主宰','莽荒纪','青云志'],
        }
    },
    computed: {
        _OX: function () {
            if (this.ox > 4) {
                console.log('_OX----'+this.ox);
            }
        }
    },
    watch: {//监控ox值得变化
        ox:{
            handler:function(nowVal,oldVal){
                console.log('nowVal-----'+nowVal);
                console.log('oldVal-----'+oldVal);
                if(nowVal != oldVal){
                    this._init();
                }
            },
            deep: true
        }
    },
     // 离开该页面销毁自调函数
    beforeDestroy() {
        clearTimeout(this.timers)
    },
    created() {

    },
    mounted() {
        this.init();
    },
    methods: {
        _init(){
            console.log('ox调用后的值-------'+this.ox);
        },
        init() {
            var $this = this;
            $this.ox += 1;
            console.log('init------'+$this.ox)
            $this.timers = setTimeout(function(){
                $this.init();
            },2000)
        }
    }
}
</script>
