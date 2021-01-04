<template>
    <div class="todoListContainer"> 
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form 
                v-on:reloadList="getListItem()"
            />
        </div>
        <list-view 
            :items ="items"
            v-on:reloadList="getListItem()"
        />
    </div>
</template>

<script>
import addItemForm from "./addItemForm"
import listItem from './listItem'
import listView from './listView'
import ListView from './listView.vue'

    export default{
        components : {
            addItemForm,
            listView
        },
        data : function(){
            return {
                items:[]
            }
        },
        methods : {
            getListItem (){
                axios.get('/api/items')
                .then( response => {
                    this.items = response.data
                })
                .catch( err => {
                    console.log(err)
                })
            }
        },
        created(){
            this.getListItem()
        }
    }
</script>

<style scoped>
    .todoListContainer {
        width: 350px;
        margin: auto;
    }
    .heading{
        background: #e6e6e6;
        padding: 10px;
    }
    #title{
        text-align: center;
    }
</style>