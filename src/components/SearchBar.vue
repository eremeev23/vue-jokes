<template>
  <form class="search__bar" >
      <input type="search" class="search" placeholder="Введите слово для поиска анекдотов..."> 
      <button type="submit" class="search__button"><i class="fa fa-search"></i></button>
  </form>
</template>

<script>
export default {

}
</script>

<style>
.search__bar{
    width: 660px;
    border: 2px solid #fff;
    box-shadow: 0 5px 10px #4291f8;
    background: #fff;
}
.search{
    outline: none;
    min-width: 600px;
    min-height: 50px;
    border: none;
    font-size: 1.4em;
    padding: 5px;
}
.search__button{
    margin: 2px;
    cursor: pointer;
    height: 50px;
    width: 50px;
    border: 1px solid #4291f8;
    border-radius: 50%;
    color: #4291f8;
    font-size: 1em;
    transition: all .3s ease;
}
.search__button:hover{
    background: #4291f8;
    color: #fff;
}
</style>