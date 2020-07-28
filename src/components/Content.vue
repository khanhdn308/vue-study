<template>
  <div id="content">
    <div class="teaser">
      <div class="teaser-content">
        Read Article
        <em class="fas fa-chevron-right"></em>
      </div>
    </div>

    <div class="infobox-container">
      <div class="infobox">
        <div class="title">Submit All</div>
        <button @click="submitAllForm">Submit All Form</button>
      </div>
      <div class="form-box">
        <div class="title">Add new form</div>
        <div>
          <label>
            <input type="number"> Number of text input
          </label>
        </div>

        <div>
          <label>
            <input type="number"> Number of number input
          </label>
        </div>

        <div>
          <label>
            <input type="number"> Number of file input
          </label>
        </div>

        <button @click="addForm">Add Form</button>
      </div>
      <div class="infobox">
        <div class="title">Remove all forms</div>
        <button @click="removeAllForm">Remove All Forms</button>
      </div>
    </div>

    <div class="form-section">
      <input-form v-for="(item, index) in formItems" :input-detail="item" :key="index"
                  @close-form="closeForm($event)"></input-form>
    </div>

    <div class="table-section">
      <data-table></data-table>
    </div>
  </div>
</template>

<script>
import InputForm from "./InputForm";
import DataTable from "@/components/Table";

export default {
  components: {
    DataTable,
    InputForm
  },
  data() {
    return {
      totalInputForm: 1,
      formItems: [{
        id: 0, text: 2, number: 2, file: 2
      }],
      items: []
    }
  },
  methods: {
    addForm() {
      this.formItems.push({
        id: this.totalInputForm, text: 2, number: 2, file: 2
      });
      this.totalInputForm++;
    },
    closeForm(formId) {
      this.formItems = this.formItems.filter((inputItem) => {
        return inputItem.id !== formId;
      })
    },
    removeAllForm() {
      this.formItems = [];
      this.totalInputForm = 0;
    },
    addNewItem() {

    },
    submitAllForm() {
      console.log("Submit all");
    }
  }
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
  float: left;
  display: block;
  width: fit-content;
  height: 80px;
  padding: 10px;
  margin: 0 20px 20px 0;
  border-radius: 20px;
  border: 1px solid #ccc;

  div {
    float: left;
  }
}

</style>