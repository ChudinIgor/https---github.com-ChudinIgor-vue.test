<template>
    <li class="list__item">
        <input type="checkbox" v-on:change="item.completed= !item.completed">
        <span v-bind:class="{list__item__comlete:item.completed}">
            <strong>{{index + 1}}</strong>
            <span>{{item.title}}</span>
            <!-- Todo Переделать описание к задаче -->
            <p>{{item.description}}</p>
        </span>
        <button class="list__item__rm" @click="$emit('remove-item', item.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props:{
        item:{
            type:Object,
            requered: true,
        },
        index: Number
    },
 
}
</script>

<style lang="scss" scoped>
    .list__item{
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem;
        margin-bottom: 1rem;
        font-size:.9rem;
        &>input {
            flex: 1 1 25px;
            margin: 0;
        }
        &>span {
            flex: 7 1 300px;
        }
        &>button {
             flex: 1 1 20px;
        }
        &:nth-child(2n){
            background: #ccc;
            color: black;
             .list__item__rm{
                  color:black;
                  box-shadow: 0 0 4px rgba($color: black, $alpha: .7);
             }
        }
         .list__item__rm {
            max-width: 20px;
            height: 20px;
            background: #00a2d3; 
            box-shadow: 0 0 4px rgba($color: white, $alpha: .7);
            color:white;
            border-radius: 50%;
            font-weight: bold;
            border: none;
            cursor: pointer;
            transition: .5s;
            &:hover { 
                background:rgb(240, 26, 26);
            }
            &:focus {
                outline:none;
            }
        }
        .list__item__comlete {
            text-decoration: line-through;
        }
    }
   
</style>