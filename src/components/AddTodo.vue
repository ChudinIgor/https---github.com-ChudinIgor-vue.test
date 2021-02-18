<template>
 <div>
    <h2>Добавить новый элемент</h2>
    <form @submit.prevent="onSubmit">
        <p>
            <label for="title">Название:</label>
            <input type="text" id="title" autocomplete="off" v-model="title">
        </p>
        <p>
            <label for="description">Описание:</label>
            <input type="text" id="description" autocomplete="off" v-model="description">
        </p>
        <div class="submit">
            <button type="submit">Create</button>
        </div>
    </form>
    <h2>Удалить все завершенные</h2>
    <div>
        <button class="control__button" @click="$emit('remove-items')">Удалить</button>
    </div>
    <h2>Фильтрация по алфавиту</h2>
    <div>
        <button class="control__button" @click="$emit('filter-items')">Отсортировать</button>
    </div>
 </div>
</template>

<script>
export default {
    data() {
        return {
            title:'',
            description:'',
            search:''
        }
    },
    methods: {
        onSubmit() {
            if(this.title.trim()){
                const newItem = {
                    id: Date.now(),
                    title: this.title,
                    completed:false,
                    description: this.description
                }
                this.$emit('add-item', newItem)
                this.title = ''
                this.description = ''
            }
           
        },  
    },
}
</script>

<style lang="scss">
.control__button {
  background: #00a2d3;
  color: white;
  border: 0;
  outline: none;
  padding: 2.5px 10px;
  border-radius: 5px;
  font-size: .7rem;
  text-align: center;
  width: 50%;
  margin-left: 50%;
  cursor: pointer;
  box-shadow: 0 0 4px 2px rgba(0, 0, 0, .3);
}
.control__input {
    width: 100%;
    color: #bbb;
    text-shadow: 1px 1px 1px black;
    background: rgba(0, 0, 0, 0.16);
    border: 0;
    border-radius: 5px;
    box-shadow: inset 0 1px 4px rgba(0, 0, 0, .3), 0 1px rgba(255, 255, 255, .2);
}
.control  form {
    position: relative;
    padding-right: 32px;
    font-weight: 300;
    color: #a8a7a8;
    width: 100%;

    p {
        margin: 5px 0 5px 0;
        display: flex;
        justify-content: space-between;
        font-size:.5rem;
        width: 90%;
    }

    label {
        flex: 1 0 20%;
        line-height: 20px;
        font-weight: 100;
        letter-spacing: 1px;
    }
    input {
        flex: 3 0 80%;
        height: 20px;
        color: #bbb;
        text-shadow: 1px 1px 1px black;
        background: rgba(0, 0, 0, 0.16);
        border: 0;
        border-radius: 5px;
        box-shadow: inset 0 1px 4px rgba(0, 0, 0, .3), 0 1px rgba(255, 255, 255, .2);
    }
    .submit {
        position: absolute;
        top: -7px;
        right: 24px;
        width: 48px;
        height: 48px;
        padding: 8px;
        border-radius: 32px;
        &:before {
            top: 28px;
            left: -4px;
            width: 4px;
            height: 10px;     
        }
        &:after {
            top: -4px;
            bottom: -4px;
            right: -4px;
            width: 36px;    
        }
        & > button {
            position: relative;
            z-index: 2;
            width: 48px;
            height: 48px;
            padding: 0 0 48px;
            text-indent: 120%;
            white-space: nowrap;
            overflow: hidden;
            background: none;
            border: 0;
            border-radius: 24px;
            cursor: pointer;
          
            &:before {
                content: '';
                position: absolute;
                top: 2.5px;
                bottom: 2.5px;
                left: 2.5px;
                right: 2.5px;
                background: #00a2d3;
                border-radius: 24px;
                box-shadow: 0 0 5px  rgba(255, 255, 255, .3);
                  transition: 0.4s;
            }
            &:after {
                    content: '';
                    position: absolute;
                    top: 14px;
                    left: 14px;
                    width: 20px;
                    height: 20px;
                    background: white;
                    border-radius: 50%;
                    box-shadow: 0 0 3px 1px rgba(0, 0, 0, .3);
                      transition: 0.8s;

            }
            &:hover:before {
                 background: white;
            }
            &:hover:after {
                background: #00a2d3;
            }
            &:focus {
                outline: none;
            }
        }
    }
}
</style>