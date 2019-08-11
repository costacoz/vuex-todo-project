<template>
    <div @dblclick="showTitleInput($event)">
        <span class="title">{{todo.title}}</span>
        <span class="inputTitle">
            <input ref="titleInput" @blur="inputBlur" v-model="newTitle" id="inputTitle" type="text">
            <button @click="saveTitle($event)" class="save-btn"><i class="far fa-save"></i></button>
        </span>
    </div>
</template>
<script>
    export default {
        name: "Todo",
        data(){
          return {
              newTitle: this.todo.title,
          }
        },
        props: ['todo'],
        methods: {
            showTitleInput(e){
                this.$el.classList.add('inputActive');
                this.$refs.titleInput.focus();
            },
            saveTitle(e){
                e.stopPropagation();
                if (this.newTitle !== '') {
                    this.todo.title = this.newTitle;
                }
                this.$el.classList.remove('inputActive');
            },
            inputBlur(){
                this.$el.classList.remove('inputActive');
            },
        }
    }
</script>
<style scoped>
    .inputTitle{
        display: none;
    }

    .inputActive .title{
        display: none;
    }
    .inputActive .inputTitle{
        display: block;
    }

    .save-btn{
        border: 1px solid white;
        background: #41b882;
        color: white;
    }
</style>