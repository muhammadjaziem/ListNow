<template>
    <div class="addItem">
        <input type="text" v-model="item.storeItem"/>
        <font-awesome-icon
        icon="plus-square"
        @click="addItem()"
        :class="[item.storeItem  ? 'active' : 'inactive','plus']"
        />
    </div>
</template>

<script>
export default {
    data: function(){
        return {
            item :{
                storeItem: ""
            }
        }
    },methods: {
        addItem(){
            if(this.item.storeItem == ''){
                return;
            }
            axios.post('api/item/store', {
                item: this.item
            })
            .then( responce => {
                if (responce.status == 201){
                    this.item.storeItem = "";
                    this.$emit('listReload');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style  scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}

input {
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding:  5px;
    margin-right: 10px;
    width: 100%;
}
.plus {
    font-size: 20px;
}
.active{
    color: #00CE25;
}
.inactive{
    color: #999999;
}
</style>
