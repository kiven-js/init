<template>
    <div class="date-picker" v-click-outside>
        <div class="picker-input">
            <span class="input-prefix">
                <i class="iconfont icon-date"></i>
            </span>
            <input type="text" 
            
            :value="chooseDate"
            >
        </div>
        <div class="picker-panel" v-if="showPanel">
            <div class="picker-arrow"></div>
            <div class="picker-body">
                <div class="picker-header">
                    <span class="picker-btn iconfont icon-prev-year"></span>
                    <span class="picker-btn iconfont icon-prev-month" ></span>
                    <span class="picker-date">
                        2020年
                    </span>
                    <span class="picker-btn iconfont icon-next-month"></span>
                    <span class="picker-btn iconfont icon-next-year"></span>
                </div>
                <div class="picker-content">
                    <div class="picker-weeks">
                        <div
                         v-for="week in ['日','一','二','三','四','五','六']"
                        :key="week"
                        >
                        {{ week }}
                        </div>
                    </div>
                    <div class="picker-days">
                        <div
                            v-for="date in 42"
                            :key="date"
                        >
                        {{ date }}
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script >
export default {
    directives:{
        bind(el,binding,vnode){
            const vm = vnode.context;
            document.onclick = function(e){
                const dom = e.target;
                const isElSon = el.contains(dom);

                if(isElSon){
                    if(!vm.showPanel){
                        vm.changePanel(true)
                    }
                    
                }else{
                    if(vm.showPanel){
                    vm.changePanel(false);
                    }

                }
            }
        }
    },
    props:{
        date:{
            type:Date,
            default:()=> new Date(),
            
        },
        methods:{
            changePanel(flag){
                this.showPanel = !flag;
            }
        },
        created(){
            console.log('ddd')
        },
        computed:{
            chooseDate(){
                const year = this.date.getFullYear();
                const month = this.date.getMonth();
                const day = this.date.getDate();
                return `${year}-${month+1}-${day}`
            },
        },
        data(){
            return {
                showPanel:false
            }
        }
    }
}
</script>




<style scoped>
@import './font.css';

.date-picker{
    display: inline-block;
}
.picker-input{
    position: relative;

}
.picker-input input{
    height: 40px;
    line-height: 40px;
    padding: 0 30px;
    border: 1px solid #dcdfe6;
    border-radius: 4px;
    outline: none;
    cursor: pointer;
    background-color: #fff;

}

.picker-input .input-prefix{
    position: absolute;
    left: 5px;
    width: 25px;
    text-align: center;
    height: 100%;
    line-height: 40px;
}

.picker-panel{
    position: absolute;
    width: 322px;
    height: 329px;
    /* background-color: red; */
    border: 1px solid #e4e7ed;
    border-radius: 4px;
    margin-top: 5px;
    box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
    background-color: #fff;
}


.picker-panel .picker-arrow{
    position: absolute;
    top: -12px;
    left: 20px;
    width: 0px;
    height: 0px;
    border:6px solid transparent;
    border-bottom-color: #ebeef5;

}

.picker-panel .picker-arrow::after{
    position: absolute;
    content: "";
    display: block;
    width: 0px;
    height: 0px;
    left: -6px;
    top: 2px;
    border: 6px solid transparent;
    border-bottom-color: #fff;
    border-top-width: 0px;
}

.picker-panel .picker-body{

}
.picker-panel .picker-header{
    display: flex;
    align-items: center;
    justify-content: center;
    padding-top: 15px;
    padding-bottom: 10px;

}
.picker-panel .picker-btn{
    margin-right: 5px;
    margin-left: 5px;
    font-size: 20px;
    color: #303133;
    cursor: pointer;
}
.picker-panel .picker-date{
    margin-left: 60px;
    margin-right: 60px;
    font-size: 15px;
    user-select: none;
}

.picker-panel .picker-content{
    padding: 0 10px 10px 10px;
    color: #606266;
    user-select: none;
}

.picker-panel .picker-weeks{
    display: flex;
    justify-content: space-around;
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid #ebeef5;
}

.picker-panel .picker-days{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}
.picker-panel .picker-days div{
    width: 30px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    margin:4px 4px;
    font-size: 12px ;
    cursor: pointer;
}
.picker-panel .picker-days div:hover{
    color: #4091ff;
}
.picker-panel .picker-days div.is-today{
    font-weight: 700;
    color: #409eff;
}

.picker-panel .picker-days div.is-select{
    background-color: #4091ff;
    color: #fff;
    border-radius: 50%;
}

.picker-panel .picker-days div.other-month{
    color: #c0c4cc;
}
</style>