<style scoped lang='less'>
	.cur{
		text-decoration: line-through;
	}
</style>
<template>
   <li>
       <input type="checkbox" v-model="item.done" @change="changeDone(item.id)" ref="cbox">
       <span v-if="!isShowInput" @dblclick = "showInput" :class="{cur:item.done}">{{item.title}}</span>
       <input type="text" v-if="isShowInput" v-focus @blur="hideInput(item)" v-model="item.title">
       <button @click="del(item.id)">X</button>
   </li>
</template>
<script>
    export default{
        props:['item'],
        data(){
            return{
                isShowInput:false
            }
        },
        methods:{
            del(id){
                this.$store.dispatch("DEL",{
                    id:id
                })
            },
            changeDone(id){
                this.$store.dispatch("CHANGEDONE",{
                    id:id,
                    done:this.$refs.cbox.checked
                })
                console.log(this.$refs.cbox.checked)
            },
            showInput(){
                this.isShowInput = !this.isShowInput;
            },
            hideInput(item){
                this.showInput()
                this.$store.dispatch("CHANGETITLE",item)
            }
        },
        directives:{
            focus:{
                inserted(el){
                    el.focus
                }
            }
        }
    }
</script>