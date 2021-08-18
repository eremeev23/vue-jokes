<template>
    <div class='list__block'>
        <ul class="list">
            <li 
            v-for='item in jokes__list'
            :key='item.id'
            :item_data="item"
            class="list__item"
            >{{ item.joke }}<i @click="changeLike" class="far fa-thumbs-up"></i></li>
        </ul>
    </div>
</template>

<script>
export default{
    props: {
        jokes__list: {
            type: Array,
            default: () => []
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


<style>
.list__block{
    width: 660px;
    background: #fff;
}
.list{
    list-style: none;
}
.list__item{
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #4291f8;
    margin: 4px 2px;
    min-height: 60px;
    padding: 8px 15px;
}
.list__item:hover{
    border: 2px solid #4291f8;
}
.fas, .far{
    margin-left: 10px;
    cursor: pointer;
}
.far {
   color: #4291f8;
}
.fas{
    color: #f84269;
}
.far:hover{
    color: #f84269;
}
.liked{
    background: rgba(125, 255, 85, 0.3);
}
</style>