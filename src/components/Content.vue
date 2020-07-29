<template>
  <div id="content">
    <!--        <div class="teaser">-->
    <!--            <div class="teaser-content">-->
    <!--                Read Article-->
    <!--                <em class="fas fa-chevron-right"></em>-->
    <!--            </div>-->
    <!--        </div>-->

    <div class="infobox-container">
      <div class="infobox">
        <div class="title">Submit All</div>
        <button @click="submitAllForm">Submit All Form</button>
      </div>
      <div class="form-box">
        <div class="title">Add new form</div>
        <div>
          <label>
            <input type="number" v-model="textInputNumber" /> Number of text input
          </label>
        </div>
        <div>
          <label>
            <input type="number" v-model="numInputNumber" /> Number of number input
          </label>
        </div>
        <div>
          <label>
            <input type="number" v-model="fileInputNumber" /> Number of file input
          </label>
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
    <!--Data grid-->
    <div class="carousel-section" v-if="cards.length > 0">
      <carousel v-if="cards.length > 0" :cards="cards" />
    </div>
    <!--Data table-->
    <div class="table-section" v-if="cards.length > 0">
      <data-table :columns="['Name', 'Age', 'Avatar']" :rows="cards"></data-table>
    </div>
    <!--Card carousel-->
    <div class="grid-section">
      <card
        v-for="(item, index) in cards"
        :key="index"
        :name="item.name"
        :age="item.age"
        :imgName="item.imgName"
        :imgSource="item.imgSource"
      ></card>
    </div>
  </div>
</template>

<script>
import InputForm from "./InputForm";
import DataTable from "@/components/Table";
import Carousel from "@/components/Carousel";
import Card from "@/components/Card";

export default {
  components: {
    Carousel,
    DataTable,
    InputForm,
    Card,
  },
  props: {},
  data() {
    return {
      textInputNumber: 0,
      numInputNumber: 0,
      fileInputNumber: 0,
      totalInputForm: 0,
      formItems: [],
      items: [],
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
      // this.cards.push({
      //     name: "Hoang",
      //     age: 23,
      //     imgSource: "https://picsum.photos/200/200"
      // });
      // console.log("Submit all");
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
  width: 300px;
  height: 200px;
  margin: 0 20px 20px 0;
  border-radius: 20px;
  border: 1px solid #ccc;
  clear:both 

  div {
    left: 0;
    top: 0;
    width: 150px;
    height: 100px;
    position: absolute;
  }

}

.grid-section {
     display: grid;
     grid-template-columns: 1fr 1fr 1fr 1fr; 
}
</style>