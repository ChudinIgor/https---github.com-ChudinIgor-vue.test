<template>
    <div class="main__todo todo">
        <h2>Список дел</h2>
        <ul   v-if="items.length" class="todo__list list">
            <TodoItem 
                v-for="(item, index) of items"
                :key="item.id"
                v-bind:item="item"
                v-bind:index="index"
                @remove-item="removeItem"
            />
        </ul>
          <h3 v-else>Список пуст</h3>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props:['items'],
    components:{
        TodoItem
    },
    methods:{
        removeItem(id){
            this.$emit('remove-item', id)
        }
    }
}
</script>

<style lang="scss">
    .todo__list{
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>