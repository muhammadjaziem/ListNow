<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">List Now</h2>
            <add-item-form v-on:listReload="fetchAllList()" />
        </div>
        <list-view
        :items="items"
        v-on:listReload="fetchAllList()"
        />
		
		<list-item
		:items="items"
		v-on:listReload="fetchAllList()" />
    </div>
</template>

<script>
import addItemForm from './addItemForm'
import listView from './listView'
import listItem from './listItem'
export default {
    components: {
        addItemForm,
        listView,
		listItem
    },
    data: function(){
        return {
            items: []
        }
    },
    methods: {
        fetchAllList () {
            axios.get('api/items')
            .then(responce => {
                this.items = responce.data
            })
            .catch( error => {
                console.log(error);
            })
        }
    },
    created(){
        this.fetchAllList();
    }
}
</script>

<style scoped>
.todoListContainer{
    width: 350px;
    margin: auto;
}

.heading{
    background: #e6e6e6;
    padding: 10px;
}

#title{
    text-align:center;
}
</style>
