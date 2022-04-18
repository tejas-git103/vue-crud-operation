<template>
<delete-popup @confirmation="handleConfirmation" ref="popup"/>
<div class="users-list">
    <hr class="hr">
    <div class="list-title">
        <span>Name</span>
        <span>Surname</span>
        <span>Email</span>
        <span>Phone Number</span>
        <span>Activate</span>
        <span>Action</span>
    </div>
    <hr class="hr">
    <div v-if="list.length" class="list-container">
        <div v-for="item in list" :key="item.email" class="list-item">
            <span>{{item.name}}</span>
            <span>{{item.surname}}</span>
            <span>{{item.email}}</span>
            <span>{{item.phone}}</span>
            <span>{{item.activate}}</span>
            <span><i class="fa fa-trash-o del-icon" @click="handleDelete(item.email)"></i></span>
        </div>
    </div>
    <div v-else class="empty-list">
        <span >No items</span> 

    </div>
</div>
</template>

<script>
import DeletePopup from './DeletePopup.vue';
export default {
  components: { DeletePopup },
    props:{
        list:[]
    },
    data(){
        return{
            data:null
        }
    },
    methods:{
        handleDelete(data){
            const popup = this.$refs.popup;
            popup.toggleDisplay('block');
            this.data = data;
        },
        handleConfirmation(ans){
            if(ans=='yes') {
                this.$emit('emitdel',this.data);
            }
        }
    }
}
</script>

<style>
.users-list{
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
}
.list-title{
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    font-size: 20px;
}
.empty-list{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 300px;
    font-size: 20px;
    font-weight: bold;
    width: 100%;
    background-color: #EBECF0;
}

.list-container{
    display:flex;
    flex-direction: column;
}
.list-item{
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    background-color: #EBECF0;
    padding: 10px;
    font-size: 20px;
}
.hr{
    color: #EBECF0;
    width: 100%;
}
.del-icon{
    font-size:24px;
    color:red;
}
</style>