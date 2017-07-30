<style>
.main {
    position: fixed;
    z-index: 999;
    bottom: 100px;
    color: #fff;
    background: #000;
    width: 100%;
}
.main ul{
    display: flex;
    width: 100%;
}
.main ul li{
    flex: 1;
    text-align: center;
    list-style: none;
    line-height: 44px;
}
</style>

<template>
    <div class="main">
        <ul>
            <li v-for="item in nav">{{item}}</li>
        </ul>
    </div>
</template>
<script>
export default {
  props:{
      nav:{
          type:Array,
          dafault:'',
      }
  }
}
</script>
