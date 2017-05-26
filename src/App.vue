<template>
  <div id="app">
    <div class="columns">
      <div class="column is-4 is-offset-4">
        <div class="box">
          <center>Grade Calculator</center>
          <b-field>
              <b-input placeholder="Name of Subject" type="text" v-model="input.subject"></b-input>
          </b-field>
          <b-field>
              <b-input placeholder="Credit" type="number" v-model="input.credit"></b-input>
          </b-field>
          <b-field>
              <b-input placeholder="Grade" type="text" v-model="input.grade"></b-input>
          </b-field>
          <center><a class="button is-primary is-outlined" @click="add()">Add</a></center>
        </div>
      </div>
    </div>
    <div class="columns" v-if="num === 1">
      <div class="column is-6 is-offset-3">
        <div class="box">
          <table class="table is-narrow  is-striped">
            <tr>
              <td>Subject</td>
              <td>Credit</td>
              <td>Grade</td>
            </tr>
            <tr v-for="item in showGrade">
              <td>{{item.subject}}</td>
              <td>{{item.credit}}</td>
              <td>{{item.grade}}</td>
            </tr>
          </table>

          <center><a class="button is-primary is-outlined" @click="cal()">Calculate</a></center>
        </div>
      </div>
    </div>

          <div class="columns" v-if="check>0">
            <div class="column is-4 is-offset-4">

                <div class="modal is-active" >
                  <div class="modal-background"></div>
                  <div class="modal-content">
                    <div class="box" >
                      Total Score : {{totalScore}}<br>
                      Total Credit : {{totalCre}}<br>
                      GPA : {{gpa}}
                    </div>
                  </div>
                  <button class="modal-close" @click="cloesMo()"></button>
                </div>

          </div>
        </div>

  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  },
  data () {
    return {
      gpa:0,
      check:0,
      num:0,
      totalCre:0,
      totalScore:0,
    input:{
        subject: '',
        credit: '',
        grade: ''
      },
     showGrade:[]
  }
  },
  methods: {
    add () {
      let vm = this
      vm.showGrade.push(this.input)
      if(this.input.grade === "A" || this.input.grade === "a"){
        vm.totalScore += vm.input.credit * 4
      }
      if(this.input.grade === "B+" || this.input.grade === "b+"){
        vm.totalScore += vm.input.credit * 3.5
      }
      if(this.input.grade === "B" || this.input.grade === "b"){
        vm.totalScore += vm.input.credit * 3
      }
      if(this.input.grade === "C+" || this.input.grade === "c+"){
        vm.totalScore += vm.input.credit * 2.5
      }
      if(this.input.grade === "C" || this.input.grade === "c"){
        vm.totalScore += vm.input.credit * 2
      }
      if(this.input.grade === "D+" || this.input.grade === "d+"){
        vm.totalScore += vm.input.credit * 1.5
      }
      if(this.input.grade === "D" || this.input.grade === "d"){
        vm.totalScore += vm.input.credit * 1
      }
      if(this.input.grade === "F" || this.input.grade === "f"){
        vm.totalScore += vm.input.credit * 0
      }
      vm.totalCre += parseInt(vm.input.credit)
      this.num = 1
      this.input = {
          subject: '',
          credit: '',
          grade: ''
        }
    },
    cal () {
      this.check = 1
      this.gpa = this.totalScore/this.totalCre
      this.gpa = this.gpa.toFixed(2)
    },
    closeMo () {
      this.check = 0
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.colorBG {
  background-color:  #f2f2f2;
}
</style>
