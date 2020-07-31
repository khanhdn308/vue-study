<template>
    <div class="card" :id="'input-card-' + inputDetail.id">
        <span class="close" @click="$emit('close-form', inputDetail.id)">x</span>

        <div v-if="inputDetail.text">
            <input v-for="(item, index) in inputDetail.text" :key="index" type="text" placeholder="Text" v-model="textValues[index]"/>
        </div>
        <div v-if="inputDetail.number">
            <input v-for="(item, index) in inputDetail.number" :key="index" type="number" placeholder="Number" v-model="numberValues[index]"/>
        </div>
        <div v-if="inputDetail.file">
            <input v-for="(item, index) in inputDetail.file" :key="index" type="file" placeholder="File"
                   @change="showImagePreview($event)" :ref="'input-file-' + index"/>
            <img v-if="inputDetail.file === 1" :src="previewImage" alt="preview-img" class="preview-image" ref="preview-image">
            <image-slider v-if="inputDetail.file > 1" :preview-images="fileValues"></image-slider>
        </div>

        <button class="clear-input-btn" @click="clearAllInput">Reset</button>
    </div>
</template>

<script>
import ImageSlider from "@/components/ImageSlider";

export default {
    name: 'InputForm',
    components: {
      ImageSlider
    },
    props: {
        inputDetail: {
            type: Object,
            default () {
                return {
                    id: 0, text: 2, number: 2, file: 2
                }
            },
            validator (value) {
                return ['id', 'text', 'number', 'file'].every(key => value[key] !== undefined)
            }
        }
    },
    methods: {
        showImagePreview (event) {
            if (event) {
                let reader = new FileReader();
                reader.readAsDataURL(event.target.files[0]);
                reader.onload = () => {
                    this.previewImage = reader.result;
                    this.fileValues.push(reader.result);
                };
                reader.onerror = function (error) {
                    console.log('Error: ', error);
                };
            }
        },
        getInputData () {
            console.log("Validate Input");
            this.$emit("send-form-data", this.validateFormData());
        },
        clearAllInput () {
            this.textValues = [];
            this.numberValues = [];
            this.fileValues = [];
            this.previewImage = '';
            if (this.inputDetail.file > 0){
                for (let i=0; i < this.inputDetail.file; i++){
                    this.$refs[`input-file-${0}`][0].value = "";
                }
            }
            console.log("All inputs cleared");
        },
        validateFormData () {
            let textInputsvalue = '';
            for (let i=0; i < this.textValues.length; i++){
                textInputsvalue += this.textValues[i] + " ";
            }
            let numberInputsvalue = 0;
            for (let i=0; i < this.numberValues.length; i++){
                numberInputsvalue += parseInt(this.numberValues[i]);
            }

            if (this.inputDetail.text > 0 && textInputsvalue.trim() === ""){
                console.log("Validation error");
            }
            if (this.inputDetail.number > 0 && parseInt(numberInputsvalue) === 0){
                console.log("Validation error");
            }

            return {name: textInputsvalue, age: numberInputsvalue, imgSource: this.fileValues[0]};
        }
    },
    data() {
        return {
            previewImage: '',
            textValues: [],
            numberValues: [],
            fileValues: []
        }
    }
    // mounted() {
    //     console.log("Hello");
    // }
}
</script>

<style lang="scss" scoped>
.card {
    display: inline-block;
    margin: 5px;
    border: 1px solid #ccc;
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

    .preview-image {
        max-width: 180px;
        max-height: 180px;
    }
}

.card:hover {
    border: 1px solid #777;

    .close {
        display: block;
    }
}
</style>