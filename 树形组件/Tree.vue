<template>
    <ul class="tree">
        <li class="tree-node"
            v-for="(node,index) in data"
            :key="node[defaultProps.label]"
        >
            <i class="iconfont"
            v-if="node[defaultProps.children]"
                :class="{

                    'icon-down':!showChildren[index],
                    'icon-right':showChildren[index]
                }"
            ></i>
            <span
             class="node-label"
             @click="handleClick(index)"
             >{{ node[defaultProps.label] }}</span>
           <keep-alive>
                <base-tree
                v-if="showChildren[index] && node[defaultProps.children]"
             :data="node[defaultProps.children]"
             
             ></base-tree>
           </keep-alive>
        </li>
    </ul>
</template>

<script>
export default {
    name:'base-tree',
    props:{
        data:{
            type:Array,
            required:true
        },
        defaultProps:{
            type:Object,
            default:()=>({
                label:'label',
                children:'children'
            })
        }
    },
    data(){
        return {
            showChildren:[],
        }
    },

    methods:{
        handleClick(index){
            const flag = !this.showChildren[index];
            // this.showChildren.splice(index,1,flag)
            this.$set(this.showChildren,index,flag)
        }
    }
}


</script>


<style scoped>
@import './font.css';

li{
        list-style:none;
}
.tree-node{
    font-size: 14px;
    cursor: pointer;
}

.tree-node .iconfont{
    color: #c0c4cc;
    font-size: 12px;
    margin-right: 5px;
    vertical-align: middle;
}

.tree-node .node-label{
    font-size: 14px;
    color: #606266;
    /* vertical-align: middle; */
}
</style>