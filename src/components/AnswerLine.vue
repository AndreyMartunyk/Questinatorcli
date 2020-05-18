<template>
<div >
    <button class="box" @click="this.vote" :class="{voted: this.voted}">
        <slot></slot>
    </button>
    
</div>
  
</template>

<script>
export default {
    prop:{
        user:{
            type: Object,
            required: true
        },

    },
    data(){
        return{
            voted: false
        }
    },
    methods:{
        vote(){
            console.log("vote");
            
            this.voted = !this.voted;
        }
    }

}
</script>

<style>

.box{

  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2);
  margin-bottom: 10px;
  
  color: black;
}
.box{
      padding: 10px 20px 10px 20px;
    width: 100%;
    height: 100%;
    background-color: #1abc7e09;
    /* #1abc7e09 */
}
.voted{
    background-color: #0ae490d5;
}
</style>