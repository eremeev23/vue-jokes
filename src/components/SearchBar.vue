<template>
  <div class="search__bar">
    <form class="search__form" @submit.prevent="submit">
      <input  type="search" v-model="search" class="search" placeholder="Введите слово для поиска анекдотов...">
      <button @click="filteredItems" class="search__button"><i class="fa fa-search"></i></button>
      <div class="select">
            <select @click="filterLikedJokes" name="jokes__list" class="options">
                <option value="all">All</option>
                <option value="liked">Liked</option>
            </select>
        </div>
    </form>
    <div class='list__block'>
            <ul class="list">
                <li 
                v-for='item in filteredItems'
                :key='item.id'
                :item_data="item"
                class="list__item"
                >
                {{ item.joke }}
                <i @click="changeLike"
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
            search: '',
            data: [],
            likedJokes: []
        }
    },
    props: {
        jokes__arr: {
            type: Array,
            default: () => []
        }
    },
    created() {
        this.data = this.jokes__arr;
    },
    computed: {
        //Search for joke with key word
        filteredItems() {
            return this.jokes__arr.filter(elem => {
                return elem.joke.toLowerCase().includes(this.search.toLowerCase());
            })
        }
    },
    methods: {
        //Like the joke, save the joke's status and remove the joke's status
        changeLike(e){
            const item = e.target;
            const likedJoke = item.parentElement;

            if (item.className == 'far fa-thumbs-up' || item.className == 'fa-thumbs-up far') {
                item.classList.add('fas');
                item.classList.remove('far');
                likedJoke.classList.add('liked');
                this.likedJokes.push(likedJoke.innerText);
                localStorage.setItem('likedJokes', JSON.stringify(this.likedJokes));
            } else {
                const todoIndex = likedJoke.children[0].innerText;
                item.classList.add('far');
                item.classList.remove('fas');
                item.parentElement.classList.remove('liked');
                this.likedJokes.splice(this.likedJokes.indexOf(todoIndex), 1);
                localStorage.setItem('likedJokes', JSON.stringify(this.likedJokes));
            }
            return;
        },
        //Filter for all and liked jokes
        filterLikedJokes(e){
            const list = document.querySelector('.list')
            const jokesList = list.childNodes;
            jokesList.forEach(function(joke){
                switch(e.target.value){
                    case 'all':
                        joke.style.display = 'flex';
                    break;
                    case 'liked':
                        if (joke.classList.contains('liked')) {
                            joke.style.display = 'flex';
                        } else {
                            joke.style.display = 'none';
                        }
                    break;
                }
            })
        }
    }
}
</script>

<style scoped>
.search__bar{
    background-image: linear-gradient(130deg,rgba(255, 255, 255, 0.65), rgba(255, 255, 255, 0.3));
    border-radius: 20px;
    max-height: 80%;
}
.search__form{
    position: relative;
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 660px;
}
.search{
    font-family: 'Montserrat', sans-serif;
    font-weight: 400;
    outline: none;
    min-width: 500px;
    min-height: 58px;
    border: none;
    font-size: 1.4em;
    padding: 5px;
    background: rgb(255, 255, 255, 0);
    -webkit-appearance: none;
}
input::-webkit-search-decoration,
input::-webkit-search-cancel-button,
input::-webkit-search-results-button,
input::-webkit-search-results-decoration { 
    display: none; 
}
input::-webkit-search-decoration,
input::-webkit-search-cancel-button,
input::-webkit-search-results-button,
input::-webkit-search-results-decoration { 
    display: none; 
}
.select {
    height: 80%; 
}
.options {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  outline: none;
  border: none;
  border-radius: 20px;
  color: #4291f8;
  cursor: pointer;
  width: 6.5rem;
  padding: .7rem;
  background: #fff;
  font-size: 1.1em;
}
.options option{
    width: 100%;
    font-size: 1.1em;
}
.select::after {
  color: #4291f8;
  content: "\25bc";
  position: absolute;
  background: #fff;
  top: 50%;
  transform: translateY(-50%);
  right: 22px;
  padding: .5rem;
  pointer-events: none;
  border-radius: 50%;
  transition: all .3s ease;
}
.select:hover::after {
    color: #fff;
    background: #4291f8;
}
.search__button{
    position: absolute;
    right: 130px;
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
    padding: 0 20px 20px;
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