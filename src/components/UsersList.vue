<template>
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
        <div v-for="item in list" :key="item.email" class="list-item" @click="handlelistclick(item.email)">
            <span>{{item.name}}</span>
            <span>{{item.surname}}</span>
            <span>{{item.email}}</span>
            <span>{{item.phone}}</span>
            <span>{{item.activate}}</span>
            <span>{{item.action}}</span>
        </div>
    </div>
    <div v-else class="empty-list">
        <span >No items</span> 

    </div>
</div>
</template>

<script>
export default {
    props:{
        list:[]
    },
    methods:{
        handlelistclick(ev){
            console.log(ev);
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
</style>