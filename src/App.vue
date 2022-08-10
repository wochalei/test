

<template>
<!-- 要求1 -->
  <div class="wrap">
    <div class="item" v-for="(item,index) in data" :key="index">
      <div class="title">
        <input type="checkbox" :id="'h'+item" v-model="item.checked" @change="toChangeFarter(item.kids)">
        <label :for="'h'+item">{{item.name}}</label>
        <div class="isShow" @click="toShow(index)">
          <span v-if="item.isShow">+</span>
          <span v-else>-</span>
        </div>
      </div>
      <div class="kids" v-if="item.isShow">
        <div class="kid" v-for="(item1,index1) in item.kids">
        <input type="checkbox" :id="'k'+item1.id" v-model="item1.checked" @change="toChangeKid">
        <label :for="'k'+item1.id">{{item1.name}}</label>
        </div>
      </div>
    </div>
  </div>

</template>
<script setup>

import { reactive, unref,computed } from 'vue';
/* 要求 6 7 */
const data = reactive([
  {
    id: 1,
    name: '部门1',
    checked: false,
    isShow:true,
    kids: [
      {
        id: 1,
        name: '小一',
        checked: false
      },
      {
        id: 2,
        name: '小二',
        checked: false
      },
      {
        id: 3,
        name: '小三',
        checked: false
      }
    ]
  },
  {
    id: 2,
    name: '部门2',
    checked: false,
    isShow:true,
    kids: [
      {
        id: 4,
        name: '小四',
        checked: false
      },
      {
        id: 5,
        name: '小五',
        checked: false
      },
      {
        id: 6,
        name: '小六',
        checked: false
      }
    ]
  },{
    id: 3,
    name: '部门3',
    checked: false,
    isShow:true,
    kids: [
      {
        id: 7,
        name: '小七',
        checked: false
      },
      {
        id: 8,
        name: '小八',
        checked: false
      },
      {
        id: 9,
        name: '小九',
        checked: false  
      }
    ]
  },
])
/* 要求2 */
const toShow = (index)=>{
  data[index].isShow=!data[index].isShow;
}
/* 要求3 */
const toReverse = (kids)=>{
  kids.forEach((item)=>{
    item.checked=!item.checked;
  })
}
/* 要求4  */
const isFull = ()=>{
    data.forEach((item,index)=>{
    let max = item.kids.length;
    let count = 0; 
    item.kids.forEach((kid)=>{
       if(kid.checked){
        count++;
       }
    })
    if(max===count) data[index].checked=true;
    else  data[index].checked=false;
  })
}
/* 要求5  */
const result = computed(()=>{
      let department = [],user=[];
      data.forEach(item=>{
        if(item.checked){
          department.push(item.id)
        }else{
          item.kids.forEach(kid=>{
            if(kid.checked) user.push(kid.id)
          })
        }
        
      })
      return {department,user};
})

const toPrint = ()=>{
   console.log(unref(result));
}
const toChangeFarter = (kids)=>{
  toReverse(kids)
  toPrint() 
}
const toChangeKid = ()=>{
  isFull()
  toPrint() 
}

</script>

<style scoped>
.item{
  margin-bottom: 10px;
}
.title{
  display: flex;
}

.isShow {
  margin-left: 5px;
}

.isShow span {
  display: block;
  width: 20px;
  line-height: 20px;
  border: 1px solid black;
  cursor: pointer;

}

input {
  margin-top: 6px;
}

.kids {
  display: flex;
  padding: 10px 0 0 40px;
}

.kid {
  margin-right: 8px;
}
</style>
