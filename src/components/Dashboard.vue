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
            <users-list v-if="!showEdit" :list="list" @emitdel = "handleDelete" @toggleshowedit="handleShowEdit"/>
            <edit-user v-else @toggleshowedit="handleShowEdit" @emitedit="handleNewData"></edit-user>
        </div>
    </div>
</div>
</template>

<script>
import UsersList from './UsersList.vue';
import CreateUser from './CreateUser.vue';
import EditUser from './EditUser.vue';
import axios from 'axios';
export default {
    components:{
        UsersList,
        CreateUser,
        EditUser
    },
    data(){
        return{
            list:[],
            showEdit:false,
            idtoEdit:null

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
        async handleDelete(data){
            // let index = this.list.findIndex(user => user.email == data);
            const res  = await axios.get(`http://localhost:3000/users`);
            let templist = res.data;
            console.log("temp:",templist);
            let user;
            user = templist.find(user =>{
                if(user.email==data){
                    return user.id;
                }
            })
            console.log("id",user.id);
            await axios.delete(`http://localhost:3000/users/${user.id}`);
            // this.list.splice(index,1);
            try {
                const res = await axios.get(`http://localhost:3000/users`);
                this.list = res.data;
            } catch (error) {
                console.log(error);
            }
        },
        handleShowEdit(id){
            this.showEdit = !this.showEdit;
            if(id != -1) {
                this.idtoEdit = id;
            }
        },
        async handleNewData(data){
            try{
                await axios.patch(`${`http://localhost:3000/users`}/${this.idtoEdit}`,data);
            }catch(err){
                console.log(err);
            }

            try {
                const res = await axios.get(`http://localhost:3000/users`);
                this.list = res.data;
            } catch (error) {
                console.log(error);
            }

            this.showEdit = !this.showEdit;
        }
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