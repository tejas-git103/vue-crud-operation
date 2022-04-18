<template>
  <div class="create-user-container" ref="container">
      <div class="create-user-elements">
          <span class="title">Create User</span>
        <div class="input-element">
            Name : <input class="input" type="text" v-model="name" value>
            <div v-if="nameErr" class="error">Please Enter Valid Name</div>
        </div>
        <div class="input-element">
            Surname : <input  class="input" type="text" v-model="surname">
            <div v-if="surnameErr" class="error">Please Enter Valid Surname</div>
        </div>
        <div class="input-element">
            Email : <input class="input" type="email" v-model="email" >
            <div v-if="emailErr" class="error">Please Enter Valid mail</div>
        </div>
        <div class="input-element">
            Phone : <input class="input" type="tel" v-model="phone" placeholder="">
            <div v-if="phoneErr" class="error">Please Enter Valid number</div>
        </div>
        <div class="input-element">
            Action : <input class="input" type="text" v-model="action">
            <div v-if="actionErr" class="error">Please Enter Valid Action</div>
        </div>
        <div class="btn-container">
            <button  class="btn" @click="handleAdd">Add</button>
            <button class="btn" @click="handleCancel">Cancel</button>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            name: "",
            surname: "",
            email: "",
            phone:null,
            action: "",
            nameErr:false,
            surnameErr:false,
            phoneErr:false,
            emailErr:false,
            actionErr:false
        }
    },
    methods:{
        handleCancel(){
            this.toggleDisplay('none');
        },
        toggleDisplay(display){
            const container = this.$refs.container;
            container.style.display = display;
            console.log('in toggle')
        },
        handleAdd(){
            if (this.name == "" || !/[a-zA-z]/.test(this.name)){
                this.nameErr = true;
            } else {
                this.nameErr = false;
            }

            if (this.surname == "" || !/[a-zA-z]/.test(this.surname)){
                this.surnameErr = true;
            } else {
                this.surnameErr = false;
            }

            if (!/[0-9]{10}/.test(this.phone)){
                this.phoneErr = true;
            } else {
                this.phoneErr = false;
            }

            if (this.action == "" || !/[a-zA-z]/.test(this.action)){
                this.actionErr = true;
            } else {
                this.actionErr = false;
            }
            const reg = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (reg.test(this.email)) {
                this.emailErr = false;
            } else {
                this.emailErr = true;
            }
            if (!this.emailErr && !this.nameErr && !this.surnameErr && !this.phoneErr && !this.actionErr) {
                this.toggleDisplay('none');
                this.$emit('emitadd',{
                    name:this.name,
                    surname:this.surname,
                    email:this.email,
                    phone:this.phone,
                    activate:true,
                    action:this.action
                });
            }
            
        }
    }
}
</script>

<style>
.create-user-container{
    position: absolute;
    width: 50%;
    /* height: 400px; */
    left: 25%;
    top:10%;
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    border:2px solid black;
    display: none;
    
}
.create-user-elements{
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    gap: 20px;
    padding: 20px;
}
.title{
    align-self: center;
    font-size: 24px;
    font-weight: bold;
    color: #bebebe;
}
.input-element{
    font-size: 20px;
    color: #bebebe;
}
.input{
    font-size: 20px;
    color: #bebebe;
    width: 60%;
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
.error{
    color:red;
    font-size: 10px;
}
</style>