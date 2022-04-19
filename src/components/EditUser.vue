<template>
  <div class="edit-user">
      <div>
          New Name: <input type="text" v-model="name">
      </div>
      <div>
          New surname: <input type="text" v-model="sname">
      </div>
      <div class="btn-container">
          <button class="btn" @click="edit">Edit</button>
          <button class="btn" @click="cancel">Cancel</button>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            name:'',
            sname:""
        }
    },
    methods:{
        cancel(){
            this.$emit('toggleshowedit',-1);
        },
        edit(){
            this.$emit('emitedit',{name:this.name,surname:this.sname})
        }
    }
}
</script>

<style>
.edit-user{
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
}
.btn-container{
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-self: stretch;
}
.btn{
    color: white;
    background-color: steelblue;
    font-size: 14px;
    padding: 10px 15px 10px 15px;
    border: none;
    border-radius: 5px;
}
</style>