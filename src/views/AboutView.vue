<template>
  <div class="about d-flex justify-content-center">
    <table class="ml-5">
      <tr class="rowCell" v-for="item in row" :key="item">
        <td class="columnCell" v-for="item2 in rowList" :key="item2" :id="`${item}${item2}`" @click="ckickFunction">
          7
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      row: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'],
      column: [0, 1, 2, 3, 4, 5, 6, 7, 8],
      rowList: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      index: []
    }
  },
  methods: {
    setIndex () {
      // this.row.forEach(row_item => {
      //   this.column.forEach(col_item => {

      //   })
      // })
    },
    ckickFunction (e) {
      console.log(e)
      console.log(e.target.id)
      const nowId = e.target.id
      const ele = document.getElementById(`${e.target.id}`)
      const otherEle = document.getElementsByClassName('columnCell')
      for (var i in otherEle) {
        if (!isNaN(Number(i))) {
          if (otherEle[i].id.indexOf(nowId.split('')[0]) !== -1 || otherEle[i].id.indexOf(nowId.split('')[1]) !== -1) {
            otherEle[i].style['background-color'] = '#F3EFE0'
          } else {
            otherEle[i].style['background-color'] = 'white'
          }
        }
      }
      ele.style['background-color'] = '#DCD0C0'
    }
  }
}
</script>
<style lang="scss">
  // border 1px #aaa
  // border 2px #606c70
  // background row/column #F3EFE0
  // background cell #DCD0C0
  table{
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
      font-size: 30px;
      border: 1px solid #aaa;
      &:nth-child(1), &:nth-child(4), &:nth-child(7){
        border-left: 2px solid #606c70;
      }
      &:last-child{
        border-right: 2px solid #606c70;
        background-color: #F3EFE0;
      }
    }
    .rowCell:first-child{
      &:last-child(){
        background-color: #DCD0C0;
      }
    }
  }
</style>
