<template>
    <div id="content">
        <div class="form-container">
            <div class="infobox">
                <div class="title">Submit All</div>
                <button @click="submitAllForm">Submit All Form</button>
            </div>
            <div class="form-box">
                <div class="title">Add new form</div>
                <div>
                    <label for="text-input-amount">Number of text input</label>
                    <input id="text-input-amount" type="number" v-model="textInputNumber"/>
                </div>
                <div>
                    <label for="num-input-amount">Number of number input</label>
                    <input id="num-input-amount" type="number" v-model="numInputNumber"/>
                </div>
                <div>
                    <label for="file-input-amount">Number of file input</label>
                    <input id="file-input-amount" type="number" v-model="fileInputNumber"/>
                </div>
                <button @click="addForm">Add Form</button>
            </div>
            <div class="infobox">
                <div class="title">Remove all forms</div>
                <button @click="removeAllForm">Remove All Forms</button>
            </div>
        </div>

        <!--Form-->
        <div class="form-section">
            <input-form
                v-for="(item, index) in formItems"
                :input-detail="item"
                :key="index"
                ref="formItems"
                @close-form="closeForm($event)"
                @send-form-data="getFormValue($event)"
            ></input-form>
        </div>
        <div class="tab-controller">
            <button class="tab-button" @click.prevent="setActive('grid')" :class="{ active: isActive('grid') }"
                    name="grid">Grid
            </button>
            <button class="tab-button" @click.prevent="setActive('table')" :class="{ active: isActive('table') }"
                    name="table">Table
            </button>
            <button class="tab-button" @click.prevent="setActive('carousel')" :class="{ active: isActive('carousel') }"
                    name="carousel">Carousel
            </button>
            <button class="tab-button" @click.prevent="setActive('chart')" :class="{ active: isActive('chart') }"
                    name="chart">Chart
            </button>
        </div>
        <!--Carousel-->
        <div class="carousel-section tab-panel" v-show="isActive('carousel')">
            <carousel v-if="cards.length > 0" :cards="cards"/>
        </div>
        <!--Data table-->
        <div class="table-section tab-panel" v-show="isActive('table')">
            <data-table :columns="['Name', 'Age', 'Avatar']" :rows="cards"></data-table>
        </div>
        <!--Data grid-->
        <div class="grid-section tab-panel" v-show="isActive('grid')">
            <card
                v-for="(item, index) in cards"
                :key="index"
                :name="item.name"
                :age="item.age"
                :imgName="item.imgName"
                :imgSource="item.imgSource"
            ></card>
        </div>
        <!--Chart-->
        <div class="chart-section tab-panel" v-show="isActive('chart')">
            <chart :chartdata="chartData"/>
        </div>

        <div id="slider">
            <image-slider :preview-images="cards.map(obj => (obj.imgSource))"></image-slider>
        </div>
    </div>
</template>

<script>
import InputForm from "./InputForm";
import DataTable from "@/components/Table";
import Carousel from "@/components/Carousel";
import Card from "@/components/Card";
import Chart from "@/components/Chart";
import ImageSlider from "@/components/ImageSlider";
// import TopBar from "@/components/TopBar";

export default {
    components: {
        ImageSlider,
        // TopBar,
        Chart,
        Carousel,
        DataTable,
        InputForm,
        Card,
    },
    props: {},
    data() {
        return {
            activeItem: 'grid',
            textInputNumber: 0,
            numInputNumber: 0,
            fileInputNumber: 0,
            totalInputForm: 0,
            formItems: [],
            items: [],
            chartData: {
                labels: ['Khanh', 'Phuc', 'VA'],
                datasets: [
                    {
                        label: 'CMC Employees',
                        data: [23, 22, 23]
                    }
                ]
            },
            cards: [
                {
                    name: "Khanh",
                    age: 23,
                    imgSource:
                        "https://i.picsum.photos/id/1048/200/200.jpg?hmac=W94UjOBeBuqxyKnyhht4a81ruXiXHpjQxvdZtNgGyow",
                },
                {
                    name: "Phuc",
                    age: 23,
                    imgSource:
                        "https://i.picsum.photos/id/284/200/200.jpg?hmac=_el2jO-f8UzHfdcTCAXQOD8XX2N6jqVZHwvC23Xm8p8",
                },
                {
                    name: "VA",
                    age: 23,
                    imgSource:
                        "https://i.picsum.photos/id/566/200/200.jpg?hmac=b6_RMcsCCCu5ULi6A3V8vdRrnNhtsnbHdakcGNIQd8s",
                },
            ],
        };
    },
    methods: {
        setActive(menuItem) {
            this.activeItem = menuItem;
        },
        isActive(menuItem) {
            return this.activeItem === menuItem;
        },
        addForm() {
            const text = parseInt(this.textInputNumber);
            const number = parseInt(this.numInputNumber);
            const file = parseInt(this.fileInputNumber);

            if (text > 0 || number > 0 || file > 0) {
                const inputObject = {
                    id: this.totalInputForm,
                    text: text,
                    number: number,
                    file: file,
                };
                this.formItems.push(inputObject);
                this.totalInputForm++;
            }
        },
        closeForm(formId) {
            this.formItems = this.formItems.filter((inputItem) => {
                return inputItem.id !== formId;
            });
        },
        removeAllForm() {
            this.formItems = [];
            this.totalInputForm = 0;
        },

        getFormValue(formData) {
            this.cards.push(formData);
        },
        submitAllForm() {
            for (let i = 0; i < this.formItems.length; i++) {
                this.$refs.formItems[i].getInputData();
            }
        },
    },
};
</script>

<style lang="scss">
.content {
    overflow-y: scroll;
}

.form-container {
    display: flex;
    justify-content: center;
    align-items: center;
}

.teaser {
    position: relative;
    width: 100%;
    max-width: 768px;
    height: 400px;
    margin-bottom: 40px;
    background-image: url("../assets/tired-student-sleeping.jpg");
    background-size: cover;
    background-position: top;
    border-radius: 20px;
    overflow: hidden;

    .teaser-content {
        position: absolute;
        left: 20px;
        bottom: 20px;
        width: 210px;
        height: 50px;
        padding: 0 0 0 20px;
        background-color: #111;
        color: #efefef;
        border-radius: 20px;
        font-size: 2rem;
        cursor: pointer;
    }

    i {
        font-size: 1.6rem;
    }
}

.infobox {
    float: left;
    width: fit-content;
    height: 80px;
    padding: 10px;
    margin: 0 20px 20px 0;
    border-radius: 20px;
    border: 1px solid #ccc;

    .title {
        font-weight: bold;
    }

    .value {
        padding: 10px 0 0 0;
        font-size: 2rem;
    }
}

.form-box {
    position: relative;
    float: left;
    display: block;
    width: fit-content;
    height: fit-content;
    margin: 0 20px 20px 0;
    border-radius: 20px;
    border: 1px solid #ccc;
    clear: both;

    .title {
        text-align: center;
        font-weight: bold;
        margin-bottom: 10px;
    }

    div {
        left: 0;
        top: 0;
        max-width: 200px;
        margin: 10px;
        //height: 100px;
        //display: block;
    }

    button {
        margin: auto;
    }

}

.grid-section {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
}

.tab-panel {
    max-width: 600px;
}

.tab-controller {
    overflow: hidden;
    border: 1px solid #ccc;
    background-color: #f1f1f1;

    .tab-button {
        background-color: inherit;
        float: left;
        border: none;
        outline: none;
        cursor: pointer;
        padding: 14px 16px;
        transition: 0.3s;
        &:hover {
            background-color: #ddd;
        }

        .active {

        }
    }
}
</style>