<template>
<div class="container">
  <div class="row">
    <div class="col">
      <table class="main-table ml-5">
        <tr class="rowCell" v-for="item in row" :key="item">
          <td class="columnCell" v-for="item2 in column" :key="item2" :id="`${item}${item2}`" @click="clickFunction"> </td>
        </tr>
      </table>
    </div>
  </div>
</div>
</template>
<style lang="scss">
  // border 1px #aaa
  // border 2px #606c70
  // background row/column #F3EFE0
  // background cell #DCD0C0
  .this-item{
    background-color: #DCD0C0;
  }
  .relative-item{
    background-color: #F3EFE0;
  }

  .main-table{
    .rowCell{
      &:nth-child(1), &:nth-child(4), &:nth-child(7){
        border-top: 2px solid #606c70;
      }
      &:last-child{
        border-bottom: 2px solid #606c70;
      }

    }
    .columnCell{
      width: 60px;
      height: 60px;
      font-size: 35px;
      border: 1px solid #aaa;
      &:nth-child(1), &:nth-child(4), &:nth-child(7){
        border-left: 2px solid #606c70;
      }
      &:last-child{
        border-right: 2px solid #606c70;
      }
      &:hover{
        cursor: pointer;
      }
    }
  }

</style>
<script>
export default {
  data () {
    return {
      nowGroup: 'a1',
      nowId: 'A1',
      row: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'],
      column: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      group: {
        a1: ['A1', 'A2', 'A3', 'B1', 'B2', 'B3', 'C1', 'C2', 'C3'],
        a2: ['A4', 'A5', 'A6', 'B4', 'B5', 'B6', 'C4', 'C5', 'C6'],
        a3: ['A7', 'A8', 'A9', 'B7', 'B8', 'B9', 'C7', 'C8', 'C9'],
        b1: ['D1', 'D2', 'D3', 'E1', 'E2', 'E3', 'F1', 'F2', 'F3'],
        b2: ['D4', 'D5', 'D6', 'E4', 'E5', 'E6', 'F4', 'F5', 'F6'],
        b3: ['D7', 'D8', 'D9', 'E7', 'E8', 'E9', 'F7', 'F8', 'F9'],
        c1: ['G1', 'G2', 'G3', 'H1', 'H2', 'H3', 'I1', 'I2', 'I3'],
        c2: ['G4', 'G5', 'G6', 'H4', 'H5', 'H6', 'I4', 'I5', 'I6'],
        c3: ['G7', 'G8', 'G9', 'H7', 'H8', 'H9', 'I7', 'I8', 'I9']
      },
      index: []
    }
  },
  methods: {
    findGroup (cellId) {
      let groupChar = ''
      let groupNum = 0
      if (this.row.indexOf(cellId.split('')[0]) <= 2) {
        groupChar = 'a'
      } else if (this.row.indexOf(cellId.split('')[0]) > 5) {
        groupChar = 'c'
      } else {
        groupChar = 'b'
      }

      if (cellId.split('')[1] <= 3) {
        groupNum = 1
      } else if (cellId.split('')[1] > 6) {
        groupNum = 3
      } else {
        groupNum = 2
      }
      console.log(`${groupChar}${groupNum}`)
      return `${groupChar}${groupNum}`
    },
    clickFunction (e) {
      console.log(e)
      console.log(e.target.id)
      this.nowId = e.target.id
      this.nowGroup = this.findGroup(this.nowId)
      this.setColor(this.nowId)
    },
    setColor (cellId) {
      const ele = document.getElementById(`${cellId}`)
      const otherEle = document.getElementsByClassName('columnCell')
      ele.classList.remove('relative-item')
      ele.classList.add('this-item')
      for (const i in otherEle) {
        if (!isNaN(Number(i))) {
          if (otherEle[i].id !== cellId) {
            if (otherEle[i].id.indexOf(cellId.split('')[0]) !== -1 || otherEle[i].id.indexOf(cellId.split('')[1]) !== -1) {
              otherEle[i].classList.add('relative-item')
            } else if (this.group[this.nowGroup].indexOf(otherEle[i].id) !== -1) {
              otherEle[i].classList.add('relative-item')
            } else {
              otherEle[i].classList.remove('relative-item')
              otherEle[i].classList.remove('this-item')
            }
          }
        }
      }
    }
  },
  mounted () {
    this.setColor(this.nowId)
  }
}
</script>
