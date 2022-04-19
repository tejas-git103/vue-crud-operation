<template>
  <div class="delete-popup" ref="delpopup">
      <div class="confirmation">Are you sure you want to delete ?</div>
      <div class="btns">
          <button class="btn" @click="handleYes"> Yes</button>
          <button class="btn" @click="handleNo"> No</button>
      </div>
  </div>
</template>

<script>
export default {
    methods:{
        handleYes(){
            this.toggleDisplay('none');
            this.$emit('confirmation','yes');
        },
        handleNo(){
            this.toggleDisplay('none');
            this.$emit('confirmation','no');
        },
        toggleDisplay(display){
            const delpopup = this.$refs.delpopup;
            delpopup.style.display = display;
        }
    }
}
</script>

<style>
.delete-popup{
    position: absolute;
    width: 40%;
    /* height: 400px; */
    left: 30%;
    top:10%;
    background-color: white;
    border:2px solid black;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    display: none;
}
.btns {
    display: flex;
    flex-direction: row;
    margin-top: 20px;
    justify-content: space-evenly;
}
.btn{
    color: white;
    background-color: steelblue;
    font-size: 14px;
    padding: 10px 15px 10px 15px;
    border: none;
    border-radius: 5px;
}
.confirmation{
    font-size: 20px;
    font-weight: bold;
    color: red;
}
</style>