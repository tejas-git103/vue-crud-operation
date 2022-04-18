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
            <users-list :list="list"/>
        </div>
    </div>
</div>
</template>

<script>
import UsersList from './UsersList.vue';
import CreateUser from './CreateUser.vue';

export default {
    components:{
        UsersList,
        CreateUser
    },
    data(){
        return{
            list:[
            {
                name:'tejas',
                surname:'apte',
                email:'tejas@abc',
                phone:123456789,
                activate:true,
                action:'none'
            }]
        }
    },
    methods:{
        displayPopup(){
            const createUserRef = this.$refs.createUserRef;
            createUserRef.toggleDisplay('block');
        },
        handleAdd(data){
            this.list.push(data);
        }
    },
    mounted(){
        console.log("mounted")
    },
    updated(){
        console.log('updated');
    }

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