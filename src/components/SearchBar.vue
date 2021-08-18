<template>
  <div class="search__bar">
    <form class="search__form" @submit.prevent="submit">
      <input  type="search" class="search" placeholder="Введите слово для поиска анекдотов..."> 
      <button @click="searchHandler" type="submit" class="search__button"><i class="fa fa-search"></i></button>
    </form>
    <div class='list__block'>
            <ul class="list">
                <li 
                v-for='item in searchHandler'
                :key='item.id'
                :item_data="item"
                class="list__item"
                :class="{'liked': liked}"
                >
                {{ item.joke }}
                <i @click="changeLike" 
                :class="{'fas fa-thumbs-up': liked}" 
                class="far fa-thumbs-up"></i></li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    data() {
        return {
            data: []
        }
    },
    props: {
        jokes__arr: {
            type: Array,
            default: () => []
        },
        jokes__list: {
            type: Array,
            default: () => []
        }
    },
    created() {
        this.data = this.jokes__arr;
        console.log(this.data);
    },
    computed: {
        searchHandler(){
            return this.data;
        }
    },
    methods: {
        changeLike(){
        const likeButtons = document.querySelectorAll('.fa-thumbs-up');
            for(let i = 0; i < likeButtons.length; i++){  
                let btn = likeButtons[i];
                btn.addEventListener('click', function (e) {
                    if (e.target.className == 'far fa-thumbs-up' || e.target.className == 'fa-thumbs-up far') {
                        e.target.classList.add('fas');
                        e.target.classList.remove('far');
                        e.target.parentElement.classList.add('liked');
                    } else {
                        e.target.classList.add('far');
                        e.target.classList.remove('fas');
                        e.target.parentElement.classList.remove('liked');
                    }
                })
            }
        
        return;
        }
    },
}
</script>

<style scoped>
.search__bar{
    background-image: linear-gradient(130deg,rgba(255, 255, 255, 0.65), rgba(255, 255, 255, 0.3));
    border-radius: 20px;
}
.search__form{
    position: relative;
    width: 660px;
    border: none;
}
.search{
    font-family: 'Montserrat', sans-serif;
    font-weight: 400;
    outline: none;
    min-width: 656px;
    min-height: 58px;
    border: none;
    margin-left: 17px;
    margin-top: 15px;
    font-size: 1.4em;
    padding: 5px;
    background: rgb(255, 255, 255, 0);
    -webkit-appearance: none;
}
input::-webkit-search-decoration,
input::-webkit-search-cancel-button,
input::-webkit-search-results-button,
input::-webkit-search-results-decoration { display: none; }
input::-webkit-search-decoration,
input::-webkit-search-cancel-button,
input::-webkit-search-results-button,
input::-webkit-search-results-decoration { display: none; }
.search__button{
    position: absolute;
    top: 10px;
    right: 17px;
    margin: 2px;
    cursor: pointer;
    height: 50px;
    width: 50px;
    border: 1px solid #4291f8;
    border-radius: 50%;
    color: #4291f8;
    background: rgb(255, 255, 255, 0);
    font-size: 1em;
    transition: all .3s ease;
}
.search__button:hover{
    background: #4291f8;
    color: #fff;
}
.list__block {
    width: 660px;
    border-radius: 0 0 20px 20px;
    padding: 20px;
}
.list {
    list-style: none;
    background: rgba(255, 255, 255, 0);
}
.list__item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #4291f8;
    margin: 4px 2px;
    min-height: 60px;
    padding: 8px 15px;
    transition: border-radius .3s ease;
}
.list__item:hover {
    border-radius: 25px;
    background: rgba(255, 255, 255, 0.3);
}
.fas, .far {
    margin-left: 10px;
    cursor: pointer;
}
.far {
   color: #4291f8;
}
.fas {
    color: #f84269;
}
.far:hover {
    color: #f84269;
}
.liked {
    background: rgba(125, 255, 85, 0.4);
    border-radius: 25px;
}
.liked:hover {
    background: rgba(50, 235, 74, 0.7);
}
</style>