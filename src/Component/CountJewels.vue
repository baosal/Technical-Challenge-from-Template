<template>
  <div>
    <b-container fluid>
      <b-row class="my-1">
        <b-col sm="3">
          <label>Enter types of stones that are jewels(unique) :</label>
        </b-col>
        <b-col sm="9">
          <input class='form-control' type="text" maxlength="50"
                v-model="typeList"
                @input="validateTypeList($event.target)">
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="3">
          <label>Enter stones you have:</label>
        </b-col>
        <b-col sm="9">
          <input class='form-control' type="text" maxlength="50"
                v-model="stoneList"
                @input="validateStoneList($event.target)">
        </b-col>
      </b-row>
      <b-row class="my-3">
        <b-col sm="12">
          <h5>The number of stones you have are also jewels is: {{countJewels}}</h5>
        </b-col>
      </b-row>
    </b-container>    
  </div>
</template>
<script>
  import regexRule from './regexRule'
  export default {
    name: 'CountJewels',
    computed: {
      stoneUniqList(){
            let result = this.stoneList.split('')
            return _.uniq(result)
      },
      // Return the number of jewels
      countJewels(){
            let typeArray = this.typeList.split('')
            let jeweryStone =  this.stoneUniqList.filter(stone => {
                 return typeArray.indexOf(stone) >= 0
            })
            return jeweryStone.length
      }
    },
    data() {
      return {
        typeList: '',
        stoneList: '',
      }
    },
    methods: {
      // User are allow to enter letter and guaranteed distinct only
      validateTypeList(e) {
        let oldValue = e._value
        if (regexRule.uniqueLetter.test(e.value.trim())) {
          oldValue = this.typeList
          e.oldSelectionStart = e.selectionStart
          e.oldSelectionEnd = e.selectionEnd
        } else {
          this.typeList = oldValue
          e.setSelectionRange(e.oldSelectionStart || e.selectionStart, e.oldSelectionEnd || e.selectionEnd)
        }
      },
      // User are allow to enter letter only
      validateStoneList(e) {
        let oldValue = e._value
        if (regexRule.letter.test(e.value.trim())) {
          oldValue = this.stoneList
          e.oldSelectionStart = e.selectionStart
          e.oldSelectionEnd = e.selectionEnd
        } else {
          this.stoneList = oldValue
          e.setSelectionRange(e.oldSelectionStart || e.selectionStart, e.oldSelectionEnd || e.selectionEnd)
        }
      }
    }
  }
</script>
<style>
.container-fluid{
  text-align: left;
}
</style>