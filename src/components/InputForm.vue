<!--Input example: [{text: 2}, {number: 3}, {image: 2}]-->

<template>
    <div class="card" :id="'input-card-' + inputDetail.id">
        <span class="close" @click="$emit('close-form', inputDetail.id)">x</span>

        <div v-if="inputDetail.text">
            <input v-for="(item, index) in inputDetail.text" :key="index" type="text" placeholder="Text"/>
        </div>
        <div v-if="inputDetail.number">
            <input v-for="(item, index) in inputDetail.number" :key="index" type="number" placeholder="Number"/>
        </div>
        <div v-if="inputDetail.file">
            <input v-for="(item, index) in inputDetail.file" :key="index" type="file" placeholder="File"/>
        </div>

        <button class="clear-input-btn" @click="clearAllInput">Reset</button>
    </div>
</template>

<script>
    export default {
        name: 'InputForm',
        props: {
            inputDetail: {
                type: Object,
                default: ()=> {
                    return {
                        id: 0, text: 2, number: 2, file: 2
                    }
                },
                validator: function (value) {
                    return ['id', 'text', 'number', 'file'].every(key => value[key] !== undefined)
                }
            }
        },
        methods: {
            showImagePreview: () => {
                console.log("Preview Image");
            },
            validateInput: () => {
                console.log("Validate Input");
            },
            clearAllInput: () => {
                console.log("All inputs cleared");
            }
        }
        // mounted() {
        //     console.log("Hello");
        // }
    }
</script>

<style lang="scss" scoped>
    .card {
        margin: 5px;
        border: 1px solid #ccc;
        float: left;
        max-width: 200px;
        text-align: center;
        position: relative;

        input {
            max-width: 90%;
            margin: 5px;
        }

        .close {
            float: right;
            display: inline-block;
            padding: 2px 5px;
            color: #fff;
        }

        .close:hover {
            cursor: pointer;
            float: right;
            display: inline-block;
            padding: 2px 5px;
            background: #ccc;
            color: #fff;
        }

        .clear-input-btn {
            cursor: pointer;
            float: right;
            display: inline-block;
            padding: 2px 5px;
            background: transparent;
            color: #0099CC;
        }
    }

    .card:hover {
        border: 1px solid #777;

        .close {
            display: block;
        }
    }
</style>