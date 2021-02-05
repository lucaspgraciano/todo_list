<template>
    <div class="new-task">
        <input v-model="name" @keydown.enter="add" type="text" class="form-element" placeholder="">
        <button @click="add" class="form-element">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', { name: this.name })
            this.name = ''
        }
    }
}
</script>

<style>
    .new-task{
        margin: 5px;
    }
    .form-element{
        outline: none;
        font-size: 1.5rem;
        border: 1px solid #fff;
        padding: 5px;
    }
    input.form-element {
        animation: searchBar 2s;
        width: 450px
    }
    button.form-element{
        width: 40px;
        background-color: #fff;
    }
    button.form-element:hover{
        animation: searchButton 1.8s;
        transform: scale(1.1);
    }
    button.form-element:active{
        transform: scale(0.8);
        background-color: #8d99ae;
        border: none;
        color: #fff;
    }
    @keyframes searchBar {
        0%{ width: 0;}
        100%{width: 450px;}
    }
    @keyframes searchButton {
        50%{transform: scale(1.1); background-color: #8d99aeaa ; color: #fff;}
    }

</style>