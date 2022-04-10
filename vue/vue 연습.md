```vue

<template>
  <h1 
  v-bind:[attr]="'active'"
  @[evnet]="add">
    {{msg}}
  </h1>
</template>

<script>
// 객체 리터럴 반환
export default {
  data() {
    return{
      msg:'active',
      attr:'class', // attr : attribute(속성)의 약어
      evnet:'click'
    }
  },
  methods:{
    add(){
      this.msg += '!'
    }
  }
}


</script>


<style scoped>
  .active{
    color:royalblue;
    font-size:100px;
  }
</style>
```

