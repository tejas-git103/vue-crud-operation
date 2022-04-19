<template>
<CreateUser ref="createUserRef" @emitadd="handleAdd" />
<div class="dashboard">
    <div class="side-bar">
        <div class="side-bar-list">
            <span>Dashboard</span>
            <span>Users</span>
        </div>
        
    </div>
    <div class="main-section">
        <span class="dasboard-title">Dashboard</span>
        <hr class="hr"/>
        <div class="users-container">
            <div class="users-title">
                <span>Users</span>
                <button class="create-user-btn" @click="displayPopup">Create User</button>
            </div>
            <users-list :list="list" @emitdel = "handleDelete"/>
        </div>
    </div>
</div>
</template>

<script>
import UsersList from './UsersList.vue';
import CreateUser from './CreateUser.vue';
import axios from 'axios';
export default {
    components:{
        UsersList,
        CreateUser
    },
    data(){
        return{
            list:[]
        }
    },
    methods:{
        displayPopup(){
            const createUserRef = this.$refs.createUserRef;
            createUserRef.toggleDisplay('block');
        },
        async handleAdd(data){
            console.log("in add");
            // const obj = JSON.stringify(data);
            // try{

            // } catch(){

            // }
            const res = await axios.post(`http://localhost:3000/users`, {
                name:data.name,
                surname:data.surname,
                email:data.email,
                phone:data.phone,
                activate:data.activate
            },{headers:{"Content-Type" : "application/json"}});
            console.log(res);
            this.list = [...this.list,res.data];
        },
        handleDelete(data){
            let index = this.list.findIndex(user => user.email == data);
            axios.delete(`http://localhost:3000/users/${index}`);
            this.list.splice(index,1);
        },
    },
    async created(){
        try {
            const res = await axios.get(`http://localhost:3000/users`);
            this.list = res.data;
        } catch (error) {
            console.log(error);
        }
    },
}
</script>

<style>
.dashboard{
    display: flex;
    flex-direction: row;
    width: 100%;
    height:600px;
    /* min-height: 100%; */
    gap: 20px;
}
.side-bar{
    width: 25%;
    background-color: #61718a;
    height: 100%;
    padding: 20px;
}
.main-section{
    width: 75%;
    background-color: #EBECF0;
    padding: 20px;
}
.dasboard-title{
    font-size: 24px;
    /* font-weight: bold; */
    color: #bebebe;
}
.hr{
 color:#bebebe
}
.users-container{
    display: flex;
    flex-direction: column;
    background-color: white;
    margin-top: 20px;
    /* width: 100%; */
    border:#bebebe 1px solid;
    border-radius: 5px;
}
.users-title{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: baseline;
    padding: 10px;
}
.create-user-btn{
    color: white;
    background-color: steelblue;
    font-size: 14px;
    padding: 10px 15px 10px 15px;
    border: none;
    border-radius: 5px;
}
.side-bar-list{
    display: flex;
    flex-direction: column;
    row-gap: 20px;
    font-size: 20px;
}
</style>