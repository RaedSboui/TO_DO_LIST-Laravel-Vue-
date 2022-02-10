<template>
    <div class="container">
        <div class="header">
            <h2 id="title">To-Do List</h2>
            <add-item-form @reloadList='getList()'/>
        </div>
        <list 
            :items='items'
            @reloadList='getList()'
        />
    </div>
</template>

<script>
import addItemForm from './addItemForm'
import list from './list'

export default {
    name: 'App',
    components: {
        addItemForm,
        list,
    },
    data: () => {
        return {
            items: []
        } 
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then(response => this.items = response.data)
            .catch(error => console.log(error))
        }
    },
    created() {
        this.getList()
    }
}
</script>

<style scoped>

.container{
    width: 350px;
    margin: auto;
}
.header{
    background: #e6e6e6;
    padding: 10px;
}
#title{
    text-align: center;
}
</style>